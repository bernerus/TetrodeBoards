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

Connect the secondary winding connections to J101 of the G1-ALC board with the mid tap
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

Re-plug the unplugged jumper on JP101

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

#### Configure for G1 switching

If R107 is a resistor and not a link:
* Connect a link between J102 pin 5 and J103 pin 5 on the G2-control board.
* Connect a wire between J103 pin 4 and J3 pin 2 on the G2-control board. (CATHODE)
* Connect a wire between J102 pin 4 on the G2-control and J103 pin 1 (G1 Switch) on the G1-ALC board.

Apply mains power to the low voltage transformer. Wait until the LED goes dim. It can take severeal minutes.

Now check the connections made using an ohmmeter.  There should be no connection between 102 pin 1 (G1 Switch) on the G1-ALC board
and J3 pin 2 on the G2-control board. 

When pushing the PTT switch, the relays should click and the ohmmeter should read nearly 0 ohms. 

Release the button and the connection should disappear.

Disconnect mains power from the low voltage transformer

#### Wire up and Class select

Get an SPST switch. Set the switch to open.

Connect a SPST switch between  J107 pin 1 and 5 on the G1-ALC board. (CLASS AB1_L).
Check that there is about 12V on J107 pin 1 against ground when the switch is off and 0V when on.

#### Test G1 output voltages

Apply power to the low voltage transformer.

Check that the DC voltage on J104 pin 4 on the G2-control board is 11.8-12.3V against ground.

Connect the secondary 100 VAC winding of the G1/G2 transformer to J104. Leave the 300VAC winding unconnected and isolated.

Connect both transformers to mains voltage.

Beware, there is now lethal voltages available on both boards.

Smoke test. If something smells warm or smoke erupts, turn off both transformers immediately

Check the G1 out voltage (j103 pin 4) against the CATHODE rail (J108 pin 2). It should be lower than -100V, typically -102 V or more.
Press the PTT button. The voltage should rise to about -93 to -92 Volts depending on the position of RV102.
Release the button.

Flip the SPST switch to the ON (Class AB1) position.
The voltage should be between -82 to -79V depending on the position of RV102
With the PTT button pressed, the voltage should rise to about between -52 to -59V

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

##### Install R14
Install R14 between J3-1 and J3-4 on the G2 board. It is off-board.

##### Install LK3
Install LK3 if not done so previously.

##### Connect the 330 volt winding

**WARNING EVEN MORE LETHAL VOLTAGES WILL BE PRESENT DURING THESE TESTS**

Disconnect the 100V Winding from J102 and put it back into J101.
Connect the 330V winding to J102 instead.

##### Test and measure the unregulated G2 voltage

Connect the voltmeter negative end to the CATHODE rail (J108-2 on G1 board)
Connect the voltmeter positive end to the G2-UNREG output (J108-1 on the G1 board)
Turn the transformer on briefly, the voltmeter should show between 350 to 410V.
If voltages seems OK, turn on for 10 seconds and then off.
Look and smell for smoke and heat building up. DO NOT TOUCH ANYTHING until the voltmeter goes below 30V.

Turn the transformers off.

##### Test the warm up timing

Wait for about 10 minutes before proceeding to allow the warmup timing capacitor to bleed out all its charge. 
Prepare a stopwatch ready while waiting.
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
Compute what resistance is needed to load the trip current needed. I needed to load 40 mA and at 350V so I needed a resistance of 8750 ohms at 14W.
Connect the load resistance between the G2 output pin and the cathode pin.
Connect the ammeter in series with the resistance to monitor the current and fine adjust the resistance to the correct trip current
while pressing the PTT button. (40 mA in my case)
When you have the precise load resistance needed, 
push the PTT button and very slowly turn RV2 counterclockwise until the LED lights up and the relays drop.
Press the reset button and the LED should go dark again.

Disconnect the meter and leave the load current path open, Push the PTT button again and the LED should stay dark.

Turn the transformers off.

### Check ALC output and adjust the G1 trip current.

#### Install U103

The optocoupler U103 must be of the type MCT5211 which is sensitive enough to be able to transfer
the low G1 currents to the other side. Observe the polarity and insert it into its socket.

#### Setup

* Disconnect the 100V Winding (J104 on the G1 board)
* Disconnect the 300V Winding as well. (J102 on the G1 board)
* Connect the G1 out (J103 pin 4) to GND (J107 pin 5) temporarily.
* Remove the wire to the RV102 slider (J105 pin 2), but leave the other pins be connected.
* If present, disconnect any wire to INH IN (J107 pin 3)

#### Measure ALC and G1 Trip at zero G1 current
Turn on the low voltage transformer.

Turn RV103 fully counterclockwise

Measure, ALC OUT (J107 pin 4) should be at 0V measured against GND (J107 pin 5)

Measure, G1 TRIP (J108 pin 5) should be at 0V measured against GND (J108 pin 6)

Turn the transformer off.

#### Generate 0.5 mA artificial G1 current

Connect an ammeter between G1 meter+ (J103 pin 2) G1 meter - (J103 pin 3)
Connect a 22 kOhm, 0.5W resistor between the RV102 slider (J105 pin 2) and +12V (J109 pin 2)

#### Check ALC output changing
Turn the transformer on. The ammeter should read 0,5 mA

Turn both RV101 and RV103 fully counterclockwise. 
While observing the ALC out pin (J107 pin 4) turn RV101 clockwise and at some point, the 
voltage of ALC should change quite quickly between 0V and -12V

If that does not happen, then if and ALC OUT stays at -12V, short-circuit R122. On the other hand if
ALC OUT stays close to 0V, replace R122 with a 1kΩ resisttor instead.

Turn the transformer off.

#### Check G1 trip functionality
##### Change the artifical current to 3 mA

Replace the 22kΩ reistor to 3.3 kΩ.

#### Tune the G1 trip level
Turn RV101 fully clockwise

Turn the transformer on again. The ammeter should read ca 3 mA.
Wait for the LED to become dim.

Turn RV101 CCW, slowly until the LED lights fully.

Turn RV101 a little clockwise and press the reset button, the LED should go dim.

Turn RV101 CCW very slowly again and find the exact trip point, repeat if unsure.

Turn the transformer off.

### Wrap up

Remove the 3.3 k resistor.

Reconnect the wire from RV102 slider to J105 pin 2

Remove the wire between G1 out (J103 pin 4) and GND (J107 pin 5)

Reconnect the wire to INH IN (J107 pin 3) if there was one before











