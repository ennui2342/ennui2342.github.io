---
layout: post
categories: blog
comments: true
author: Mark Cheverton
title: Stream support for the Arduino MQTT library
description: Added the ability to write large payloads to Stream compatible storage
---

> [MQTT][] is a lightweight messaging protocol for the [Internet of
> Things][].
> This post details the use of Stream support for large payload storage
> in the [Arduino][] MQTT [library][pubsubclient].

MQTT is a lightweight protocol, but that doesn't mean that the
payloads have to be small. The
[spec](http://public.dhe.ibm.com/software/dw/webservices/ws-mqtt/mqtt-v3r1.html) was designed to allow for messages up to
256MB, but taking advantage of this with an Arduino can be difficult as they usually only have [small amounts of
memory](http://arduino.cc/en/Tutorial/Memory) in three pools:

- Flash memory where the Arduino sketch is stored (32k in an Atmega328)
- SRAM where the sketch creates and manipulates variables when it runs (2k in an Atmega328)
- EEPROM that programmers can use to store long-term information (1k in an Atmega328)

Which makes receiving any payloads of any size via MQTT problematic.
Common external storage options to beef up your Arduino project include [SD
cards](http://arduino.cc/en/Reference/SD) and
[SRAM chips](http://playground.arduino.cc/Main/SpiRAM). These come with
control libraries that inherit from the [Arduino Stream
class](http://arduino.cc/en/Reference/Stream) - a standard
interface for manipulating character and binary based streams (also used by
Ethernet and Serial amongst others).

For my latest project I got hold of a 23LC1024 - a 1024KB SPI SRAM chip with
5V logic levels making it easy to work with my 5V Arduino.
I wanted to pass fairly large binary bitmaps around
by MQTT, so I added support to [Nick's][Nick O'Leary] [MQTT Arduino library][pubsubclient]
for storing payloads using Stream objects.

I started by wiring the SRAM up to the Arduino's SPI pins as follows:

![Circuit diagram](/images/arduino-sram-schematic.png)

There is currently no standard Arduino SRAM library (the Arduino site
lists one, but the files are 404) so I knocked up a
[simple library](https://github.com/ennui2342/arduino-sram) which supports the 23LC1024.
It should be good for the 23K256 as well, but I haven't had one handy to
do a test.

In the trivial example code below, we're taking any message that comes through
on `inTopic` writing it to SRAM and then reading it back and writing it
to the serial console.

```c++
#include <SPI.h>
#include <Ethernet.h>
#include <PubSubClient.h>
#include <SRAM.h>

// Update these with values suitable for your network.
byte mac[]    = {  0xDE, 0xED, 0xBA, 0xFE, 0xFE, 0xED };
byte mqtt_server[] = { 172, 16, 0, 2 };

SRAM sram(10, SRAM_1024);

void callback(char* topic, byte* payload, unsigned int length) {
  sram.seek(1);

  // do something with the message
  for(uint8_t i=0; i<length; i++) {
    Serial.write(sram.read());
  }
  Serial.println();
  
  // Reset position for the next message to be stored
  sram.seek(1);
}

EthernetClient ethClient;
PubSubClient client(mqtt_server, 1883, callback, ethClient, &sram);

void setup() {
  Ethernet.begin(mac);
  if(client.connect("arduinoClient")) {
    client.subscribe("inTopic");
  }

  sram.begin();
  sram.seek(1);
  
  Serial.begin(9600);
}

void loop() {
  client.loop();
}
```

Note that the Stream object (sram) is passed to PubSubClient as the last argument of the instantiator to let it know you want
it to write payloads to the SRAM. I'm storing the payloads at memory position 1, so
I move there in `setup` with the `seek` method.

Once a payload is received `callback` executes. I move to memory
position 1, read the message back and write it to the console, then move back to
memory position 1 again ready for the next message to be written (if
you were using an SD card for storage you might be opening and closing
Files instead of moving to memory postitions).

The nice thing about this approach to storage is that many libraries will take a Stream object for
manipulation which makes it easy to pass off a message for processing.
I'll take a bit more in my next blog post about how I used this approach
to make use of 3rd party libraries to process my images.

[Arduino]: http://arduino.cc/
[Internet of Things]: http://en.wikipedia.org/wiki/Internet_of_Things
[MQTT]: http://mqtt.org/ "Message Queue Telemetry Transport"
[Nick O'Leary]: http://twitter.com/knolleary
[pubsubclient]: https://github.com/knolleary/pubsubclient
