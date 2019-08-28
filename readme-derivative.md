Derivative Work by Goat Curry

# EAGLE Project
I added an EAGLE project to the `eurorack` repo. The purpose is to save the
state of the working environment for the last PCB I was working with in the
`eurorack` repo. It lowers the friction in switching between `eurorack` work and
my day-job work.

For example, if I am looking at the `shades` schematic and board files, I close
the project, not the files. Then when I reopen the project, those files open up.
Similarly, whatever libraries are active are reactivated, the grid settings in
the board file are loaded, etc.

# Price Module Builds
I use PCB:NG in Brooklyn. They are professional, have a quick turn time, and are
the cheapest prototyping service I know of. The only drawback is that they only
assemble surface mount parts. A lot of Eurorack parts are through-hole.

As ridiculous as it feels to pay $300-$500 for a module, there is no
cost-savings to order a single board. PCB:NG requires ordering six boards.
MacroFab allows ordering a single board, but the cost is very high. Set the
through-hole parts as DNP and the cost of a module like Shades or Ears is the
same as buying the module new. In addition:

- most modules have a metal panel,
    - I still need to laser cut a proxy for the front panel
    - in the case of Ears, the front panel is another PCB
    - this is cheap to order from OSHPark, but still, that's another PCB to
      order!
- I still need to solder the through-hole parts by hand
- I have to deal with procuring the 3.5mm jack that matches the PCB footprint

## Jacks
This took me by surprise. There are *many* 3.5mm mono jacks that solders to a
PCB. The PCB footprint must match whatever jack I procure. Even more surprising,
very few of these are available in the US. In fact, none of the ones used in
Eurorack designs are available from the usual US vendors (Mouser, Digi-Key,
Newark, etc.). Instead, it seems all of the threaded 3.5mm jacks are
right-angle. Many of these are confusingly labeled *vertical*, but they are also
right-angle (the *vertical* is not in the dimension required by the Eurorack
build).

Also, the jacks take a lot of abuse, so they must be attached to the front
panel via a threaded nut. If an SMT threaded vertical jack exists, I'll try it,
but it sounds exotic. I'd like to try doing an entirely surface mount design. I
cannot find anything like this, not even from QingPu.

Stereo jacks are OK too. On a stereo jack, in addition to the sleeve and tip
there is a ring pin. Leave the ring pin not connected.

The ring pin shorts to the sleeve pin when a mono plug is inserted into a stereo
jack. The ring pin floats when unplugged.

Here is the Mouser page with the most likely candidates:

<https://www.mouser.com/Connectors/Audio-Video-Connectors/Phone-Connectors/_/N-778cv?P=1z0yy6bZ1yzsf9eZ1yzrk55Z1yzrwr8Z1yzowym>

- Amphenol# ACJM-MV35-2S is the ideal jack:
    - 3.5mm
    - threaded: the `MV` is for threaded metal?
    - mono (has sleeve and tip pins, the first `M` is for mono)
    - switched (has a switch pin, the final `S` is for switched)
    - purchase 100 from Master Electronics for $70.20 plus $9 shipping
        - they have a minimum order service fee for orders under $50, so
          ordering quantity 10 is not much cheaper than quantity 100
    - [x] purchase 100 on 2019-08-27, order confirmation# M39230
        - ships tomorrow via UPS ground
        - sub-total: $70.20
        - shipping: $8.99
        - tax: $6.1776
        - total: $85.3676
- Amphenol# ACJS-MV35-3S is the stereo version of the switched mono jack
    - this is fine
    - just leave the ring pin unconnected
- Amphenol# ACJM-MV35-2 is OK if I don't need the switch pin
- Amphenol# ACJS-MV35-3 is the stereo version of the no-switch jack
    - also OK if I don't need the switch pin
    - just leave the ring pin unconnected
    - another stereo no-switch jack is Kobiconn# 161-MJ355W-EX
    - the incentive of this part is that it is unlikely to go out of stock
    - but the Amphenol inventory is not bad, between Mouser and Master
      Electronics
- Since I'm ordering from Master Electronics, I decided to get 50 of the mono
  jack and 20 of the stereo jack. It's enough jacks for now. By the time I need
  more, they should be back in stock at Mouser. And the switched stereo version
  is not even stocked at Mouser. Ah no, the stereo are on back-order. So just
  the mono then.
- The mono and stereo, switched and not-switched, are all interchangeable as
  long as I always use the pin out for the case with the most pins: the stereo
  switched. This lets me use any jack on any board. That kind of
  interchangeability would be confusing if I was making products to sell, but
  it's great for making one-offs for myself and not being *stuck* when the
  vendors run out of stock on the parts with less pins. I could always cut the
  pins off, but it's cleaner to just add the extra holes on the board. The only
  case against this is if it eats up valuable PCB real estate.

## QingPu WQP-WQP518MA, Thonkiconn PJ301M12, now Thonkiconn PJ398SM
Mutable Instruments uses Thonkiconn# PJ301M12, which is actually QingPu#
WQP-WQP518MA. The part is now Thonkiconn# PJ398SM.

