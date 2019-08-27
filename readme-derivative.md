Derivative Work by Goat Curry

# Price Module Builds
I use PCB:NG in Brooklyn.

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

### Cost
- boards only are $231 for 6, so it will probably be about $300 for 6 with the
  SMT parts, that is $50/unit plus the cost of the through-hole parts and the
  time it will take me to solder them
- Shades is $119 new
- do not order Shades as-is
- *use* Shades in a design with Ears

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

#### Instructables piezo element
- the instructables recommends a larger 27mm diameter piezo element
    - the larger size is probably so that it fits snug in a standard bottlecap
    - here is the 27mm diameter microphone piezo element:
        - `Murata Electronics# 7BB-27-4`
        - `Digi-Key# 490-7713-ND`
        - $6.55 for 10
    - and the same part but with 2-inch leads already soldered on:
        - `Murata Electronics# 7BB-27-4L0`

#### Smallest in family
- maybe smaller works better for some instruments?
    - the smallest in this series is 12mm diameter
    - `Murata Electronics# 7BB-12-9`

#### Largest in family
- or maybe larger?
    - the largest in the series is 41mm diameter
    - with 2-inch leads already soldered on
    - `Murata Electronics# 7BB-41-2L0`

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
- [ ] buy both and do a continuity test

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
