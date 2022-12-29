---
title: Stream processing in Ruby
excerpt: Introducing Qswarm, a DSL implementing a stream processing agent framework for Ruby
tags:
  - ruby
  - steam-processing
---

Reactive applications seems to have been the new hotness this year. Whether it’s at a conference about Big Data, DevOps or IoT, the same use case is coming up repeatedly - the need to process real-time streams of data. There’s even a [reactive programming manifesto][Reactive Manifesto] for those really feeling the need to get polemical about it.

A couple of years back I did a piece of consultancy work where I needed to process twitter data and catch a load of web hooks to provide real-time reporting on a big social media campaign. I was taking the opportunity to have a play with [RabbitMQ][] and needed an easy way to manage a swarm of small separate agents doing simple processing operations on queues... [Qswarm][], my own little reactive framework, was born.

Roll forward to 2013 and I’m back to messing about with queues again and deciding that my initial implementation of the Qswarm DSL needs an overhaul. So after a considerable syntax re-write, and a decent period of testing with real data, I’m releasing the new version of Qswarm and bumping it to version 1.0.

Enough back story, let’s dive in to some examples. Qswam initially ships with a small number of clients which allow you to `source` and `sink` data from AMQP, Twitter, and XMPP.  Here’s a simple chatbot programme to source data from an AMQP queue and dump it to an XMPP server such as [Hipchat][].

```ruby
agent :mybot do
  connect :hipchat,
          :type            => :xmpp,
          :jid             => '54321_123456@chat.hipchat.com',
          :real_name       => 'MyBot',
          :channel         => ['54321_lounge@conf.hipchat.com', '54321_chat@conf.hipchat.com'],
          :password        => 'foobar'

  connect :messages,
          :type            => :amqp,
          :uri             => 'guest:guest@localhost:5672/',
          :exchange_type   => :topic,
          :exchange_name   => 'messages',
          :bind            => '#',
          :format          => :raw

  source  :messages do
    case payload.routing_key
    when /^wall\./
      sink :hipchat
    when /^channel\.(.*)/
      sink  :hipchat,
            :channel       => "54321_#{$1}@conf.hipchat.com"
    end
  end
end
```

The first `connect` sets up the XMPP connection, in this case to Hipchat, passing an initial set of groupchat rooms to join. The second `connect` sets up the XMPP stream subscribing to a # wildcard on the messages topic exchange and specifying the messages will be raw (i.e. plain text rather than json or XML).

The final section is where the flow logic is setup. We `source` messages from the `:messages` connection and then dependant on the routing key, `sink` them either to all the groupchat rooms if its a wall, or to a specific room based on the routing key. Save the above file as bot.swarm and let's give it a test with the RabbitMQ command line:

```sh
qswarm bot.swarm &
rabbitmqadmin publish exchange=messages routing_key=channel.lounge payload="Test message"
```

Now we have our chat bot running, let's see if we can feed it a tweetstream. For this you'll need to get oauth connection details from dev.twitter.com.

```ruby
agent :twitter do
  connect :amqp,
          :type            => :amqp,
          :uri             => 'guest:guest@localhost:5672/',
          :exchange_type   => :headers,
          :exchange_name   => 'twitter',
          :format          => :json

  connect :twitter,
          :type            => :twitter,
          :consumer_key    => 'YOURKEYHERE',
          :consumer_secret => 'YOURSECRETHERE',
          :oauth_token     => 'YOURTOKENHERE',
          :oauth_token_secret => 'YOURSECRETHERE',
          :track           => {
            :colours         => ['red', 'green', 'blue'],
            :feelings        => ['happy', 'sad'],
            :tech            => ['ruby', 'python'],
          },
          :follow          => {
            :tech            => [11987892]
          },
          :list            => {
            :flibbertigibbets     => { 'Scobleizer' => 'most-influential-in-tech' }
          }

  source :twitter do
    case payload.headers[:type]
    when :follow
      sink :amqp,
           :routing_key    => "follow.#{payload.data[:user][:id]}"

    when :track
      sink :amqp,
           :routing_key  => "track.#{agent.name}"

    when :list
      sink :amqp,
           :routing_key  => "list.#{payload.headers[:user_id]}.#{payload.headers[:slug]}"
    end
  end
end
```

The twitter source allows you to track keywords used in tweets, follow particular users, and track tweets from people in lists. The flow logic in this case takes each of these twitter events and pumps them into an exchange with the appropriate routing key. We're using a headers exchange in this case as the twitter client adds useful headers to the payload (used in the `case` statement):

* **:type** => :track, **:group** => colours|feelings|tech, **:matches** => [red|green|blue|happy|sad|ruby|python]
* **:type** => :follow, **:group** => tech, **:user_id** => 11987892
* **:type** => :list, **:group** => flibbertigibbets, **:user_id** => Scobleizer, **:slug** => most-influential-in-tech

Now lets wire this up to our bot with a final agent that routes between the `twitter` exchange and the `messages` exchange.

```ruby
agent :chirp do
  connect :twitter,
          :type            => :amqp,
          :uri             => 'guest:guest@localhost:5672/',
          :exchange_type   => :headers,
          :exchange_name   => 'twitter',
          :bind            => '#',
          :format          => :json

  connect :messages,
          :type            => :amqp,
          :uri             => 'guest:guest@localhost:5672/',
          :exchange_type   => :topic,
          :exchange_name   => 'messages',
          :format          => :raw

  before :twitter do
    @pp = "<#{payload.data[:user][:name]}/#{payload.data[:user][:screen_name]}> #{payload.data[:text]}"
    payload.data[:entities][:user_mentions].each do |u|
      @pp.gsub!(/@#{u[:screen_name]}/,"<#{u[:name]}/#{u[:screen_name]}>")
    end
  end

  source  :twitter, :type => 'list' do
    if payload.data[:text].match(/awesome/)
      sink  :messages,
            :routing_key     => "wall.#{agent.name}",
            :data            => @pp
    end
  end

  source  :twitter, :group => 'tech' do
    sink  :messages,
          :routing_key     => 'channel.tech',
          :data            => @pp
  end

  source  :twitter, :type => 'track', :group => %w( colours feelings ) do
    sink  :messages,
          :routing_key     => 'channel.chat',
          :data            => @pp
  end

  source  :twitter, :type => 'list', :slug => 'most-influential-in-tech' do
    sink  :messages,
          :routing_key      => 'channel.lists',
          :data             => @pp
  end
end
```

We're doing a couple of new things here. Firstly the before statement allows us to register a `filter` which we're using to format the message. The source statements also have `guards` on them which allows us to do conditional execution based on the headers. Finally in the first source statement you can see we're using data from the message payload - in this case the tweet which has been turned into a Ruby Hash as we specified JSON format in the connection.

Putting all the code together and running it with Qswarm should now give you a selection of tweets filtered to different channels. Of course you could equivalently resort to a simpler script which takes a stream from twitter and sends it straight to Hipchat without the intermediate exchanges, but the intention was to show what could be done in a more complicated decoupled setup using all the clients.


[Reactive Manifesto]: http://www.reactivemanifesto.org/ "The reactive manifesto"
[RabbitMQ]: http://www.rabbitmq.com/
[Qswarm]: http://github.com/ennui2342/qswarm
[Hipchat]: http://www.hipchat.com/
