Power Delivery Standard 2016\*
==============================

(C) 2016 Daniel Dunn

Introduction
------------

This document collects info on power connectors, fuses, and other power related gear, for use in the design of new devices and systems. These standards are desiged for maximum compatibility with existing equipment, however **nothing in this document should be taken to imply that any given existing device will behave in any particular way.**

Voltages
--------

* Devices that use external power and use less than 10W should should have a maximum input voltage of at least 5v.
* Devices that use external power and use  10-50W should have a maximum input voltage of at least 12v.
* Devices that use external power and use  more than that should should have a maximum input voltage of at least 32v, or be mains powered.

Devices should accept the widest possible voltage range, but should use one of 12v, 5v, 9v, 18v, 24v, or -9v(Audio gear only) if a wider range is not possible.

Low-power devices(Under 30W) should never connect directly to mains and should instead use a power adapter.

"12V" devices should accept up to at least 16v and require at most 9v to run correctly.

Power supplies should provide regulation within 4% unless labeled as to their exact output voltage range.

No semi-exposed conductor(such as can be found on the charger end of xt60 connectors) should have more than 24v.

No fully exposed connector(Such as can be found on 9v batteries and the like, and on bannana plugs in some cases) should carry more than 15v.

Connectors:
-----------

### Regulated Voltages

Devices using 5v should be powered by a microusb connector, 0.8mm barrel, or 1.3mm barrel. Use of 2.1mm barrel connectors for 5V is also acceptable but not ideal.

The 2.1mm barrel jack may be used with any regulated or unregulated voltage between 0 and 24v, but use with voltages above 12v should be avoided if there are other connectors available.

Barrel jacks must always be used in in the center positive configuration, except 2.1mm jacks in the case of legacy equipment, and 9v or 18v audio gear. Center negative outputs should have a voltage and polarity tag affixed to them.

1.3mm barrel jacks may carry up to 9v, and 0.8mm connectors may carry up to 9v.

It is acceptable for any female barrel jack to serve as an outlet, provided both a diode and resettable fuse or breaker are placed to prevent backfeeding from causing damage. 2.1mm outlets should not use non-resettable fuses, and must be clearly marked with their output voltage and the word OUT or OUTPUT, or the equivalent in the appropriate language.

### Unregulated Voltages