It has three pins that are axial with the jack so that the jack is oriented
vertical to the PCB. The pins are intended for through-hole soldering. The pins
do not have loops for chassis wiring.

All 3.5mm jacks work with the same plugs. But the PCB layout is specific to each
jack. See <http://www.qingpu-electronics.com/en/products/WQP-PJ398SM-362.html>.

The layout for this particular part has two pins close together. The two
close together are the sleeve and switch. The sleeve pin is the one that
sticks out the side of the jack. QingPu bends this pin down so that it runs down
to the PCB like the other two pins. The pin farthest away is the tip.

### Procurement
Procuring the jacks sucks. Options are attempting to buy direct from China, or
procuring from a vendor in Europe.

- send an inquiry to QingPu:
<http://www.qingpu-electronics.com/inquiry-en.asp?id=362&p=WQP-WQP518MA&u=http://www.qingpu-electronics.comproducts/WQP-PJ398SM-362.html>

- buy from the Thonkiconn in the UK:
<https://www.thonk.co.uk/shop/thonkiconn/>

### function of the three pins
The three pins are tip, sleeve, and a normally-close (N/C) switch.

The two important pins are sleeve and tip. These carry the signal on the audio
cable. Sleeve ties to a 0V reference in the circuit. Tip is the signal input or
output.

The switch pin functionality depends on the module.
Normally-closed means the switch pin shorts to the tip when no cable is inserted
and opens when a cable is inserted.

### switch pin usage examples

#### Elements
- all the jacks on Elements do not use the switch connection
- the switch pin is left unconnected

#### Ears
- the sleeve pin connects to a `0V` reference
- the piezeo element is a two-terminal device
    - one terminal ties to the `0V` reference
- the switch pin connects to the other terminal of the piezo element
- when nothing is plugged into the jack, the switch pin shorts to the tip pin,
  so the piezo element connects to the input stage
- when a device is plugged in, the switch pin opens and the piezo element is no
  longer connected to the input stage

#### Shades
- all the jacks on Shades use the switch connection
- the default reference to the jack inputs is `0V`
- the switch pin, in conjunction with the three-pin header, provides an
  alternative default reference to the jack inputs of either `+5V` or `+10V`
- design:
    - tie the switch to the middle pin of a three-pin header
    - the outer pins are voltage references
    - the three-pin header is not accessible via the front panel
    - the user puts a jumper on the three-pin header prior to installing the
      module in their eurorack
    - the jumper ties the `switch` pin to either `+5V` or `+10V`
    - so the input to the jack can default to `+5V` or `+10V`
    - removing the jumper results in defaulting to `0V` because the op-amp
      is in a negative feedback configuration:
        - non-inverting terminal is tied to a `0V` reference
        - therefore the inverting terminal is driven to `0V`
        - the jack tip pin is connects to the inverting terminal via the
          the `10kΩ` pot and the `100kΩ` resistor

## Price a PCB at MacroFab
- upload `.brd` file
- disregard all unassigned files
    - these are EAGLE layers that are not necessary
    - the other layers look OK
    - but take a closer look before ordering
    - this is for pricing info only
- do not need to make a BOM:
    - MacroFab does a decent job of picking parts where the `VALUE` is something
      reasonable
    - but some parts require intervention
    - look at the `.xlsx` BOM in the `hardware_design` folder
    - or manually inspect the part:
        - left-click to select part
        - select `Open Footprint`
        - measure the footprint artwork to find out which part it is

- the 
- the PCBs have no front panel
- I have to 

- Mutable Instruments designs are 2-layer.
- DRU with conservative values:

```powershell
C:\chromation-dropbox\Dropbox\eagle\dru\PCB-NG\Conservative-clearance-check-before-2-layers-PCB-NG.dru
```

- CAM job:

```powershell
C:\chromation-dropbox\Dropbox\eagle\cam\PCB-NG\pcbng2layer-for-EAGLE-9.cam
```

## Shades
- no microcontroller
- perfect candidate for ordering as-is
- I touched up silly errors: wire stubs, angles, and clearances
- I left the Keepout and Stop Mask errors
- PCB:NG only assembles surface-mount
- [ ] generate an xyrs for the surface-mount parts
- [ ] generate a Mouser cart for through-hole parts

### PCB:NG Cost
- boards only are $231 for 6, so it will probably be about $300 for 6 with the
  SMT parts, that is $50/unit plus the cost of the through-hole parts and the
  time it will take me to solder them
- Shades is $119 new
- do not order Shades as-is
- *use* Shades in a design with Ears

### MacroFab Cost
- parts I entered manually:
- C5 and similar 22pF, selected part is not available
    - substitute
    - Murata# 81-GRM1885C1H220GA1J
    - with
    - Vishay VJ0603A220GXACW1BC
