---
layout: post
categories: blog
comments: true
author: Mark Cheverton
title: QOS1 added to the Arduino MQTT library
description: How to use Quality of Service level 1 (guaranteed at least once delivery) in the Arduino MQTT library
---

> [MQTT][] is a lightweight messaging protocol for the [Internet of
> Things][].
> This post details the use of QoS level 1 (guaranteed at least once delivery)
> in the [Arduino][] MQTT [library][pubsubclient].

When you want your shiny new _thing_ to send or receive data, the most common
approach is to periodically connect to a web server and use HTTP to
poll for updates or to send data home.

There are a number of drawbacks with this model. Firstly it's not
real-time, so any application where the device needs to respond quickly
needs to be polling on a short interval to reduce lag.
Secondly you're using HTTP as a messaging system and as
you move from tens, to hundreds, to thousands of devices all manically
chattering away, you'll start
to hit scaling issues. Newer protocols such as
websockets add a real-time layer to HTTP and can ameliorate these
problems, but you'll still have to create your own routing so that the
messages flow to and from the right _things_.

This is a solved problem in other domains where
queuing systems (also known as enterprise service buses, or message
brokers) are a common element of modern distributed architectures, most
adhering to a common standard called [AMQP][]. Queuing systems support
message delivery based on a loosely coupled data-centric [publish/subscribe model][pubsub] rather than a network-centric push/pull model.

However, for the Internet of Things, AMQP is too big a protocol to run
on devices such as [Arduino][], so I haven't been able to
use queuing systems with my IoT projects. However, before Christmas, I was excited to discover
[MQTT][] - an open standard which aims
to deliver a lightweight messaging protocol suitable for IoT. Thanks to [Nick O'Leary][] from IBM, there
was already an [MQTT Arduino library][pubsubclient] available which was
fairly trivial to get hooked up to the MQTT plugin for [RabbitMQ][] - my messaging server of choice.

MQTT has a concept called Quality of Service which can be either 0, 1,
or 2. At level 0, messages are sent out 'fire and forget', at level 1,
an acknowledgement is expected to confirm the message has been processed at
least once, and at level 2 an acknowledgement of receipt is also added to
make sure that the message is only delivered to one consumer to be processed exactly once.

Nick's library only supported QoS0, which for most IoT applications
would be just fine - a few dropped sensor readings here or there isn't
usually too much of a problem. However, for this particular project I'm sending
larger messages (monochrome bitmaps) over the queue. RabbitMQ and MQTT can handle the
large messages, and the Arduino was also okay because it would
only process one message at a time, but RabbitMQ would keep sending messages as they
arrived, so if the Arduino was busy they would pile up in the Ethernet buffer until it overflowed.

Normally you'd get RabbitMQ to buffer the
messages using the `prefetch` setting which limits the number of
simultaneous messages sent to a consumer. But because Nick's library
only supported QoS1, RabbitMQ had no way to know when the Arduino was
ready for the next message and so it just sends them instantly - a
ready-made denial of service attack.

So to cut a long story short I added QoS1 support into the library and
after a bit of polish, my pull request has been accepted by Nick
to the main repo. Now, when you subscribe to a topic, you can add the QoS level as follows:

```c++
mqttClient.subscribe("inTopic", 1);
```

If you have a look in the RabbitMQ management console you should now see
that your queue name contains `qos1`. You don't need to do
anything else as the library will
automatically deal with the acknowledgements as messages are receieved.
So if you want to limit the number sent, as I did, then all you need to do is
add the `prefetch` setting to your [rabbitmq.conf][]:

```erlang
[{rabbitmq_mqtt, [{default_user,     <<"guest">>},
                  {default_pass,     <<"guest">>},
                  {allow_anonymous,  true},
                  {vhost,            <<"/">>},
                  {exchange,         <<"amq.topic">>},
                  {subscription_ttl, 1800000},
                  {prefetch,         1},
                  {ssl_listeners,    []},
                  {tcp_listeners,    [1883]},
                  {tcp_listen_options, [binary,
                                        {packet,    raw},
                                        {reuseaddr, true},
                                        {backlog,   128},
                                        {nodelay,   true}]}]}
].
```

Now RabbitMQ will only send one message and then wait for an ACK before
it sends the next, keeping the backlog safely in the queue.

[Arduino]: http://arduino.cc/
[Internet of Things]: http://en.wikipedia.org/wiki/Internet_of_Things
[MQTT]: http://mqtt.org/ "Message Queue Telemetry Transport"
[AMQP]: http://amqp.org/ "Advanced Message Queuing Protocol"
[pubsub]: http://en.wikipedia.org/wiki/Publish–subscribe_pattern "Wikipedia: Publish Subscribe Pattern"
[Nick O'Leary]: http://twitter.com/knolleary
[pubsubclient]: https://github.com/knolleary/pubsubclient
[rabbitmq.conf]: http://www.rabbitmq.com/configure.html
[RabbitMQ]: http://rabbitmq.com/