Devices requiring an unregulated "automotive style" 12v may use XT60, Cigarette plugs, or Anderson PowerPoles in the [ARES configuration.](http://www.qsl.net/w2vtm/powerpole.html) "Automotove style" 12v should be read as unregulated 10-15V

Supplies providing power via ciggarette adapters should not provde more than 14.4V, but devices accepting power via ciggarette plugs should expect transients that may range from -20 to  70v, or perhaps even more. 

Anderson PowerPoles should never carry more than 15v under any circumstances, except where a middle spacer PowerPole is used. In this configuration the ARES ordering should be maintained.

In this case the two outer pins may carry at most 30V. In this configuration the middle pin may be used for the center connector between two batteries for monitoring or balancing purposes, or to connect a separate supply of no more than 15v above ground or 15v below the outer pin's voltage voltage.

This scheme should not be used unless PowerPoles are already accepted and widely used in the application domain or there is specific reason to prefer them.

Devices requiring unregulated voltages above nominal 12V but under 32v should use XT60 or XT90.

XT90 Connectors may carry up to 50V, but extreme care should be used as 50v can deliver dangerous shocks in some cases.

### Misc
Pre- USB C connectors may not be used for more than 2A.

2.1mm connectors may carry no more than 5A.

1.3mm barrel jacks may not be used with center negative polarity or with voltages greater than 9v

### Special Connectors

The SAE connector may be used for the connection between solar panel and controller provided the input is protected against reverse current, and that the controller can handle sudden panel disconnection. The SAE connector should otherwise be avoided entirely. The positive terminal or the panel should be the shrouded one in this usage.

Small solar panels should use the 2.1mm connector and should be labeled with their peak output voltage(Not MPP voltage) and MPP wattage.

Banana connections should be used for all "lab" or "prototyping" power connections requiring an adjustable voltage, as nearly all [bench supplies](https://www.circuitspecialists.com/bench-top-power-supplies) use this voltage

RCA jacks are acceptable for very low power devices, under 5v and with a source impedance of 4.7k or more. The center should always be positive on these.

RJ45 connectors may be used in the standard [passive Poe](https://en.wikipedia.org/wiki/Power_over_Ethernet#Passive) configuration, but should be labeled at both ends on both male and female if used for more than 5v, unless only one voltage is used at a location. 

### Negotiation

"Active" means of voltage negotiation, such as some USB fast charging variants, should generally be avoided unless they are so pervasive there is no reasonable alternative. In this case devices should be designed to tolerate up to the maximum voltage level of the standard used, even under fault conditions such as reversed wiring.

Grounding
---------

Devices should not directly connect signal cable grounds to power ground, to avoid a dangerous loop. Instead a 10k-47k resistor bypassed with an 0.1uf or greater capacitor should be used in most cases. This does not apply to signal cables indented to connect only to one other device at a time, which is powered entirely via that cable or via isolated sources.

Where it is desired that a device have the option of being powered from either the signal cable or a power input, both a diode and a fuse should be provided on both the ground and power leads of the signal line, with the fuse rated for not more than the safe ampacity of the cable(Factoring in common counterfeiting of cables and conductors), divided by the maximum devices connected to one signal line if it is a bus topology.

Alternately, an active isolating circuit may be used on either the signal or main power input lines, or a DPDT switch that can switch both signal and ground between the two inputs.

Labeling
--------

Devices must be clearly marked with their full acceptable Input Voltage range, their input polarity, and their maximum input current. The format
should be as follows: `9-15v 2A` or `9-12v 2A(300ma avg)`.

Relevant documentation should include the notice or a variation thereof: `This device can accept any center-positive power adapter with a voltage between XV and YV, and a current of ZA or more. Center-positive power adapters usually display this symbol:<Common polarity marking>. Ensure that the + and - signs are not reversed. Use only power adapters that have been certified by UL or another agency.`

When a voltage range is not specified, a reader should assume that a device expects a maximum +-4℅ variation from the rated voltage.

Fusing
------

Where practical, resettable fuses or circuit breakers should be used. Where fuses are used, 5x20mm, ATC, and miniature automotive fuses should be the preferred types, although 5x20mm fuses should not be used with DC voltages above 24v or 32v if the maximum fault current is limited, no  matter what the rating of the fuse is, due to the difficulty in  sourcing DC rated 5x20mm fues and possibility of incorrect replacement.


Devices requiring fuses must be clearly marked as to the size and ampacity of fuse required.

Any junction of a larger wire feeding current into a smaller wire should have a fuse unless the smaller wire is less than 0.3 meters and the conductivity of the smaller wire is sufficient to blow the fuse por breaker protecting the larger wire.

Layout
------

No device or span of wire should be powered or power-grounded at more than 1 point unless the total current that all of it's connections are capable of sourcing or sinking is equal to or less than the maximum safe current of the device, or unless special equipment such as isloators are used.

Multiple parallel wires should not be used to increase ampacity, but may be used to decrease resistance or increase reliablilty, so long as the total current carried by all paralell wires is not more than any one of it's conductors could handle alone.

The exception to this is if every wire is individually fused at both the source and load and parallel wires are never joined along the span. In this case each wire may carry 85% of its full load.

Power Adapters
--------------

Devices internally using DC should not connect directly to the mains unless they require more than 32v or more than 120W.

Battery Choice
--------------

Where practical, LiFePo4 cells should be chosen over lithium ion. NiCd and pb-acid should almost always be avoided.

Handheld devices should use common cylindrical or coin sizes of rechargable battery where at all possible, otherwise pouch cells with JST-PH connectors should be used.

All Lithium Ion rechargeable batteries should contain protection circuitry against under and overcharge integral to the battery. 

Where possible, most common lithium ion cells that have a maximum voltage of 4.2V(Li-Co, NMC,etc) should only be charged to 4.10v to enhace cycle life.

Permanently attached batteries should not be used.

XT60 or PowerPole Connectors should be used on non-cylindrical batteries except very small ones, which should use JST-PH connectors, as is common practice by [SparkFun](https://www.sparkfun.com/products/13851) and [Adafruit](https://www.adafruit.com/products/258).

[JST-XH](http://www.tjinguytech.com/charging-how-tos/balance-connectors) should be used for balancing connectors, although integrated balancing and protection modules should be preferred. Anderson Powerpoles may also be for balancing in the 3-position 28v configuration mentioned in an earlier section. 

DIYers and hobbyists should generally not attempt to charge any type of lithium battery without a protection circuit, and should strongly consider avoiding scratch built charging circuits completely for large lithium ion cells.

Switching
---------

Physical on/off switches and digital switches that will automatically turn on when power is restored after being cut should normally be preferred.

Hot plugging
------------

Devices should not be damaged by a full voltage hot plug to a stiff supply through even several hundred feet of cable inductance, even when plugged and unplugged rapidly. See [the article by Pololu Robotics.](https://www.pololu.com/docs/0J16/all)

Noise
-----

Devices should not backfeed noise into power lines. Noise levels must be low enough that harmful or illegal emissions will not result even from 250ft of untwisted zip cord.