- C1 and C2:
    - footprint shows 4mm diameter cap
    - based on this diameter and the capacitance, the part is either rated for
      16VDC, 25VDC, or 35VDC:
        - <https://www.mouser.com/datasheet/2/315/ABA0000C1145-947633.pdf>
    - I picked the 35VDC part
    - Panasonic# `EEE-FK1V100UR`
    - nevermind, BOM shows the 25VDC part
    - go with what's on the BOM

# Contact Microphones for Ears
- the basic design is from
  <https://www.instructables.com/id/Make-a-Contact-Microphone/>
- the instructables uses the same family of piezo element used in Ears

## Goals
The goal of this contact microphone project is to input acoustic instruments to
Ears. But I want to do this in two ways:

1. simple: just input to Ears, good for one instrument per Ears
2. more involved: input multiple contact microphones to a pre-amp hub, copying
   the design from Ears but ignoring the envelope following part, and including
   a mixer section like Links or Shades

## BOM for a contact microphone

### [ ] try different size piezo elements
- the instructables points towards the Murata `7BB` buzzers as piezo element

#### Ears piezo element
- Ears uses the same family of piezo elements
    - the Ears BOM shows:
    - `Murata Electronics# 7BB-20-6L0`
    - the `L0` means it is sold with 2-inch leads already soldered on
    - get 10 because this is what Ears uses, so if I make Ears, I have the same
      part
    - [x] purchase 10 from Digi-Key on 2019-08-26

#### Instructables piezo element
- the instructables recommends a larger 27mm diameter piezo element
    - the larger size is probably so that it fits snug in a standard bottlecap
- here is the 27mm diameter microphone piezo element:
    - `Murata Electronics# 7BB-27-4`
    - `Digi-Key# 490-7713-ND`
    - $6.55 for 10
    - get 10 because this is what the instructables uses
    - [x] purchase 10 from Digi-Key on 2019-08-26
- and the same part but with 2-inch leads already soldered on:
    - `Murata Electronics# 7BB-27-4L0`
    - get 1 with leads for a quick test
    - [x] purchase 1 from Digi-Key on 2019-08-26

#### Smallest in family
- maybe smaller works better for some instruments?
    - the smallest in this series is 12mm diameter
    - `Murata Electronics# 7BB-12-9`
    - get 1 for testing, unfortunately not available with leads already on
    - [x] purchase 1 from Digi-Key on 2019-08-26

#### Largest in family
- or maybe larger?
    - the largest in the series is 41mm diameter
    - with 2-inch leads already soldered on
    - `Murata Electronics# 7BB-41-2L0`
    - get 1 with leads for a quick test
    - [x] purchase 1 from Digi-Key on 2019-08-26

### [ ] figure out which audio cable to use
- I am looking at two from Tensility
- both have:
    - shield
    - 3.5mm mono plug (tip/ring)
- they differ on the end with the tinned conductors
- the first has:
    - tip and ring conductors tinned
    - shield is exposed but there is no tinned conductor
- the second has:
    - tip, ring, *and* a tinned shield conductor
- I think I want the first cable, not the second
- the shield is only supposed to connect on one end
- therefore, I'm guessing that:
    - the first connects the shield to the ring at the mono plug
    - the second does not connect the shield at the mono plug since it is made
      available for connection at the tinned conductor end
- [x] buy both
- [ ] do a continuity test to see which has the shield connected internally

#### Tensility International Corp# `10-00343`

<https://tensility.com/cable-assemblies/audio-video-cables/mono-cables/10-00343>

- `Digi-Key# 839-1038-ND`
- $3.20 for 1
- $30.69 for 10
- specifications:
- 6-ft length
- shielded
- Eurorack end:
    - 3.5mm mono plug
    - Tensility# 50-00399
    - https://tensility.com/connectors/50-00399
- Piezo-soldering end:
    - 5mm-length, bare, tinned, 28AWG conductors
    - tip conductor has red jacket
    - Tensility# 30-00177
    - https://tensility.com/wire/30-00177
- shield:
    - spiral and foil
    - do not solder to piezo element
    - [ ] is this internally connected to the shield at the mono plug?
- [x] purchase 3 from Digi-Key on 2019-08-26

#### Tensility International Corp# `CA-2205`

<https://tensility.com/cable-assemblies/audio-video-cables/mono-cables/053-0279r>

- `Digi-Key# CP-2205-ND`
- $3.62 for 1
- $34.71 for 10
- specifications:
- 6-ft length
- shielded
- Eurorack end:
    - 3.5mm mono plug
    - Tensility# 50-00120
    - https://tensility.com/connectors/50-00120
- Piezo-soldering end:
    - bare, tinned, 24AWG conductors
    - tip conductor has red jacket
    - ring conductor has black jacket
    - shield is tinned as a third conductor with a heatshrink jacket
    - Tensility# 30-00005
    - https://tensility.com/wire/30-00005
- shield:
    - spiral and foil
    - shield is also broken out to a tinned wire, so...
    - solder to piezo element?
    - [ ] is this *not* internally connected to the shield at the mono plug?
- [x] purchase 1 from Digi-Key on 2019-08-26
