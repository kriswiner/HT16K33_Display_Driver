HT16K33_Display_Driver
======================

Simple demo of driving four seven segment bubble displays with one HT16K33 display driver

Each HT16K33 cathode pin can drive two display cathodes. The HT16K33 can drive a total of 128 LED segments.
So a total of four, 4-digit, 7-segment displays can be driven with this one chip with just 2 TWI wires and power and ground. That is a lot of display without taking up a lot of the GPIO pins.

I decided to try to reduce thisidea of driving four bubble displays to a more concrete parctice; what follows is what I did and how it worked out.

First I breadboarded the circuit with Adafruit's HT16K33 breakout board shown here:

![](http://www.adafruit.com/images/970x728/1427-00.jpg)

Here is what my initial circuit looked like. I was able to easily get two bubble displays running from the HT16K33 breakout on my little breadboard. I actually added a third display using jumper wires to another breadboard just to prove that I really could drive four (well, at least three!) of the bubble displays at a time with just one HT16K33.

After that success, I spent most of a Saturday soldering up a circuit on a perf board with foud bubble displays and one HT16K33. This is what it looks like:


![](http://uploads.oshpark.com/uploads/project/top_image/LanQ5PLH/thumb_i.png)
