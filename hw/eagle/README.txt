README.txt
12/09/2020

/bmspoorman

First attempt. 

Status: Layout ran out of space.

Uses two sets of relays 

One set for by-passing the battery cells for cell balancing. 

The other set connects the ADC to each cell (in succession). The ground of the
ADC connects to the minus of the cell so aas the relays are energized the 
ground steps up the battery module (similar to using a VOM to check the 
cell voltages). This requires the grounding of the processor, and PC 
(monitoring) to be isolated.

Board layout on a two-sided 160x80mm size limit was becoming difficult.

/bmspoorman2 

Second attempt. 

Status: Board layout lost in some screw-up copying.

Two new ideas incorporated. One is to use FET flip-flops instead of 
relays for cell balancing by-passing. The other is to have the board
handle six cells. Three boards are daisy-chained with two ribbon cables.
One cable is a 20 pin battery module cable. The other is a 2x5 cable
that connects the gnd, +5, and signals.

Three boards are required, but for one or two rigs the cost is somewhat
less than having it all on one board as the minimum proto-type quantity
from the PCB fab is five.

A strip of ribbon can have multiple connectors which ties the boards
together. The last board for the battery module cable has two headers
mounted which plugs the battery module into the bus with the the other
three boards. The board space for the second header is essentially 
wasted on the other two boards since only one board needs to have 
"in/out" connectors.

Each cell position has a 2x3 jumper header for selecting with group
of six cells is connected. It is rather important these are set consistently
on the same board, otherwise a short across the cell with be made and
the pcb will have some traces rise up in an orange light of glory.

One set of relays is used for flying capacitor voltage measurement. 
This gives isolation for the cell voltage readings, so the processor
ground is isolated from the battery module ground.

The balancing by-pass is done by cross-coupled flip-flops using FETs. One
FET has a small resistor in the drain for by-passing current (e.g. 39 ohms) 
and the other FET a very large resistor that has a very small current
drain (e.g. 1M ohm). The flip-flop set/reset is via a capacitor to the
a shift register output (74HCT595). An positive/negative edge of the
shift register output sets/resets the flip-flop and the capacitor 
provides the dc offset for the cell-flip-flop.

/bmspoorman3

A hack of bmspoorman2. One cross-coupled resistor is not needed on the
flip-flop. Swapping the set/reset is expected to take care of the
situation where the battery module is plugged in but the boards are
not powered, which is a situation where one wants all the flip-flops
to come up in the non-by-passing state. 

When battery module cable is plugged in the voltage across the cell
flip-flop will cause the FET g-s capacitance plus the shift-register
to flip-flop capacitor to charge. The idea is to have the FET with the 
small resistor in the drain to have its gate voltage rise slower than
the other FET, thus leaving the flip-flop come up in the non-by-passed
state.

