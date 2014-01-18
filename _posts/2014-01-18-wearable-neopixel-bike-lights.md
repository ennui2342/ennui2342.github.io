---
layout: post
categories: blog
comments: true
author: Mark Cheverton
title: Wearable NeoPixel Bike Lights
description: A project to make wearable bike lights by embedding Adafruit NeoPixels into a messenger bag
---

<iframe width="560" height="315" src="//www.youtube.com/embed/wQitfnP5M9Q" frameborder="0"></iframe>

I've wanted to play with [Adafruit's NeoPixels][Neopixels] for a while
now. They're great little devices, available in a number of form factors
for sewing into wearables, mounting on breadboards, or epoxying as strips. Each NeoPixel contains red,
green and blue LEDs giving 24-bit colour, and a built-in driver chip which
provides a one-wire interface for a microcontroller. Unlike
the common analog 12v LED strips, NeoPixels are driven at 5v, giving
you more options for powering them in wearables projects.

For my project I decided I wanted to replace my bike lights - I'm always
forgetting them, or leaving them on the bike and draining the batteries. I
figured I could use NeoPixels to build lights into my messenger
bag which I always have with me when I'm cycling.

I decided to go with the [30 pixels per meter weatherproof](http://www.adafruit.com/products/1376) strip as high resolution
wasn't necessary for the ['Knight
Rider'](http://www.youtube.com/watch?v=WxE2xWZNfOc) effect I wanted to
achieve. In retrospect I should have gone for the black backing
to make it blend in with the bag's strap. It also remains to be seen how
robust the strips are in the long run, and whether [sewable
pixels](http://www.adafruit.com/products/1260) would have been a better choice, but after a month of
careful wear everything is still in good shape.

I initially sewed the straps on with thread, but there was too much
movement in the strap when worn and the thread cut in. Elastic was a
better choice and I swapped the thread out in a couple of key places.
The ends of the NeoPixel strip are sealed with
hot glue and a capacitor added to smooth out the power-on, also sealed in
some heatshrink so the whole thing should stand up to cycling through
showers. A 4AA battery pack of rechargeables is concealed in the bag with a superglued
guard to stop the power switch being knocked.

The controller is the [Adafruit
Gemma](http://learn.adafruit.com/introducing-gemma) - a beautiful little
Arduino board made for wearables projects. As suggested I used [tiny
snaps](http://learn.adafruit.com/flora-snaps/overview) to handle the connections to the board, and secured it
tightly with sticky-back velcro. Programming the Gemma is no
different from any other Arduino board - you just have fewer pins and
less memory. Adafruit distribute a helpful [Arduino
library](https://github.com/adafruit/Adafruit_NeoPixel)
for NeoPixels which makes interfacing really easy. Included below is my code to achieve the dual
red and white effect. If you want to use it in your own projects
I've made it [available as a
Gist](https://gist.github.com/ennui2342/8497773)

```c++
#include <Adafruit_NeoPixel.h>

#define PIN 1
#define NUM_PIXELS 20
#define NUM_NODES 2

Adafruit_NeoPixel strip = Adafruit_NeoPixel(NUM_PIXELS, PIN, NEO_GRB +
NEO_KHZ800);

uint32_t state[NUM_PIXELS];

// Pixel positions start at 1
// start pixel, end pixel, direction of travel 1|2, initial pixel
position, color
uint32_t nodes[NUM_NODES][6] = {
  { 1, 10, 1, 5, 0xFF1000 },
  { 11, 20, 2, 20, 0xFFFFFF }
};
  
void setup() {
  strip.begin();
  strip.setBrightness(32);
  strip.show();
}

void loop() {
  fadeStrip(2);
  updateNodes();
  strip.show();
  delay(70);
}

void updateNodes() {
  for(int i = 0; i<NUM_NODES; i++) {
    switch(nodes[i][2]) {
      case 1:
        nodes[i][3]++;
        if(nodes[i][3] == nodes[i][1]) {
          nodes[i][2] = 2;
        }
        break;
      case 2:
        nodes[i][3]--;
        if(nodes[i][3] == nodes[i][0]) {
          nodes[i][2] = 1;
        }
        break;
    }
    strip.setPixelColor(nodes[i][3]-1, nodes[i][4]);
    state[nodes[i][3]-1] = nodes[i][4];
  }
}

void fadeStrip(uint8_t rate) {
  for(int i = 0; i<NUM_PIXELS; i++) {
    state[i] = dimColor(state[i], rate);
    strip.setPixelColor(i, state[i]);
  }
}

// Borrowed the below from NeoPixel-KnightRider
uint32_t dimColor(uint32_t color, uint8_t width) {
   return (((color&0xFF0000)/width)&0xFF0000) +
(((color&0x00FF00)/width)&0x00FF00) +
(((color&0x0000FF)/width)&0x0000FF);
}
```
[NeoPixels]: http://learn.adafruit.com/adafruit-neopixel-uberguide/overview
