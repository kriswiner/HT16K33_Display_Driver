HT16K33_Display_Driver
======================

Simple demo of driving four seven segment bubble displays with one HT16K33 display driver

Each HT16K33 cathode pin can drive two display cathodes. The HT16K33 can drive a total of 128 LED segments.
So a total of four, 4-digit, 7-segment displays can be driven with this one chip with just 2 TWI wires and power and ground. That is a lot of display without taking up a lot of the GPIO pins.
