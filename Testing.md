# Testing and initial power up.

These are the testing steps I went through when powering up the boards the very first time.
If any test failed, I went back, documented the issue, produced a workaround or a fix and
updated the design to make the next release better.

## Low voltage DC power up.

### Trensformer checks
#### Primary connecion
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
Now turn to the scondary winding. It should deliver at least 2x16V with a mid tap. 
Identify the mid tap by measuring the voltage between the different connections. Find one pair that gives 32-48 Volts. These are
the outer connections. The mid tap is the third one. Check that the voltage between the mid tap and the outer connections is between 
16 avd 19 V and absolutely no more than 24V. When done, disconnect tre transformer from the mains.

### G1-ALC Low voltage check
Connect the secondary winding connections to J101 of the G!-ALC board.with the mid tap
to the middle pole of J101. Turn the transformer on.

Check that the DC voltage between ground and the pole of J107 closest to the corner is 22-27V
Check that the DC voltage between ground and the pole of J107 next closest to the corner is 11.8-12.3V
Check that the DC voltage between ground and the anode of D118 is about -12V.

Let the voltage be on for a few minutes and check that nothing is getting warm.

### G2-Control low voltage check

Turn off the transformer.

Make connections between J108 on the G1-ALC board to J104. The pin order is order same on both boards. Note that if you
place the boards beside each other the pin order will mirror each other.

Unplug any jumper on JP101

Turn the transformer on again. 
Check that the DC voltage on the pin closest to the corner of J104 is 22-27V
Check that the DC voltage on the 4:th pin from the corner of J104 is 11.8-12.3V
Check that the DC voltage on pin 1 of U4 is 5V.




