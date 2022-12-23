---
title: Internet of Things kit for hackdays/spaces
excerpt: Defining a kit for an Internet of Things hackday or hackerspace
---

Roughly every quarter my employer, [Red Gate](http://www.red-gate.com/),
has a 'Down Tools Week' which is a week long opportunity to
hack on ideas that never get space in a normal work day. This cycle
our theme is the Internet of Things, so I'm pulling together kits to get
people up and running. The key criteria are:

* The audience is primarily software engineers so minimise the
  electronics knowledge required
* Eliminate the need for hardware hacking skills such as soldering
* Provide enough diversity of kit (more than just a pile of Arduino's)
  to enable people to create something interesting and useful within the week
* The parts shouldn't be too expensive and should be fairly mainstream

Here's what I have so far. If you have ideas on alternatives or things
I've missed then add to the comments at the end. I've listed the original supplier
(Sparkfun, Adafruit etc) as well as the UK distributor I
used (mostly Proto Pic or Farnell).

# Networking

I'd like people to experiment with different options for networking
IoT devices. So I started with the following kits:

## Bluetooth Low Energy

> Bluetooth Low Energy (BLE) or Bluetooth Smart is an update to the
> Bluetooth spec which allows for very low power consumption making it
> ideal for IoT devices and wearables. Newer generation Android and
> IPhones support BLE out of the box allowing direct interfacing from
> mobile applications.

![RFduino](/assets/images/rfduino.jpg "RFduino")
![BLEduino](/assets/images/bleduino.jpg "BLEduino")
![BLE shield](/assets/images/bleshield.jpg "BLE shield")
![BLE mini](/assets/images/blemini.jpg "BLE mini")

There are a couple of really nice kickstarters proving single board
Arduino-based BLE devices - [RFduino][] and [BLEduino][]. I missed both
when they were doing their campaigns and they're a bit hazy
on when they would be able to ship. So decided to go
the more pedestrian route and get a separate board.
[RedBearLab][] make a couple of nice looking ones -
the [BLE shield][] or the [BLE mini][] so I grabbed one of the latter.

* BLE mini ([Seeedstudio](http://www.seeedstudio.com/depot/Bluetooth-40-Low-Energy-BLE-Mini-p-1366.html?cPath=19_21) / [Proto Pic](http://proto-pic.co.uk/ble-mini-bluetooth-4-0-low-energy/))

## ZigBee

> ZigBee is a specification for a suite of high level communication
> protocols used to create personal area networks built from small,
> low-power digital radios. Though low-powered, ZigBee devices can
> transmit data over long distances by passing data through intermediate
> devices to reach more distant ones, creating a mesh network.

![XBee Explorer USB](/assets/images/sparkfun-xbee-explorer-usb.png "XBee Explorer USB")
![Arduino Wireless Shield](/assets/images/arduino-wireless-shield.jpg "Arduino Wireless Shield")
![Slice of Pi](/assets/images/slice-of-pi.jpg "Slice of Pi")
![XBee](/assets/images/xbee.jpg "XBee")

This is an easy one as the [XBee][] kit is a commonly used for IoT. I
decided that for ease of use I'd get three parts: An [XBee Explorer
USB][] for direct serial connection from a laptop to aid debugging,
a Arduino with the [Wireless Shield][Arduino Wireless Shield] to act as a device, and a Raspberry Pi
with a [Slice of Pi][] to act as a hub. Top off with a couple of [series 2 XBee modules][Sparkfun XBee buying guide].

* Xbee explorer USB ([Sparkfun](https://www.sparkfun.com/products/8687) / [Proto Pic](http://proto-pic.co.uk/xbee-explorer-usb/))
* Arduino wireless shield ([Farnell](http://uk.farnell.com/arduino/a000065/prototype-board-wireless-sd-card/dp/2075344))
* Slice of Pi ([Ciseco](http://shop.ciseco.co.uk/slice-of-pi-add-on-for-raspberry-pi/))
* Xbee module v2 ([Farnell](http://uk.farnell.com/digi-international/xb24-z7wit-004/zigbee-module-xbee-zb-wire-ant/dp/1690810?Ntt=XB24-Z7WIT-004))

## Radio Frequency Identification (RFID)

> RFID is the wireless non-contact use
> of radio-frequency electromagnetic fields to transfer data, for the
> purposes of automatically identifying and tracking tags attached to
> objects.

![RWD Dev Board](/assets/images/rwd-dev-board.jpg "RWD Dev Board")
![RWD Hitag 2](/assets/images/rwd-hitag2.jpg "RWD Hitag 2")

We have a HiTag2 based [Paxton](http://www.paxton-access.co.uk) system at Red Gate.
[ib technology][] do a reader module which is easy to use
through a simple serial interface (more on this in a later blog post).
So I picked up their [RWD Dev board][], and a [RWD-HiTag2][] module.

* RWD-Hitag2 ([ibtechnology](http://www.buyrfid.co.uk/store/index.php?route=product/product&path=36&product_id=56))
* RWD dev board ([ibtechnology](http://www.buyrfid.co.uk/store/index.php?route=product/product&path=39&product_id=58))

## Near Field Communication (NFC)

> Near field communication (NFC) is a set of standards for smartphones
> and similar devices to establish radio communication with each other
> by touching them together or bringing them into proximity, usually no
> more than a few inches.

![mbed](/assets/images/mbed.jpg "mbed")
![PN532 breakout board](/assets/images/pn532.jpg "PN532 breakout board")

NFC doesn't seem to be well supported on the Arduino - in particular it won't work
with phones which is the fun bit! Adafruit to the rescue again with
their [mbed NFC starter pack](http://www.adafruit.com/products/836) which includes an mbed and their PN532
breakout board all driven by the &mu;NFCstack developed by local
Cambridge company [AppNearMe][].

* mbed NFC starter pack ([Adafruit](http://www.adafruit.com/products/836))

## Lightweight Local Automation Protocol (LLAP)

> [LLAP][] is an easy to use, licence free, "open" and standardised method
> to send data between local networks of low cost wired or wireless
> devices. Designed by UK company [Ciseco][] and
> implemented in their ISM band (868 to 915 Mhz) RF kit.

![SRF Stick](/assets/images/srf-stick.jpg "SRF Stick")
![Slice of Radio](/assets/images/slice-of-radio.jpg "Slice of Radio")
![Arduino Wireless Shield](/assets/images/arduino-wireless-shield.jpg "Arduino Wireless Shield")
![XRF Module](/assets/images/xrf-module.jpg "XRF Module")

[Ciseco][] are a small UK company who are doing nice bits of kit at a low
price, so I really wanted to support them and get them into the mix.
Similar to the ZigBee setup, I went for a [SRF stick][] for laptop
debugging, a Raspberry Pi with [Slice of Radio][] as a hub, and an Arduino with
the [Wireless Shield][Arduino Wireless Shield] and an [XRF module][] to act as a device.

* SRF stick ([Ciseco](http://shop.ciseco.co.uk/srf-stick-868-915-mhz-easy-to-use-usb-radio/))
* Slice of Radio ([Ciseco](http://shop.ciseco.co.uk/slice-of-radio-wireless-rf-transciever-for-the-raspberry-pi/))
* Arduino wireless shield ([Farnell](http://uk.farnell.com/arduino/a000065/prototype-board-wireless-sd-card/dp/2075344))
* XRF module ([Ciseco](http://shop.ciseco.co.uk/xrf-wireless-rf-radio-uart-rs232-serial-data-module-xbee-shape-arduino-pic-etc/))
* 4Gb SD card for Ciesco ([Ciseco](http://shop.ciseco.co.uk/4gb-wheezy-raspberry-pi-sd-card-configured-for-ciseco-products/))

## GSM

> GSM (Global System for Mobile Communications)
> is a standard developed by the European Telecommunications
> Standards Institute (ETSI) to describe protocols for second generation
> (2G) digital cellular networks used by mobile phones.

![GPRS Quadband Module](/assets/images/gsm-shield.png "GPRS Quadband Module")

I've not had a lot of experience with using mobile networks for devices.
3G network modules seem a bit expensive, so after a bit of hunting around I
decided to experiment with the [GPRS+GPS Quadband module for Arduino / Raspberry
Pi](http://www.cooking-hacks.com/gprs-gps-quadband-module-for-arduino-sim908)
from [Cooking Hacks][] - if you're going to be on the move then might as
well throw in GPS!

* GPRS Quadband module ([Cooking Hacks](http://www.cooking-hacks.com/gprs-gps-quadband-module-for-arduino-sim908))
* GPRS antenna ([Cooking Hacks](http://www.cooking-hacks.com/internal-4g-3g-gprs-gsm-antenna))
* GPS antenna ([Cooking Hacks](http://www.cooking-hacks.com/internal-gps-antenna))

## Wifi

> Wi-Fi is a popular technology that allows
> an electronic device to exchange data or connect to the internet
> wirelessly using radio waves.

![Adafruit CC3000](/assets/images/adafruit-cc3000.png "Adafruit CC3000")
![Spark Core](/assets/images/spark-core.jpg "Spark Core")

The easiest, but not necessarily cheapest or most efficient, option
is to connect your device directly to the Internet by Wifi.
Adafruit do a lovely little SPI board at a reasonable price for the [TI CC3000][] wifi
chip. I also couldn't resist an Arduino compatible [Spark Core][], which is also CC3000
based - hopefully it will arrive in time.

* CC3000 breakout ([Adafruit](http://www.adafruit.com/products/1469) / [Proto Pic](http://proto-pic.co.uk/adafruit-cc3000-wifi-breakout-with-onboard-ceramic-antenna/))
* Spark core ([Spark Core](https://www.spark.io))

## Low power IPv6 (6LowPan, RPL, CoAP)

> IETF protocols for low-power IPv6 networking, including the 6lowpan
> adaptation layer, the RPL IPv6 multi-hop routing protocol, and the
> CoAP RESTful application-layer protocol.

![Openmote](/assets/images/openmote.jpg "Openmote")

Had a bit of trouble finding affordable options for this. 
Using a Raspberry Pi as a hub with the [Contiki
OS][] (an OS in 40Kb of RAM!) looks like a viable option, but getting
cheap nodes seems difficult - Arduino Megas running
[&mu;IPv6](https://github.com/telecombretagne/Arduino-IPv6Stack) are
kind of supported, but the Arduino port doesn't seem very active or
loved.

I did spend a long time admiring [Libelium's Waspmotes][Waspmotes] which seems
a very polished platform, but in the end I decided on
[Openmote][] who are building out
boards based on the TI CC2538 system on a chip. This will allow
2.4GHz 802.15.4 communications via a CC2520 radio paired with an ARM
Cortex M3 and will be compatible with 6LowPan style platforms such as
Thingsquare, Libelium and Contiki.

* Open mote ([Openmote](http://www.openmote.com))

# Platforms / Software

Platform recommendations are difficult as there are so many to choose
from at the moment - this is a whole blog post on its own. At the moment I'm just pointing people
towards some of the most well known to get experience:

* Backends: [Xively][], [Thingworx][]
* 6LowPan: [Thingsquare][], [Libelium][]
* Other software: [Node-Red][], [MQTT][], [The Thing System][]

# Microcontrollers

#### Arduino

![Arduino](/assets/images/arduino.jpg)

The [Arduino][] will be the primary platform due to it's low cost and ease
of use.

* Arduino Uno ([Farnell](http://uk.farnell.com/arduino/a000066/atmega328-arduino-uno-eval-board/dp/2075382))
* Arduino sidekick basic kit ([Cooking Hacks](http://www.cooking-hacks.com/arduino-sidekick-basic-kit))

#### Raspberry Pi

![Raspberry Pi](/assets/images/raspberrypi.png)

Not really a microcontroller, but for hubs and gateways, the [Raspberry Pi][]
makes an ideal device. We'll also pick up some extras that we'll need ...

* Raspberry Pi model B & 8Gb SD ([Farnell](http://uk.farnell.com/raspberry-pi/raspberry-pi-8gb-usd/sbc-raspberry-pi-8gb-sd-bundle/dp/2334982))
* Raspberry Pi PSU 5V 1A ([Farnell](http://uk.farnell.com/raspberry-pi-psu/rpi-psu-uk-mk1/power-supply-raspberry-5v-1a-uk/dp/2254792))
* GPIO Breakout Board with Cable ([Proto Pic](http://proto-pic.co.uk/gpio-breakout-board-with-cable/))
* Slice of Relay ([Ciseco](http://shop.ciseco.co.uk/slice-of-relay/))
* WiFi dongle ([Farnell](http://uk.farnell.com/element14/wipi/dongle-wifi-usb-for-raspberry-pi/dp/2133900#))
* Pi Camera ([Farnell](http://uk.farnell.com/raspberry-pi/rpi-camera-board/raspberry-pi-camera-board-5mp/dp/2302279#))
* Pi NoIR camera ([Farnell](http://uk.farnell.com/raspberry-pi/rpi-noir-camera-board/raspberry-pi-noir-camera-board/dp/2357308))
* Dynamode CR-31 Card Reader ([Farnell](http://uk.farnell.com/dynamode/cr-31/card-reader-9-in-1-sim/dp/2081767))
* USB Hub with interface expansion ([Farnell](http://uk.farnell.com/ftdi/rpi-hub-module/module-interface-expansion-for/dp/2147355))
* Cerberus USB Cable - 6ft w hub ([Sparkfun](https://www.sparkfun.com/products/12016) / [Proto Pic](http://proto-pic.co.uk/sparkfun-cerberus-usb-cable-6ft-with-internal-hub/))
* Embest - Pi Arduino board ([Farnell](http://uk.farnell.com/embest/embedded-pi/rpi-arduino-like-stm32-i-o-board/dp/2301086))

#### Javascript

![Tessel](/assets/images/tessel.png)
![Espurino](/assets/images/espruino.jpg)

Our developers love Javascript and it's event driven model is very well
suited to the reactive world of IoT applications. The [Tessel][] and
[Espruino][] are two interesting kickstarter projects to build
microcontrollers that run Javascript. There's a great Makezine [comparison of the two
boards](http://makezine.com/magazine/first-look-javascript-micro-controllers-for-web-developers/) by [Alasdair Allan](https://twitter.com/aallan).
Hopefully I'll be able to grab one of each to play with.

* Tessel ([Tessel](http://tessel.io))
* Espurino ([Phenoptix](http://www.phenoptix.com/products/espruino-board-javascript-on-an-arm-based-board))

#### Wearables

![Flora](/assets/images/flora.jpg)

There's no company more interesting than [Adafruit][] when it comes to
wearable tech. So picking up a Flora Sensor
Pack to play with was a no-brainer.

* Flora sensor pack ([Adafruit](http://www.adafruit.com/products/1458))

# Sensors and Actuators

#### Sensors

![SensorTag](/assets/images/sensortag.jpg)
![Electret microphone](/assets/images/electret.jpg)
![HRLV-EZ1](/assets/images/HRLV-EZ1.jpg)
![Flex Sensor](/assets/images/flexsensor.jpg)

The drive here was to focus on breakout boards to remove the need for
electronics skills.

* Triple Axis Magnetometer Breakout - HMC5883L ([Sparkfun](https://www.sparkfun.com/products/10530) / [Proto Pic](http://proto-pic.co.uk/triple-axis-magnetometer-breakout-hmc5883l/))
* Triple Axis Accelerometer and Gyro Breakout - MPU-6050 ([Sparkfun](https://www.sparkfun.com/products/11028) / [Proto Pic](http://proto-pic.co.uk/triple-axis-accelerometer-and-gyro-breakout-mpu-6050/))
* Piezo Vibration Sensor - Large Mass ([Sparkfun](https://www.sparkfun.com/products/9197) / [Proto Pic](http://proto-pic.co.uk/piezo-vibration-sensor-large-mass/))
* Flex Sensor 2.2" ([Sparkfun](https://www.sparkfun.com/products/10264) / [Proto Pic](http://proto-pic.co.uk/flex-sensor-2-2/))
* Force Sensitive Resistor 0.5" ([Sparkfun](https://www.sparkfun.com/products/9375) / [Proto Pic](http://proto-pic.co.uk/force-sensitive-resistor-0-5/))
* SoftPot Membrane Potentiometer - 50mm ([Sparkfun](https://www.sparkfun.com/products/8680) / [Proto Pic](http://proto-pic.co.uk/softpot-membrane-potentiometer-50mm/))
* Reed switch ([Sparkfun](https://www.sparkfun.com/products/8642) / [Proto Pic](http://proto-pic.co.uk/reed-switch/))
* Magnet square - 0.25" ([Sparkfun](https://www.sparkfun.com/products/8643) / [Proto Pic](http://proto-pic.co.uk/magnet-square-0-25/))
* PIR motion sensor ([Sparkfun](https://www.sparkfun.com/products/8630) / [Proto Pic](http://proto-pic.co.uk/pir-motion-sensor/))
* Ultrasonic Range Finder - Maxbotix HRLV-EZ1 ([Sparkfun](https://www.sparkfun.com/products/11308) / [Proto Pic](http://proto-pic.co.uk/ultrasonic-range-finder-maxbotix-hrlv-ez1/))
* HIH-4030 Humidity Sensor Breakout ([Sparkfun](https://www.sparkfun.com/products/9569) / [Proto Pic](http://proto-pic.co.uk/hih-4030-humidity-sensor-breakout/))
* IR receiver breakout ([Sparkfun](https://www.sparkfun.com/products/8554) / [Proto Pic](http://proto-pic.co.uk/ir-receiver-breakout/))
* Mini Photocell ([Sparkfun](https://www.sparkfun.com/products/9088) / [Proto Pic](http://proto-pic.co.uk/mini-photocell/))
* Optical Detector / Phototransistor ([Sparkfun](https://www.sparkfun.com/products/246) / [Proto Pic](http://proto-pic.co.uk/optical-detector-phototransistor/))
* Altitude/Pressure Sensor - MPL3115A2 Breakout ([Sparkfun](https://www.sparkfun.com/products/11084) / [Proto Pic](http://proto-pic.co.uk/altitude-pressure-sensor-mpl3115a2-breakout/))
* Flora sensor pack ([Adafruit](http://www.adafruit.com/products/1458))
* Gas sensor breakout board ([Sparkfun](https://www.sparkfun.com/products/8891) / [Proto Pic](http://proto-pic.co.uk/gas-sensor-breakout-board/))
* Alcohol gas sensor ([Sparkfun](https://www.sparkfun.com/products/8880) / [Proto Pic](http://proto-pic.co.uk/alcohol-gas-sensor-mq-3/))
* CO gas sensor ([Sparkfun](https://www.sparkfun.com/products/9403) / [Proto Pic](http://proto-pic.co.uk/carbon-monoxide-sensor-mq-7/))
* Non-Invasive Current Sensor - 30A ([Sparkfun](https://www.sparkfun.com/products/11005) / [Proto Pic](http://proto-pic.co.uk/non-invasive-current-sensor-30a/))
* Conductive Rubber Cord Stretch Sensor ([Adafruit](http://www.adafruit.com/products/519) / [Proto Pic](http://proto-pic.co.uk/conductive-rubber-cord-stretch-sensor-extras/))
* Liquid level sensor ([Sparkfun](https://www.sparkfun.com/products/10221) / [Proto Pic](http://proto-pic.co.uk/liquid-level-sensor/))
* Load sensor 50kg ([Sparkfun](https://www.sparkfun.com/products/10245) / [Proto Pic](http://proto-pic.co.uk/load-sensor-50kg/))
* Tilt sensor ([Sparkfun](https://www.sparkfun.com/products/10289) / [Proto Pic](http://proto-pic.co.uk/tilt-sensor/))
* 1/2" flow sensor ([Seedstudio](http://www.seeedstudio.com/depot/G12-Water-Flow-Sensor-p-635.html?cPath=25_32) / [Proto Pic](http://proto-pic.co.uk/g-1-2-water-flow-sensor/))
* Infrared Emitters and Detectors Pair ([Sparkfun](https://www.sparkfun.com/products/241) / [Proto Pic](http://proto-pic.co.uk/infrared-emitters-and-detectors-pair/))
* Photo Interrupter GP1A57HRJ00F ([Sparkfun](https://www.sparkfun.com/products/9299) / [Proto Pic](http://proto-pic.co.uk/photo-interrupter-gp1a57hrj00f/))
* Photo Interrupter GP1A57HRJ00F Breakout Board ([Sparkfun](https://www.sparkfun.com/products/9322) / [Proto Pic](http://proto-pic.co.uk/photo-interrupter-gp1a57hrj00f-breakout-board/))
* QRE1113 Line Sensor Breakout - Analogue ([Sparkfun](https://www.sparkfun.com/products/9453) / [Proto Pic](http://proto-pic.co.uk/qre1113-line-sensor-breakout-analogue/))
* Color Light Sensor ADJD-S311-CR999 ([Proto Pic](http://proto-pic.co.uk/color-light-sensor-evaluation-board/))
* Magnetic contact switch (door sensor) ([Adafruit](http://www.adafruit.com/products/375) / [Proto Pic](http://proto-pic.co.uk/magnetic-contact-switch-door-sensor/))
* Hall effect sensor ([Sparkfun](https://www.sparkfun.com/products/9312) / [Proto Pic](http://proto-pic.co.uk/hall-effect-sensor/))
* Magnet ring ([Sparkfun](https://www.sparkfun.com/products/8914) / [Proto Pic](http://proto-pic.co.uk/magnet-ring-3-16/))
* Temperature Sensor - Waterproof (DS18B20) ([Sparkfun](https://www.sparkfun.com/products/11050) / [Proto Pic](http://proto-pic.co.uk/temperature-sensor-waterproof-ds18b20/))
* VCNL4000 Infrared Emitter/Proximity ([Sparkfun](https://www.sparkfun.com/products/10901) / [Proto Pic](http://proto-pic.co.uk/vcnl4000-infrared-emitter-breakout/))
* Pressure-Sensitive Conductive Sheet ([Adafruit](http://www.adafruit.com/products/1361) / [Proto Pic](http://proto-pic.co.uk/pressure-sensitive-conductive-sheet-velostat-linqstat/))
* Electret Microphone Amplifier - MAX4466 with Adjustable Gain ([Adafruit](http://www.adafruit.com/products/1063))
* TSL2561 digital luminosity / lux / light sensor ([Adafruit](http://www.adafruit.com/products/439))
* SensorTag ([Farnell](http://uk.farnell.com/texas-instruments/cc2541dk-sensor/cc2541-sensortag-bluetooth-dev/dp/2334329))

TI's [SensorTag][] is worth special mention - it's a BLE device which has a six on-board sensors and its
own iOS and Android SDKs. Alasdair does another great Make blog post
[tearing it down](http://makezine.com/2013/04/18/teardown-of-the-ti-sensortag/).

#### Motors, steppers, servos, buttons, switches and claws

![Robotic Claw](/assets/images/roboticclaw.jpg)
![](/assets/images/servo.jpg)
![](/assets/images/keypad.jpg)
![](/assets/images/solenoid.jpg)

We want to interact with the world not just measure it ...

* 3v relay board ([Ciseco](http://shop.ciseco.co.uk/kit-relay-board-simple-to-use-3v-operation-supports-logic-level-also/))
* 3v to 5v Bistable Latching relay ([Ciseco](http://shop.ciseco.co.uk/3v-to-5v-bistable-latching-relay-kit/))
* 4 channel Arduino relay shield ([Seeedstudio](http://www.seeedstudio.com/depot/Relay-shield-p-693.html?cPath=73) / [Proto Pic](http://proto-pic.co.uk/4-channel-relay-shield-for-arduino/))
* VS1053 Codec + MicroSD Breakout - MP3/WAV/MIDI/OGG Play + Record - v2 ([Adafruit](http://www.adafruit.com/products/1381))
* 5v Solenoid ([Sparkfun](https://www.sparkfun.com/products/11015) / [Proto Pic](http://proto-pic.co.uk/solenoid-5v-small/))
* 12V Solenoid Valve - 3/4" ([Sparkfun](https://www.sparkfun.com/products/10456) / [Proto Pic](http://proto-pic.co.uk/12v-solenoid-valve-3-4/))
* Robotic Claw - MKII ([Sparkfun](https://www.sparkfun.com/products/11524) / [Proto Pic](http://proto-pic.co.uk/robotic-claw-mkii/))
* Medium servo ([Sparkfun](https://www.sparkfun.com/products/10333) / [Proto Pic](http://proto-pic.co.uk/servo-medium/))
* Surface Transducer - Small ([Sparkfun](https://www.sparkfun.com/products/10917) / [Proto Pic](http://proto-pic.co.uk/surface-transducer-small/))
* Vibrating Mini Motor Disc ([Adafruit](http://www.adafruit.com/products/1201))
* Motor/Stepper/Servo shield v2 ([Adafruit](http://www.adafruit.com/products/1438) / [Proto Pic](https://proto-pic.co.uk/adafruit-motor-stepper-servo-shield-for-arduino-v2-kit-v2-0/))
* 16-Channel 12-bit PWM/Servo Driver TLC5940  ([Sparkfun](https://www.sparkfun.com/products/10616) / [Proto Pic](http://proto-pic.co.uk/tlc5940-breakout/))
* 9 gram servo ([Proto Pic](http://proto-pic.co.uk/analogue-9-gram-servo/))
* 3 channel servo tester ([Proto Pic](http://proto-pic.co.uk/3-channel-servo-tester/))
* Servo Cable - Female to Female ([Sparkfun](https://www.sparkfun.com/products/9187) / [Proto Pic](http://proto-pic.co.uk/servo-cable-female-to-female/))
* Big easy stepper driver ([Sparkfun](https://www.sparkfun.com/products/11876) / [Proto Pic](http://proto-pic.co.uk/big-easy-driver/))
* Small stepper motor ([Sparkfun](https://www.sparkfun.com/products/10551) / [Proto Pic](http://proto-pic.co.uk/small-stepper-motor/))
* L298 Dual H-Bridge Motor Driver ([Seedstudio](http://www.seeedstudio.com/depot/L298-Dual-HBridge-Motor-Driver-p-284.html?cPath=91_92) / [Proto Pic](http://proto-pic.co.uk/l298-dual-h-bridge-motor-driver/))
* QIK Dual Serial Motor Controller ([Pololu](http://www.pololu.com/picture/view/0J1027) / [Proto Pic](http://proto-pic.co.uk/qik-dual-serial-motor-controller/))
* Brushed DC Motor: 130-Size 800mA Stall 6V 11.5kRPM ([Proto Pic](http://proto-pic.co.uk/brushed-dc-motor-130-size-6v-11-5krpm-800ma-stall/) / [Pololu](http://www.pololu.com/product/1117))
* Small Arcade Joystick ([Adafruit](http://www.adafruit.com/products/480) / [Proto Pic](http://proto-pic.co.uk/small-arcade-joystick/))
* Thumb joystick - Analogue ([Sparkfun](https://www.sparkfun.com/products/9032) / [Proto Pic](http://proto-pic.co.uk/thumb-joystick-analogue/))
* Breakout board for thumb joystick ([Sparkfun](https://www.sparkfun.com/products/9110) / [Proto Pic](http://proto-pic.co.uk/breakout-board-for-thumb-joystick/))
* Keypad - 12 Button ([Sparkfun](https://www.sparkfun.com/products/8653) / [Proto Pic](http://proto-pic.co.uk/keypad-12-button/))
* Pull Chain Switch ([Sparkfun](https://www.sparkfun.com/products/11136) / [Proto Pic](http://proto-pic.co.uk/pull-chain-switch/))
* Tactile Button Assortment ([Sparkfun](https://www.sparkfun.com/products/10302) / [Proto Pic](http://proto-pic.co.uk/tactile-button-assortment/))
* Concave Button - Blue ([Sparkfun](https://www.sparkfun.com/products/9337) / [Proto Pic](http://proto-pic.co.uk/concave-button-blue/))
* Concave Button - Red ([Sparkfun](https://www.sparkfun.com/products/9336) / [Proto Pic](http://proto-pic.co.uk/concave-button-red/))
* Concave Button - Green ([Sparkfun](https://www.sparkfun.com/products/9341) / [Proto Pic](http://proto-pic.co.uk/concave-button-green/))
* Concave button - yellow ([Sparkfun](https://www.sparkfun.com/products/9338) / [Proto Pic](http://proto-pic.co.uk/concave-button-yellow/))
* Rotary Encoder LED Ring Breakout Board - Blue ([Sparkfun](https://www.sparkfun.com/products/10407) / [Proto Pic](http://proto-pic.co.uk/rotary-encoder-led-ring-breakout-board-blue/))
* SPDT slide switch ([Sparkfun](https://www.sparkfun.com/products/9609) / [Proto Pic](http://proto-pic.co.uk/spdt-slide-switch/))
* Toggle Switch and Cover - Illuminated (Blue) ([Sparkfun](https://www.sparkfun.com/products/11313) / [Proto Pic](http://proto-pic.co.uk/toggle-switch-and-cover-illuminated-blue/))
* Silicone Elastomer 4x4 Button Keypad - for 3mm LEDs ([Adafruit](http://www.adafruit.com/products/1611))
* Adafruit Trellis Monochrome Driver PCB for 4x4 Keypad & 3mm LEDs ([Adafruit](http://www.adafruit.com/products/1616))
* Tactile on/off switch ([Adafruit](http://www.adafruit.com/products/1092))
* IR remote module for Arduino / Raspberry Pi ([Cooking Hacks](http://www.cooking-hacks.com/hvac-ir-remote-module-for-arduino-raspberry-pi))

# The Basics

We also need all the basics. Here's my initial list which I'm sure I'll
be revising as I discover things I've forgotten.

#### Misc breakout boards

![OpenLog](/assets/images/openlog.jpg)

* 8 channel logic level converter ([Adafruit](http://www.adafruit.com/products/395) / [Proto Pic](http://proto-pic.co.uk/8-channel-bi-directional-logic-level-converter-txb0108/))
* ADS1115 16-Bit ADC ([Adafruit](http://www.adafruit.com/products/1085) / [Proto Pic](http://proto-pic.co.uk/ads1115-16-bit-adc-4-channel-with-programmable-gain-amplifier/))
* OpenLog ([Sparkfun](https://www.sparkfun.com/products/9530) / [Proto Pic](http://proto-pic.co.uk/openlog/))

#### Tools

![Breadboard](/assets/images/breadboard.jpg)

* Farnell tool kit ([Farnell](http://uk.farnell.com/farnell/1pk-302n-f-uk/tool-kit-large-electronics/dp/3170603?dimVals=110444201))
* Alligator Test Leads - Multicolored 10 Pk ([Sparkfun](https://www.sparkfun.com/products/11037) / [Proto Pic](http://proto-pic.co.uk/alligator-test-leads-multicolored-10-pack/))
* Half-size breadboard ([Farnell](http://uk.farnell.com/wisher/wbu-301j/bread-board-proto-type-84mm-x-56/dp/1472862))
* FTDI Voltage Selectable board ([Proto Pic](http://proto-pic.co.uk/ftdi-voltage-selectable-board/))

#### Consumables

![Jumpers](/assets/images/jumpers.jpg)

* Beginner Parts Kit ([Sparkfun](https://www.sparkfun.com/products/10003) / [Proto Pic](http://proto-pic.co.uk/beginner-parts-kit-new/))
* Resistor Kit 1/4W ([Sparkfun](https://www.sparkfun.com/products/10969) / [Proto Pic](http://proto-pic.co.uk/resistor-kit-1-4w/))
* Break Away Headers - Right Angle ([Sparkfun](https://www.sparkfun.com/products/553) / [Proto Pic](http://proto-pic.co.uk/break-away-headers-right-angle/))
* Break Away Headers - Straight ([Sparkfun](https://www.sparkfun.com/products/116) / [Proto Pic](http://proto-pic.co.uk/break-away-headers-straight/))
* Break Away Female Headers ([Sparkfun](https://www.sparkfun.com/products/115) / [Proto Pic](http://proto-pic.co.uk/break-away-female-headers/))
* Hook-Up Wire - Assortment (Solid Core) ([Sparkfun](https://www.sparkfun.com/products/11367) / [Proto Pic](http://proto-pic.co.uk/hook-up-wire-assortment-solid-core/))
* Hook-Up Wire - Assortment (Stranded) ([Sparkfun](https://www.sparkfun.com/products/11375) / [Proto Pic](http://proto-pic.co.uk/hook-up-wire-assortment-stranded/))
* Jumper Wire - JST Black Red ([Sparkfun](https://www.sparkfun.com/products/8670) / [Proto Pic](http://proto-pic.co.uk/jumper-wire-jst-black-red/))
* JST Right-Angle Connector Thru-Hole 2Pin ([Sparkfun](https://www.sparkfun.com/products/9749) / [Proto Pic](http://proto-pic.co.uk/jst-right-angle-connector/))
* Breadboard Jumper wires ([Seeedstudio](http://www.seeedstudio.com/depot/Breadboard-Jumper-Wire-Pack200mm165mm125mm80mm-p-234.html?cPath=44_47) / [Proto Pic](http://proto-pic.co.uk/breadboard-jumper-wire-pack/))
* Ribbon Cable - 10 wire (3ft) ([Sparkfun](https://www.sparkfun.com/products/10649) / [Proto Pic](http://proto-pic.co.uk/ribbon-cable-10-wire-3ft/))
* 3ply conductive thread ([Adafruit](http://www.adafruit.com/products/641))
* 2ply conductive thread ([Adafruit](http://www.adafruit.com/products/640))
* Copper tape ([Sparkfun](https://www.sparkfun.com/products/10561) / [Proto Pic](http://proto-pic.co.uk/copper-tape-5mm-50ft/))
* Magnet Wire Kit ([Sparkfun](https://www.sparkfun.com/products/11363) / [Proto Pic](http://proto-pic.co.uk/magnet-wire-kit/))
* 2Gb MicroSD ([Farnell](http://uk.farnell.com/sandisk/sd4661/memory-micro-sd-2gb/dp/1795130))

#### Power

![Lipo](/assets/images/lipo.jpg)

* Battery Holder 2xAA Cover Switch JST ([Sparkfun](https://www.sparkfun.com/products/9547) / [Proto Pic](http://proto-pic.co.uk/battery-holder-2xaa-with-cover-and-switch/))
* Battery holder 4xAA with switch ([Sparkfun](https://www.sparkfun.com/products/12083) / [Proto Pic](http://proto-pic.co.uk/4-x-aa-battery-holder-with-on-off-switch/))
* 9v battery holders with switch & barrel ([Adafruit](http://www.adafruit.com/products/67))
* 2x 2032 Coin Cell Holder - 6V ([Adafruit](http://www.adafruit.com/products/783) / [Proto Pic](http://proto-pic.co.uk/coin-cell-battery-holder-2-x-cr2032-6v-output-with-on-off-switch/))
* Coin Cell Holder - 20mm ([Sparkfun](https://www.sparkfun.com/products/783) / [Proto Pic](http://proto-pic.co.uk/coin-cell-holder-20mm/))
* Sewable CR2032 Battery Holder ([Sparkfun](https://www.sparkfun.com/products/8822) / [Proto Pic](http://proto-pic.co.uk/coin-cell-holder-sewable-smd/))
* DC Barrel Jack Adapter - Female ([Sparkfun](https://www.sparkfun.com/products/10288) / [Proto Pic](http://proto-pic.co.uk/dc-barrel-jack-adapter-female/))
* DC Barrel Jack Adapter - Male ([Sparkfun](https://www.sparkfun.com/products/10287) / [Proto Pic](http://proto-pic.co.uk/dc-barrel-jack-adapter-male/))
* Barrel Jack to 2-pin JST ([Sparkfun](https://www.sparkfun.com/products/8734) / [Proto Pic](http://proto-pic.co.uk/barrel-jack-to-2-pin-jst/))
* LiPo battery 3.7v 2500mAh ([Adafruit](http://www.adafruit.com/products/328) / [Proto Pic](http://proto-pic.co.uk/lithium-ion-polymer-battery-3-7v-2500mah/))
* LiPo Battery 3.7v 850mAh ([Sparkfun](https://www.sparkfun.com/products/341) / [Proto Pic](http://proto-pic.co.uk/polymer-lithium-ion-battery-850mah/))
* LiPo Battery 3.7v 400mAh ([Sparkfun](https://www.sparkfun.com/products/10718) / [Proto Pic](http://proto-pic.co.uk/polymer-lithium-ion-battery-400mah/))
* LiPo battery 3.7v 40mAh ([Sparkfun](https://www.sparkfun.com/products/11316) / [Proto Pic](http://proto-pic.co.uk/polymer-lithium-ion-battery-40mah/))
* USB/DC LiPo charger 5-12V - 3.7/4.2v ([Adafruit](http://www.adafruit.com/products/280))
* CR2032 Lithium Coin Cell Battery ([Farnell](http://uk.farnell.com/multicomp/cr2032/cell-lithium-cr2032-210mah-3v/dp/2065171))
* 9v battery x4 ([Farnell](http://uk.farnell.com/duracell/5000394020092/battery-alkaline-plus-9v-pk4/dp/2062015))
* 12 pack AA battery ([Farnell](http://uk.farnell.com/duracell/5000394017825/battery-alkaline-plus-aa-pk12/dp/2345257))

#### Optical

![Neopixels](/assets/images/neopixels.jpg)

* LED starter kit ([Sparkfun](https://www.sparkfun.com/products/9878) / [Proto Pic](http://proto-pic.co.uk/led-starter-kit/))
* i2c / SPI character LCD backpack ([Adafruit](http://www.adafruit.com/products/292) / [Proto Pic](http://proto-pic.co.uk/i2c-spi-character-lcd-backpack/))
* Basic 16x2 Character LCD - Black on Green 5V ([Sparkfun](https://www.sparkfun.com/products/255) / [Proto Pic](http://proto-pic.co.uk/basic-16x2-character-lcd-black-on-green-5v/))
* Basic 20x4 Character LCD - Black on Green 5V ([Sparkfun](https://www.sparkfun.com/products/256) / [Proto Pic](http://proto-pic.co.uk/basic-20x4-character-lcd-black-on-green-5v/))
* Monochrome 1.3" 128x64 OLED ([Adafruit](http://www.adafruit.com/products/938) / [Proto Pic](http://proto-pic.co.uk/monochrome-1-3-128x64-oled-graphic-display/))
* 0.56" 4Digit 7Seg I2C Blue ([Adafruit](http://www.adafruit.com/products/881) / [Proto Pic](http://proto-pic.co.uk/adafruit-0-56-4-digit-7-segment-display-w-i2c-backpack-blue/))
* 0.56" 4Digit 7Seg I2C Yellow ([Adafruit](http://www.adafruit.com/products/879) / [Proto Pic](http://proto-pic.co.uk/adafruit-0-56-4-digit-7-segment-display-w-i2c-backpack-yellow/))
* 4x Breadboard RGB Smart NeoPixel ([Adafruit](http://www.adafruit.com/products/1312) / [Proto Pic](http://proto-pic.co.uk/breadboard-friendly-rgb-smart-neopixel-pack-of-4/))
* NeoPixel RGB LED Weatherproof 30 LED 1m  BLACK ([Adafruit](http://www.adafruit.com/products/1460) / [Proto Pic](http://proto-pic.co.uk/adafruit-neopixel-digital-rgb-led-weatherproof-strip-30-led-1m-black/))
* Adafruit NeoPixel NeoMatrix 8x8 - 64 RGB LED Pixel Matrix ([Adafruit](http://www.adafruit.com/products/1487) / [Proto Pic](http://proto-pic.co.uk/adafruit-neopixel-neomatrix-8x8-64-rgb-led-pixel-matrix/))
* AdaFruit NeoPixel Ring - 16 x WS2812 5050 RGB LED with Integrated Drivers ([Adafruit](http://www.adafruit.com/products/1463) / [Proto Pic](http://proto-pic.co.uk/adafruit-neopixel-ring-16-x-ws2812-5050-rgb-led-with-integrated-drivers/))
* NeoPixel Stick - 8 x WS2812 5050 RGB LED with Integrated Drivers ([Adafruit](http://www.adafruit.com/products/1426) / [Proto Pic](http://proto-pic.co.uk/neopixel-stick-8-x-ws2812-5050-rgb-led-with-integrated-drivers/))
* Aqua EL Wire Starter Pack - 2.5 Metres ([Adafruit](http://www.adafruit.com/products/545) / [Proto Pic](http://proto-pic.co.uk/aqua-el-wire-starter-pack-2-5-metres/))

Let me know what you think of the selection in the comments, particularly whether there's anything I
missed, or your own favourite kit lists.

[LLAP]: http://openmicros.org/index.php/articles/85-llap-lightweight-local-automation-protocol/297-llap-reference
[Ciseco]: http://www.ciseco.co.uk/
[Spark Core]: https://www.spark.io
[XBee Series 1]: http://www.digi.com/products/wireless-wired-embedded-solutions/zigbee-rf-modules/point-multipoint-rfmodules/xbee-series1-module
[Tessel]: http://tessel.io
[Espruino]: http://www.espruino.com
[Adafruit]: http://www.adafruit.com
[Rfduino]: http://www.rfduino.com
[BLEduino]: http://bleduino.cc
[BLE shield]: http://redbearlab.com/bleshield/
[BLE mini]: http://redbearlab.com/blemini/
[RedBearLab]: http://redbearlab.com
[XBee]: http://www.digi.com/products/wireless-wired-embedded-solutions/zigbee-rf-modules/zigbee-mesh-module/
[XBee Explorer USB]: https://www.sparkfun.com/products/8687
[Arduino Wireless Shield]: http://arduino.cc/en/Main/ArduinoWirelessShield
[Slice of Pi]: http://openmicros.org/index.php/articles/94-ciseco-product-documentation/raspberry-pi/227-slice-of-pi
[Sparkfun XBee buying guide]: https://www.sparkfun.com/pages/xbee_guide
[ib technology]: http://www.ibtechnology.co.uk
[RWD-Hitag2]: http://www.ibtechnology.co.uk/products/hitag2-product.htm
[RWD dev board]: http://www.ibtechnology.co.uk/products/universal-socket-board-product.htm
[XRF module]: http://shop.ciseco.co.uk/xrf-wireless-rf-radio-uart-rs232-serial-data-module-xbee-shape-arduino-pic-etc/
[SRF stick]: http://openmicros.org/index.php/articles/249-urf-and-srf-stick-document-index
[Slice of Radio]: http://openmicros.org/index.php/articles/94-ciseco-product-documentation/raspberry-pi/282-b023-slice-of-radio
[Cooking Hacks]: http://www.cooking-hacks.com
[TI CC3000]: http://www.ti.com/product/cc3000
[Openmote]: http://www.openmote.com
[Contiki OS]: http://www.contiki-os.org
[Waspmotes]: http://www.libelium.com/products/waspmote-mote-runner-6lowpan/
[AppNearMe]: http://www.appnearme.com
[SensorTag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/index.shtml
[Grove]: http://www.seeedstudio.com/depot/Grove-t-3.html
[Thingsquare]: http://thingsquare.com
[Libelium]: http://www.libelium.com/
[Xively]: https://xively.com
[Thingworx]: http://www.thingworx.com
[The Thing System]: http://thethingsystem.com
[Node-Red]: http://nodered.org
[MQTT]: http://mqtt.org
[Tinkerkit]: http://www.tinkerkit.com
[Arduino]: http://arduino.cc
[Raspberry Pi]: http://www.raspberrypi.org
