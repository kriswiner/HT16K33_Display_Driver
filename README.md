HT16K33_Display_Driver
======================

Simple demo of driving four seven segment bubble displays with one HT16K33 display driver

Each HT16K33 cathode pin can drive two display cathodes. The HT16K33 can drive a total of 128 LED segments.
So a total of four, 4-digit, 7-segment displays can be driven with this one chip with just 2 TWI wires and power and ground. That is a lot of display without taking up a lot of the GPIO pins.

I decided to try to reduce this idea of driving four bubble displays to practice; what follows is what I did and how it worked out.

First I breadboarded the circuit with Adafruit's [HT16K33 breakout board] (http://www.adafruit.com/products/1427) shown here:
 
![](http://www.adafruit.com/images/970x728/1427-00.jpg)

Here is what my initial circuit looked like. The HT16K33 is powered by the 3.3 V reference from and connected to the I2C of an 8 MHz Pro Mini Arduino microcontroller.

![](https://cloud.githubusercontent.com/assets/6698410/3207741/b97316ce-edfc-11e3-8077-10a0ca2ddf08.jpeg)


I was able to easily get two bubble displays running from the HT16K33 breakout on my little breadboard. I actually added a third display using jumper wires to another breadboard just to prove that I really could drive four (well, at least three!) of the bubble displays at a time with just one HT16K33.

After that success, I spent most of a Saturday soldering up a circuit on a perf board with four bubble displays and one HT16K33. This is what it looks like:

![](https://cloud.githubusercontent.com/assets/6698410/3207651/a2fefb0e-edf4-11e3-9e32-181882e85784.jpeg)

Look at all those wires! This is not a great picture but you can see that all four displays are working using the display driver sketch in this repository, which currently displays floating point (top left and bottom right) or integer (top right and bottom left) numbers of four digits or less. The sketch has simple utility but is good enough to display temperature, time, and other sensor output.

The last step was biting the bullet and learning how to use Eagle CAD to design a PCB with the same circuit. It took only a few days mostly because: 1) I was able to take advantage of all the work Adafruit and [uChip](https://github.com/uChip/BubbleDisplay) had already done and, 2) I got a lot of help from Jim Lindblom of [Sparkfun] (http://www.sparkfun.com) and Dan Sheadel of [OSHPark] (http://www.oshpark.com), where I am having the first prototypes made. Here is what the boards will look like at almost actual size! (1.48 x 1.58 inches).

![](http://uploads.oshpark.com/uploads/project/top_image/LanQ5PLH/thumb_i.png).....![](http://uploads.oshpark.com/uploads/project/bottom_image/LanQ5PLH/thumb_i.png).....![](https://cloud.githubusercontent.com/assets/6698410/3350569/8c4899da-f9be-11e3-9953-b6c926f8eaa1.jpg)

I received the boards from OSHPark and promptly put the components on. A bad picture of the board is on the right above. It was straightforward to solder even the small diode; 0805 passive components are easy to handle with a good pair of tweezers. Using a soldering iron for surface mounted components is doable but the solder joints are never going to look like machine-made parts do without a lot of practice. I noticed that the displays worked just fine mounted in their through holes before soldering; I guess there is enough contact to allow the proper current flow even without soldering. I assembled all three boards and---they all worked! I love it when this happens. This is what the boards look like in action.

![](https://cloud.githubusercontent.com/assets/6698410/3350511/a55e100a-f9b7-11e3-8383-eef494fc2576.JPG)

The board is connected to an Arduino 3.3 V 8 MHz Pro Mini running the sketch in this repository. Notice that there are only four wires, not the rat's nest of wires from the perf board prototype. So what are the advantages of this "FrontPack" design over conventional LED display choices?  Well, 1) you don't need external current-limiting resistors with the HT16K33 chip, 2) you can run the display board wih 3.3 V or 5 V as you wish, 3) it only takes four wires to control up to 8 x 4 four-digit displays since up to eight of these "FrontPacks" can be independently addressed in a given circuit by soldering a unique 3-bit address on the board pads, 4) it has a rather small footprint at 1.48 x 1.58 inches square so it saves space, and 5) it is so retro cool!

This is the first prototype; there are several variants I can think of that might be more useful for a given application. For example, why not mount the HT16K33 on the back to make a conventional "BackPack" version of this display. This would come in handy for mounting on a cased surface. The FrontPack (I'll toss the scare quotes from now on) has the additional attribue that the bubble displays, even fully inserted into the through holes, stand proud of the top surface of the HT16K33 chip, meaning that even the FrontPack can be mounted, albeit a little more awkwardly, on a case surface. But the really neat thing about the bubble displays and this through-hole mounting is that the displays can be soldered into the board at a tilt angle to aid viewing and can stand as much as a millimeter prouder still of the HT16K33 chip by a judicious choice of how far to push the displays into the board before soldering. Bottom line: even the FrontPack is likely to suit most needs.

Now there is a quirk with the current setup (there always is!). I noticed a curious unwanted behavior with this driver chip. The sketch works as intended when I have the displays numbered in (the somewhat unintuitive) order 1-2-3-4 from top right to bottom left. When I change the order to go from top left to bottom right (the more intuitive ordering), everything still works but the minus sign on displays 1 and 3 becomes intermittent. I don’t understand this behavior yet, but I suspect it has something to do with the RAM ordering of the multiplexing coupled with the particular way I am constructing the characters to display.  That is, I am hoping it is a subtle software error and not some hidden limitation of the chip. It doesn’t get in the way of using any or all of the displays, but in the interest of full disclosure, I thought I would mention this oddity. If anyone spots my error in the sketch above I would appreciate a heads up.

This is version v.01 and there are a few things I would do differently. I noticed that Adafruit (from whom I shamelessly copied the idea of using the HT16K33) used a 10 or 12 mil trace for their VDD and GND lines. This is good practice that I would follow next time but didn't here. Likewise, putting the capacitor right next to ground is OK, but it might be better to place it right next to the VDD pin on the HT16K33, instead. I used 4.7 kOhm resistors as pull-ups for the SDA and SCL lines since I am currently in the habit of using fast (400 kHz) I2C. This is in contrast to the 10 kOhm pullups used by Adafruit. I'd stick with the 4.7 kOhm in the next design iteration. Lastly, I used 39 kOhm resistors in the address lines as specified in the HT16K33 data sheet instaead of the 47 kOhm resistors used by Adafruit. They probably just had a lot of these 47 kOhm resistors lying around.

I had a lot of fun designing this board, my first real experience with Eagle CAD, and I must close by thanking Adafruit for showiing me how to use this wonderful chip by Holtek, uChip from whom I shamelessly borrowed the QDSP-6064 Eagle device package and who has devised a different solution to using these retro cool bubble displays, and Sparkfun Electronics for their cheery answers to all my inane questions, and somehow providing an inexpensive supply of these quirky, odd looking, lovable bubble displays.

Despite standing on the shoulders of these giants, I take full responsibility for any and all errors in the sketch or Eagle design. I would only ask that you tell me when you find an error so I can do my best to fix it.
