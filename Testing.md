# Testing and initial power up.

These are the testing steps I went through when powering up the boards the very first time.
If any test failed, I went back, documented the issue, produced a workaround or a fix and
updated the design to make the next release better.

## Low voltage DC power up.

### Transformer checks

In the following, I used two transformers, one for the low voltages and one for the higher voltages.
Hence, I'm talking about different transformers. If you have only one, after the identification and testing, be sure to keep the
high voltage windings isolated until they are actually being used.

#### Primary connection

Measure the primary winding. There may be many connections.
Find the pair of connections that have the largest resistance.
Connect these, in a safe way, to the mains voltage. You should hear a very soft hum
from the transformer. If it makes more noise that a soft hum, you might have connected
to the wrong winding or a pair of connections to the primary winding that was not designed
for your mains voltage.

Now let the transformer run on mains voltage without connecting anything to the secondary winding(s).
Observe it for 10 minutes, then disconnect it from mains, and feel it with your hands. It should not feel warm anywhere.
If it gets noisy, oe warm, or if you see smoke or you feel any smell from it, disconnect immediately. The primary test has failed.

#### Secondary winding check.

Now turn to the secondary winding. It should deliver at least 2x16V with a mid tap.
Identify the mid tap by measuring the voltage between the different connections. Find one pair that gives 32-48 Volts. These are
the outer connections. The mid tap is the third one. Check that the voltage between the mid tap and the outer connections is between
16 avd 19 V and absolutely no more than 24V. When done, disconnect tre transformer from the mains.

### G1-ALC Low voltage check

Connect the secondary winding connections to J101 of the G!-ALC board.with the mid tap
to the middle pole of J101. Turn the transformer on.

Check that the DC voltage between ground and pin 6 of J108 (closest to the corner) is 22-27V
Check that the DC voltage between ground and pin 3 of J108 and pin 2 of J109 is 11.8-12.3V
Check that the DC voltage between ground and pin 4 of J109 is about -12V.

Let the voltage be on for a few minutes and check that nothing is getting warm.

### G2-Control low voltage check

Turn off the transformer.

Make connections between J108 on the G1-ALC board to J104.
The pin order is order same on both boards, but mirrored,  so you could use a flat band of wires.

Verify the connection between J108 on the G1-ALC board to J104 by measuring the resistance from, JP101, pin closest to the corner on the G2 board,
to J108 pin 6, (closest to the corner) i.e. the middle of the board edge. It should be 0-0.2 ohms.

Unplug any jumper on JP101

Turn the transformer on again.

Check that the DC voltage on the pin closest to the corner of J104 is 22-27V

Check that the DC voltage on the 4:th pin from the corner of J104 is 11.8-12.3V

Check that the DC voltage on pin 1 of U4 is 5V.

Turn the transformer off

Re-plug any unplugged jumper on JP101

### G2-Control G2 rectifier low voltage check

Connect the low voltage transformer secondary to J102 on the G1-ALC board instead of J101.
Turn the transformer on

Check the DC voltage between CATHODE and G2-unreg pins of J108.
(These are the two pins of J108 closest to J104) You should see about 44-52 Volts, depending on the transformer.
Note that this is just a check using low voltages, in the final setup the voltage should be considerablu higher.

Turn the transformer off

## G1 voltage power up

### Transformer check

Apply mains power to the primary winding. Measure the voltages on the secondary windings,
Find out which winding gives about 100 VAC, and which gives more than 300VAC.
Disconnect the transformer from mains.

### Configure relay voltage
Insert a jumper at JP101 for either 24V or 12V relay voltage, depending on the relays.

#### Wire up a PTT button.

Connect an SPST button between J1 pin2 (PTT_L) and J3 pin 7 (GND) on the G2-control board

### Check voltages of the G1 section

Connect the low voltage transformer secondary to J101 on the G1-ALC board. J102 should be unconneced.
Connect the secondary 100 VAC winding to J104. Leave the 300VAC winding unconnected and isolated.
Smoke test. If something smells warm or smoke erupts, turn off both transformers immediately

#### Configure for G1 switching

If R107 is a resistor and not a link:
* Connect a link between J102 pin 5 and J103 pin 5 on the G2-control board.
* Connect a wire between J103 pin 4 and J3 pin 2 on the G2-control board. (CATHODE)
* Connect a wire between J102 pin 4 on the G2-control and J103 pin 1 (G1 Switch) on the G1-ALC board.

Apply mains power to the low voltage transformer. Wait until the LED goes dim. It can take severeal minutes.

Now check the connections made using an ohmmeter.  There should be no connection between 102 pin 1 (G1 Switch) on the G1-ALC board
and J3 pin 4 on the G2-control board. 

