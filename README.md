Download Link: https://assignmentchef.com/product/solved-eec172-lab3-serial-interfacing-using-i2c
<br>
<strong>Objective: </strong>In this lab, you will use I<sup>2</sup>C to communicate with an on-board Bosch BMA222 acceleration sensor. Your application program will detect the XY tilt of your board based on BMA222 readings and use the tilt to control an icon on your OLED display. You can also use a Saleae logic probe to capture and monitor SPI and I<sup>2</sup>C signal waveforms for debugging purpose.

<h1>New Equipment Needed Per Group</h1>

1    Adafruit OLED Breakout Board – 16-bit Color 1.5″ (product id: 1431) on small breadboards

1    Saleae USB Logic Analyzer

Jumper wires




<strong>Note: </strong>Do not lose the shorting blocks (jumpers) that come with the board. They are used to configure different hardware functions on the board, and may be needed for this and future labs. Unused shorting blocks should be kept on the board attached to a single header pin.




<h1>Resources (Technical Data Sheets)</h1>

Refer to the following technical documents:

<ul>

 <li>CC3200 Technical Reference Manual</li>

 <li>CC3200 LaunchPad User Guide</li>

 <li>CC3200 LaunchPad Schematic</li>

 <li>CC3200 Datasheet</li>

 <li>SSD1351 128 RGB x 128 Dot Matrix OLED/Common Driver with Controller Advance Information OLED Display Module Product Specification (Doc No. SAS1-D038-A)</li>

 <li>Bosch BMA222 Data sheet</li>

</ul>







<h1>Part I. Using I<sup>2</sup>C to communicate with the on-board BMA222 accelerometer</h1>

In this part, you will interface to the Bosch BMA222 accelerometer on the CC3200 Launchpad using I<sup>2</sup>C. You will then write an application program that uses the acceleration data to control a graphical icon on your OLED.




<ol>

 <li><strong> <u>Implement i2c_demo project on a CC3200 LaunchPad</u> </strong></li>

</ol>

As a starting point, you should study, import, build, and test the i2c_demo project on a CC3200

LaunchPad. The project is documented at

<u>http://processors.wiki.ti.com/index.php/CC32xx_I2C_Application</u> and in the CC3200 SDK

(C:tiCC3200SDK_1.2.0cc3200-sdkdocsexamples CC32xx I2C application.pdf).

In addition, you should study the Bosch BMA222 Data sheet to understand how the acceleration sensor can be used. For example, the acceleration data is described in Section 4.4.1 and includes the following basic information:




“The width of acceleration data is 8 bits given in two’s complement representation. The 8 bits for each axis are given in registers (0x03) acc_x, (0x05) acc_y and (0x07) acc_z.”

You can use the i2c demo program to see what kinds of acceleration data you get for various tilt angles using the readreg command as shown below, where the BMA222 has I<sup>2</sup>C device address 0x18. The following three commands read the acceleration data for the x, y and z axes, respectively.




cmd# readreg 0x18 0x3 1 cmd# readreg 0x18 0x5 1 cmd# readreg 0x18 0x7 1




Another way to read the data is to read multiple bytes at once, such as in the command below. This command will read the new data flag and the acceleration data for the x, y and z axes, respectively.

cmd# readreg 0x18 0x2 6




<ol start="2">

 <li><strong> Debugging <u>I</u><sup>2</sup><u>C waveforms using a Saleae logic</u> </strong></li>

</ol>

Set up your Saleae logic probe to capture I<sup>2</sup>C waveforms by enabling the I<sup>2</sup>C Analyzer. You will need to connect three wires: Ground, I2C_SCL, and I2C_SDA. To avoid damaging the electronics, you should always make the signal connections with both the CC3200 LaunchPad and the Saleae logic probe <strong><em><u>unpowered</u></em></strong>. As before, make sure that the ground symbol on the bottom of the Saleae module is aligned with the grey wire and connect the grey wire to one of the CC3200 GND pins. You can check the pinmux.c file in the i2c_demo project to find out which pins are used for I2C_SCL and I2C_SDA. Connect two of the Saleae probes, such as the Black and Brown leads, to the appropriate header pins. Double-check your ground and signal connections <strong><em>before </em></strong>you turn on the power to the CC3200 LaunchPad.




<h1>Verification</h1>

<strong> </strong>

An example screen-shot of an I2C waveform is shown below.










<ol start="3">

 <li><strong> <u>Application Program</u> </strong>In this part, you will use the accelerometer to move a small “ball” (a filled circle icon) with a radius of about 4 pixels (± 2) around on the OLED display. The accelerometer output can be used to determine the accelerometer pitch and roll orientation angles, which can be used to control the motion of the ball left, right, up and down. Rotating the accelerometer around the x-axis (roll) will move the ball left and right. The steeper the roll angle, the faster the ball should scroll across the OLED display. Similarly, rotating the accelerometer around the y-axis (pitch) will move the ball up and down on the OLED display, where the speed of the ball scrolling up and down on the display will be proportional to the pitch angle. Since the Z measurement is not used, you can disable or ignore the Z measurements. When the ball reaches the edge of the OLED display, it should not move any further in that direction. That is, it should not scroll off the screen, but should stop at any edge.</li>

</ol>




Initially, you should display the ball at the center of your OLED display. When the CC3200 Launchpad is flat, the ball should be stationary on the display. Note that you should be able to tilt the x and y axes simultaneously to move the object in any arbitrary direction on the display. For example, you should be able to move the object from the center directly to any of the four corners. The scrolling rate should be fairly slow for small tilts so that you can precisely control the position of your object.





