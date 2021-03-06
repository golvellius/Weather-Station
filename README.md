Weather-Station / Estación Meteorológica
========================================
This is a Fork of the supperb Weather code of docwelch ...
I have added new code to use different sensors like UV sensor ( ML8511 ) from here = https://learn.sparkfun.com/tutorials/ml8511-uv-sensor-hookup-guide .As i have a lot of problems with the sensors attached in the Weather Shield ( sometimes no good pressure measures ), i am using other sensor, the  BME280 GYBMEO ( Temp + Humidity + Pressure ) . With these i can use 1 meter cable to install the sensors ( uv + temp + humidity + pressure) in the weather meter and protect the arduino + xbee from corrosion in a watertight box .

Also with this code your able to send data to Weatherunderground (as in the original code ) plus you can send the solarradiation paramter.

As you can read from the original TEXT from docwelch :

This is a weather station created with components from Sparkfun. The Arduino firmware is a modified version of Sparkfun's Wimp Weather Station. While the Imp is an interesting device, I wanted to get the weather data back to a BeagleBone Black for further processing/evaluation. The BeagleBone Black can easily push the data to Weather Underground. 


##Equipment

To set up your station, please follow the [Sparkfun tutorial](https://learn.sparkfun.com/tutorials/weather-station-wirelessly-connected-to-wunderground). Obviously, you won't need the Imp or the Imp shield. In its place, you will need an XBee shield, an XBee breakout (with headers) and and two XBees. I am using XBee Pro modules due to the distance and other factors. You will need *three* sets of Arduino headers (one for the XBee shield and two for the weather shield) because the weather shield is so tall. So that we can turn the XBee off and on to conserve power, you will need a connection between the XBee pin 9 and digital pin 4 on the RedBoard.

I am using a BeagleBone Black Rev. C (a Rev. B board would work as well if you have one) running [Debian](http://beagleboard.org/latest-images/). You will need to have your BeagleBone Black connected to the internet (wired or wireless) if you want to push your data to Weather Underground. On the P9 header of the BeagleBone Black, connect pin 1 to ground on the XBee breakout, pin 3 to VCC on the XBee breakout, pin 21 (Serial 2 TX) to DIN on the XBee breakout, and pin 26 (Serial 1 RX) to DOUT on the XBee breakout.


##Libraries

You will need the [xbee-arduino library](https://code.google.com/p/xbee-arduino/) as well as the [pressure](https://github.com/sparkfun/MPL3115A2_Breakout) and [humidity](https://github.com/sparkfun/HTU21D_Breakout) sensor libraries from Sparkfun. 
If your are not going yo use the weather shield sensors and you wanted to use other type of sensors :

Barometric sensor (bmp280) from adafruit (https://github.com/adafruit/Adafruit_BMP280_Library) . 
If you are using sensor (BME280 GYBMEP) , you have to edit the library to change the address from 0x77 to 0x76 see : (https://github.com/adafruit/Adafruit_BME280_Library/issues/15) .

UV sensor ( ML8511 ) you do not need library .

For the BeagleBone Black, you will need (in addition to libraries bonescript, socketio, and serial installed by default) [xbee-api](https://www.npmjs.org/package/xbee-api) and [moment](https://www.npmjs.org/package/moment). Unless you are using the latest Bonescript from Github, you need to modify your serial.js file (found in /usr/local/lib/node_modules/bonescript) to include the following line at the end of the file: `exports.serialParsers = m.module.exists ? m.module.parsers : {};`