When pushing the PTT switch, the relays should click and the ohmmeter should read nearly 0 ohms. 

Release the button and the connection should disappear.

Disconnect mains power from the low voltage transformer

#### Wire up and Class select

Get an SPST switch. Set the switch to open.

Connect a SPST switch between  J107 pin 1 and 4 on the G1-ALC board. (CLASS AB1_L).

#### Test G1 output voltages

Apply power to the low voltage transformer.

Connect both transformers to mains voltage.
Beware, there is now lethal voltages available at the cards.
Check that the DC voltage on the 4:th pin from the corner of J104 to ground is 11.8-12.3V
Check the G1 out voltage against the CATHODE rail (J108 pin 2), should be less than -100V.
Press the PTT button. The voltage should rise to about -93 to -92 Volts depending on the position of RV102.
Release the button.

Flip the SPST switch to the ON (Class AB1) position.
The voltage should be between -84 to -81V depending on the position of RV102
With the PTT button pressed, the voltage should rise to about between -50 to -56V V
Check that there is about 12V on J107 pin 1 against ground.

Disconnect mains power from the transformers

## G2 voltage check and adjustment

##### Check the 30V Rail

Now, with the transformers off, connect the 100 VAC winding ( NO, not the 330V yet) to J102 on the G1-ALC board.
Connect the voltmeter between pin 4 and 7 of yet empty socket of U2. Positive on pin 7.
Turn on the transformers. The voltmeter should show +30V approximately. If not, fix before continuing. The 748 is precious
and hard to come by. It is no longer manufactured.
Turn the transformers off again.


##### Install the 748

Now it's time to put in the 748 in its socket. IMPORTANT! Do not continue without it or you will burn R13 due to VDR1 clamping the overvoltage produced without the 748 regulating it down below 400V. Observe the polarity of the 748.

##### Install R14
R14 is off-board. Connect it to J3 between pins 1 and 4 on the G2 board.

##### Connect the 330 volt winding

**WARNING EVEN MORE LETHAL VOLTAGES WILL BE PRESENT DURING THESE TESTS**

Disconnect the 100V Winding from J102 and put it back into J101.
Connect the 330V winding to J102 instead.

##### Test and measure the unregulated G2 voltage

Connect the voltmeter negative end to the CATHODE rail (J108-2 on G1 board)
Connect the voltmeter positive end to the G2-UNREG output (J108-1 on the G1 board)
Turn the transformer on briefly, the voltmeter should show between 350 to 400V.
If voltages seems OK, turn on for 10 seconds and then off.
Look and smell for smoke and heat building up. DO NOT TOUCH ANYTHING until the voltmeter goes below 30V.

Turn the transformers off.

##### Test the warm up timing

Wait for about 10 minutes before proceeding to allow the warmup timing capacitor to leed out all its charge. Get a stopwatch ready while waiting.
Turn the transformers again and start the stopwatch. The LED should be fully lit.
After about 2 or 3 minutes the LED should go almost off. Then stop the watch.
Check the required warmup time needed for your tube(s). You may want to adjust the value of R20 to get the desired time.
Remember that each time you thurn the transformer on, you will have to wait this time before trying to enable the G2 voltage.

##### Measure and adjust the G2 regulated voltage output

Now move the positive probe to the G2 Reg output (J3 pin 3)
Adjust RV102 to its middle position.
Turn the transformers on again.
Voltmeter should show 0 V because the relay connects to the CATHODE rail.
Push the PTT Button, the relays should click and the voltmeter should show over 300V.
Adjust RV101 while pushing the PTT switch until the voltmeter shows 350V (For 4CX250B)
Release the PTT switch and turn the transformers off.

##### Check waveform of G2
Connect an oscilloscope in parallel to the voltmeter. Use a 10x probe. Check that the waveform when pushing the PTT button
is absolutely flat. If not, the transformer may need more turns of wire for the G2 winding.

##### Adjust the G2 trip current.
Turn RV2 fully clockwise.
Compute what resistance is needed to load the trip current needed. I needed to load 40 mA and at 350V I needed a resistance of 8750 ohms at 14W.
Connect the load resistance between the G2 output pin and the cathode pin.
Connect the voltmeter to measure the current through the load resistance and fine adjust the resistance,
while pressing the PTT button until the current is at the computed trip current (40 mA in my case)
When you have the precise load resistance needed, 
push the PTT button and very slowly turn RV2 counterclockwise until the LED lights up and the relays drop.
Press the reset button and the LED should go dark again.
disconnect the meter and leave the load current path open, Push the PTT button again and the LED should stay dark.





