HT16K33_Display_Driver
======================

Simple demo of driving four seven segment bubble displays with one HT16K33 display driver

Each HT16K33 cathode pin can drive two display cathodes. The HT16K33 can drive a total of 128 LED segments.
So a total of four, 4-digit, 7-segment displays can be driven with this one chip with just 2 TWI wires and power and ground. That is a lot of display without taking up a lot of the GPIO pins.

I decided to try to reduce this idea of driving four bubble displays to practice; what follows is what I did and how it worked out.

First I breadboarded the circuit with Adafruit's [HT16K33 breakout board] (http://www.adafruit.com/products/1427) shown here:

![](http://www.adafruit.com/images/970x728/1427-00.jpg)

Here is what my initial circuit looked like. I was able to easily get two bubble displays running from the HT16K33 breakout on my little breadboard. I actually added a third display using jumper wires to another breadboard just to prove that I really could drive four (well, at least three!) of the bubble displays at a time with just one HT16K33.

After that success, I spent most of a Saturday soldering up a circuit on a perf board with four bubble displays and one HT16K33. This is what it looks like:

![](https://cloud.githubusercontent.com/assets/6698410/3207651/a2fefb0e-edf4-11e3-9e32-181882e85784.jpeg)

Look at all those wires! This is not a great picture but you can see that all four displays are working using the display driver sketch in this repository, which currently displays floating point (top left and bottom right) or integer (top right and bottom left) numbers of four digits or less. The sketch has simple utility but is good enough to display temperature, time, and other sensor output.

The last step was biting the bullet and learning how to use Eagle to design a PCB with the same circuit. It took only a few days mostly because: 1) I was able to take advantage of all the work Adafruit and [uChip](https://github.com/uChip/BubbleDisplay) had already done and, 2) I got a lot of help from Jim Lindblom of [Sparkfun] (http://www.sparkfun.com) and Dan Sheadel of [OSHPark] (http://www.oshpark.com), where I am having the first prototypes made. Here is what the boards will look like at almost actual size.

![](http://uploads.oshpark.com/uploads/project/top_image/LanQ5PLH/thumb_i.png)         ![](http://uploads.oshpark.com/uploads/project/bottom_image/LanQ5PLH/thumb_i.png)

Now I am waiting for delivery. When I get the boards assembled and working, I will post the results.
