# PC Engine HuBus Project

Rather than create separate repositories for each of the projects, this repository will
hold all of my projects related to the HuBus (based off of the HuCard port on the PC Engine).

## HuCard_Breakout

![HuCard_Breakout](images/HuCard_Breakout.jpg)

This is a board - actually 2 boards - which are a total of 2.4mm thick, and plug into
the HuCard slot.  A HuCard connector (rare, unfortunately) is attached at the end, but
a 40-pin (2x20) Raspberry Pi GPIO-type header header is mounted in the middle, exposing
all signals.  This becomes the basis of the bus; various memory-based peripherals.

### How to build:
You will need both HuCard_Breakout and HuCard_Breakout_under boards - the gerber files
are included:
- Make the HuCard_Breakout board 1.6mm thick, I use ENIG finish - not as durable as hard gold, but much cheaper
- Make the HuCard_Breakout_under board 0.8mm thick
You will probably want a stencil, since the two boards areintended to be held together
with solder:  I apply a low-temperature solder paste along the metallized edge, and bake
with a regular lead solder profile, with the board held together by miniature letter clips.

There are often tiny spheres of solder at the edges, which can be removed easily with a
light scrape along the edge.

Once the board is properly attached, don't forget to sand a bevel on the leading edge of
the card-edge: I use sandpaper of about 180 grit, and sand gently by hand until a bevel of
slightly less than 1mm exists evenly.

For attaching the header (and card edge connector), I clip the leads as close as possible to
the board **before soldering**, so that no sharp edges remain after the soldering.
Ideally, the solder is level, but a gentle convex curve is acceptable.


## HuMem board

![HuMem board](images/HuMem.jpg)

This board attaches to the bus, and presents the following to the bus:
- Flash memory (SST39SF010A, PDIP) at banks $90 through $9F
- Static RAM (LY625128SL-55LLI available as part of JLCPCB's SMD assembly service) at banks $B0-$EF

I have included the gerbers and relevant bom.csv and assembly.csv files to get these boards
assembled by JLCPCB, but you will still need the following parts:
- ATF16V8BQL, PDIP (and socket), and an EPROM programmer capable of programming these
- SST39SF010A, PDIP (and scoket), and as EPROM programmer capable of programming these
- a longer-than-usual 2x20 DIP header, such as PRT-16763 from Sparkfun

### How to build
Assembly should be straightforward - just remember that the long pins server as next-level
pin headers for the bus, and that the IC chips don't all face in the same direction.

### GAL logic
The GAL (ATF16V8BQL) serves as the address decoder on this board, and can be reprogrammed to
locate these memories anywhere in the address space.

The logic for this was assembled using an obsolete software package, WinCUPL, because there are
very few ways to program for 5V logic anymore (and I didn't want to use level-shift for everything
on this board).  The key files to reference in that folder are:
- MEMSEL.PLD - the CUPL source code; should be more or less self-explanatory
- MEMSEL.si  - simulation test inputs/outputs for validation of the design
- MEMSEL.jed - used for programming the GAL device

## More to come !



## Notes:

I designed all boards using the free version of EAGLE (2-layer, less than 100mm
on both X- and Y-axes).  The gerbers are included in this repository, in case you
want to get your own set made.

