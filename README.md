#Flashing Christmas Tree Decoration

This project is based on the wonderful resources provided by Adafruit, more specifically their great [uberguide for Neopixels](https://learn.adafruit.com/downloads/pdf/adafruit-neopixel-uberguide.pdf)
Follow their guide to install the necesary libraries for Arduino.

###For this project you will need.

* An Arduino Uno, Pro Mini, Leonardo or other Arduino compatible device.
* A neopixel ring with 12 RGB LED (You can go larger, and I will show where to change this value in the code)
* Wire to solder the neopixel ring.
* 220 ohm resistor (RED, RED, BROWN)
* Breadboard, optional.

###To build
Solder three wires to your neopixel.

1. VCC (5V Power, also labelled as PWR)
2. GND (Ground)
3. DIN (Data In, also can be labelled as IN)

With the wires soldered, connect 

1. Attach GND to the Arduino GND
2. Attach DIN to Arduino pin 6

For the power, run a 220 ohm resistor inline from the Arduino power to the neopixel power wire. A breadboard makes this very easy to do.

Refer to this diagram to see how I wired the project using my Arduino Pro Mini.
![layout of project diagram](./xmas_lights.png)

You can also optionally use an inline 220 ohm resistor between the DIN and pin 6 to protect the neopixel from power spikes.

###Software
Install the Arduino neopixel library provided by Adafruit.

With the library installed we start work on the code.

To use the library inside of our code we need to include it

```Arduino
#include <Adafruit_NeoPixel.h>
```

For this project we will be using pin 6 to connect our neopixel DIN(IN) to the Arduino.

```Arduino
define PIN 6
```

Next we need to instruct our Arduino that we are using a neopixel, and in this example we are using one with 12 RGB LED. If you are using a larger sized neopixel ring, change this number to reflect it.

```Arduino
Adafruit_NeoPixel strip = Adafruit_NeoPixel(12, PIN, NEO_GRB + NEO_KHZ800);
```
Now we setup the the neopixel ring by initialising it via _strip.begin()_ and then we use _strip.show()_ to set all of the LED to off.

```Arduino
void setup() {
  strip.begin();
  strip.show(); // Initialize all pixels to 'off'
}
```
With the setup complete, we move on to the main loop that forms our light show.
The loops consists of three for loops

The first loop sets the colour of the LED to red using an R G B value (255,0,0), we then use _strip.show()_ to push this to the neopixels and then delay for 1/10 of a second.

```Arduino
void loop() {
  for (int led = 0; led < 12; led++) {
      strip.setPixelColor(led,255,0,0);
      strip.show();
      delay(10);
   }
```

Our second loop is exactly the same as the first for loop, but this time it changes the R G B value to green (0,255,0).

```Arduino
  for (int led = 0; led < 12; led++) {
      strip.setPixelColor(led,0,255,0);
      strip.show();
      delay(10);
  }
```

Our final for loop changes the R G B value to blue (0,0,255).

```Arduino
  for (int led = 0; led < 12; led++) {
      strip.setPixelColor(led,0,0,255);
      strip.show();
      delay(10);
  }    
}
```

Upload this code to yor Arduino, and you should see something like this.

[![Click the image to watch the video](https://farm8.staticflickr.com/7527/15369486073_bfddbc0eaf_z_d.jpg)](https://www.youtube.com/watch?v=JX9NkHFaKj8)




