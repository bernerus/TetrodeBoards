I have made a few changes from Ian's original design.

# G2 rectifier

The original schematic shows four 1N4007 forming a rectifier bridge. 
However, the original board layout shows that each leg of the 
rectifier is supposed to use two 1N4007 in series. 

Maybe things have changes the last 30 years, but then the usual way of
extending the voltage handling capability for a diode was to
put diodes in series and have bleeder resistances of equal values 
parallelling the diodes to make sure that they split the back voltages
in equal parts. Also each diode should have a capacitor across to protect against
voltage surges. I couldn't see any place for resistors or capacitors on the photos
I have seen on the internet, I decided instead to use another diode, the BY220 which is
good for 3 A and 1200V. These are also avalanche diodes which means that they can 
be put in series without any extra components. If you need more than one in series
for higher voltage, put one in each hole vertically and tie them together on top. 
Dont forget to change the filter caps in that case.

# 24V Relays
I happened to have five relays with the same pinout as the ones Ian used, however they were
for 24V. I  changed the circuit to allow to feed unregulated 24V to the relays instead of 12V. 
There is a jumper on the G2 board to select this.

# Connectors
I like to be able to easily take out boards for inspection, repair or testing new ideas. 
All connections have been taken to the edge of the board, or at least close to the edge.
There is space for Phoenix PCB connectors with 5.08 mm spacing. 
There are matching female screw connectors for these and they are certified up to 500V.
Unfortunately they are a bit pricey.

# SMD components
I wanted to make a professional PCB. I have previously ordered PCB's from Elecrow who offer 
PCBs for only $1 for 5 boards if the size is max 100x100 mm, so I wanted to keep the size down.
That's why I decided to use SMD components where possible. Mounting them may feel as a
challenge, but I also ordered a stencil for each board cost me another $10 but worth it.
The challenge is mostly to keep track on all components and putting them in place on the 
solder paste. A hot air gun and the solder mask together with the surface tension of liquid
does the final adjustment. 
The boards are two layer, plated through holes, tinned copper, solder mask and silkscreen print on both sides.
When ordering from Elecrow you always get 5 boards, but it is not uncommon that you get more, so I
have 10 empty boards left for anyone interested. I might lend you the stencils.

# Class C
Since '98 ham radio has evolved. Nowadays there is a lot of machine generated modes, most notably FT8.
Many of these modes employ a constant amplitude, tid means that PA's in Class C are interesting again.
As an experiment I included some circuitry to make it possible to switch the bias voltage
between 2 different values. This circuit uses an optocoupler to short-circuit one zener diode
of two that makes up the bias reference.
