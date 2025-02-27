![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg) ![](../../workflows/wokwi_test/badge.svg)

# Async Balanced Ternary Calculator
A 2-trit async balanced ternary calculator allowing multiplication, addition and subtraction with negative numbers in binary encoded ternary

![Chip overview](https://user-images.githubusercontent.com/6376127/236570359-f9235439-efb3-4894-984d-8a67f9a3ce30.png)

## Description
This chip is a 2-trit asynchronous balanced ternary calculator having 2 functions: multiplication and addition/subtraction (which is one function in balanced ternary). It demonstrates how to build ternary logic with binary transistors using binary encoded ternary (BET). 1-trit (3 values) is thus encoded in 2-bits (4 values, 1 is ignored). This inefficient encoding is neccesary since current CMOS processes can only construct binary transistors. Despite this inefficiency, there are several benefits on various levels. We use balanced ternary notation meaning that each trit contains -1, 0 and +1. This allows balanced arithmethic with negative numbers without any special circuitry or convention (eg. 2's complement). Typically designing ternary logic is cumbersome. The open source tool MRCS works with binary and ternary and mixed truth tables (TT) that automatically convert to netlist and verilog. This means a designer does not need to think in binary when making ternary logic. The design can be verified 1) manually in the tool, 2) automated by uploading a CSV with TT input-output pairs, 3) by using Vivado verilog simulator (test bench is included), 4) by deploying on FPGA (constraint file for Xilinx Basys3 is included) or 5) by using HSPICE for analog verification. The HSPICE verification is currently using 3 types of carbon nanotubes transistors (CNTFET) as technology as these are designed for ternary signals. Future versions of MRCS will integrate the various SPICE libs from the Sky130 open PDK. 

## Features: 
- balanced ternary multiplication
- balanced ternary addition/subtraction 

## Interactive simulation 
1) Load MRCS [WebGL](https://ternaryresearch.com/mixed-radix-circuit-synthesizer/) or build [Standalone (Unity C# Project)](https://github.com/aiunderstand/MixedRadixCircuitSynthesis)
2) Click "Import component" and select the *src/MRCS/MRCS_Export_TT03-BTCalculator.zip* package from this repo
3) Drag and drop the chip on the canvas and click on the inputs to see the computations being done in real-time. 
4) To verify in MRCS, open the chip such that the inputs and outputs are visible. Click verify and upload the *src/Tests/test_tt03-btcalculator.csv*. Wait a few minutes to see a verification result screen.

## Youtube video

[![Youtube link to MRCS tt03-btcalculator project](https://img.youtube.com/vi/-DzVKAxmSQ0/0.jpg)](https://www.youtube.com/watch?v=-DzVKAxmSQ0)

## FPGA with Digilent Basys3 (Artix-7) and Vivado
1) [Install Vivado ML Free](https://www.xilinx.com/products/design-tools/vivado.html#editions), [See instructions](https://digilent.com/reference/programmable-logic/guides/installing-vivado-and-vitis)
2) [Install FPGA Board eg. for Basys3](https://github.com/Digilent/vivado-boards?_ga=2.157791610.1532643487.1683319632-1629076669.1682349043), [manual of Basys3](https://digilent.com/reference/programmable-logic/basys-3/start) 
3) Create new project, choose FPGA board (eg. Basys3) and set top module name to *c_TT3_BTCalculator*
4) Add design source, select */src/c_TT03_BTCalculator.v* 
5) Add simulation source, select */src/c_TT03_BTCalculator_tb.v*
6) Add constraints, select */src/Basys3_FPGA/basys3_constraints_8x8.xdc*
7) Run simulation. Confirming that input-output result is 55->96 and 79->db
8) Run synthesis.
9) Run implementation.
10) Generate bitstream and program
11) Optional: flash the chip permanently by following [these instructions](https://sites.google.com/a/umn.edu/mxp-fpga/home/vivado-notes/programming-the-basys3-boards-non-volatile-flash-memory-through-vivado)


#### Simulation View
![Simulation View](https://user-images.githubusercontent.com/6376127/236565410-835f88f1-1256-4e66-8701-5957bad7bad3.png)

#### Schematic View
![Schematic View](https://user-images.githubusercontent.com/6376127/236565434-c01e3d6d-c1af-4f6d-a6a7-a920d803c86f.png)

#### Layout View
![Layout View](https://user-images.githubusercontent.com/6376127/236565454-211ef783-918f-40f0-82dd-5fbc2cd9bc4f.png)

## HSPICE (with CNTFET instead of SKY130 CMOS)
#### Balanced Ternary (Half) Adder - Heptavintimal index 7PB (SUM) and RDC (CARRY)

![BTA overview](https://user-images.githubusercontent.com/6376127/236571779-62805118-68e0-48ad-a185-b19569f56a5d.png)

The two truthtables of the BTA. Note that the input B is 0 and input A is 1 and output is 1 (0+1=1). The truthtable cell becomes more yellow and finally red when the state is used more.

![Truthtable implementation of the BTA](https://user-images.githubusercontent.com/6376127/236571604-236db468-846a-4297-84c1-d2782bbd339d.png)

The discrete CNTFET transistor implementation of 7PB (SUM) generated by MRCS. Transistors that are greyed-out are not conducting with given input. Visible is that a single transistor path is active (in this case actually 2!), thus connecting output to VDD resulting in output 1 and reflecting the truth table state.

![Discrete CNTFET transistor implementation of 7PB (SUM)](https://user-images.githubusercontent.com/6376127/236573298-91801292-a96a-4157-89d8-88265762c1a1.png)

2do add HSPICE sim of the 7PB

## Images
#### Balanced ternary calculator overview
![tt03_BTCalculator](https://user-images.githubusercontent.com/6376127/236537010-23d40e56-3591-4687-bcd3-6532dea8da82.png)

#### Balanced ternary adder (BTA4)

![bta4](https://user-images.githubusercontent.com/6376127/236623453-1dcce0e1-5859-4700-a88e-b6090558c2e2.png)

#### Balanced ternary multiplier (BTM4)

![btm4](https://user-images.githubusercontent.com/6376127/236626738-dbd25fd1-1d22-4210-ac48-b560486c610e.png)

#### Balanced ternary multiplier

![btm](https://user-images.githubusercontent.com/6376127/236623445-c1334297-cf60-49b9-9877-6b67c54320ce.png)

#### Deselect4

![deselect4](https://user-images.githubusercontent.com/6376127/236623440-1efc6446-ca1f-4f71-952c-727b9f9e08b4.png)

#### Tiny Tapeout die shot
![GDS (die) shot](https://user-images.githubusercontent.com/6376127/236537573-b82ada43-5148-4762-9e68-377a44ea1426.png)

## How does it work?
MRCS allows binary and ternary truth tables. Both balanced {-1,0,1} and unbalanced {0,1,2} ternary is allowed. The key thing to realize is that balanced and unbalanced ternary is only a semantic interpretation. Physically they are the same signals. Binary is just the extreme sides of them. So for balanced ternary logical -1 is 0 Volt, logical 0 is VDD/2 and logical 1 is VDD. In the case of binary logical 0 = 0 Volt and logical 1 is VDD. In the case of unbalanced ternary the logical 0 is 0 Volt, logical 1 is VDD/2 and logical 2 is VDD. This interpretation scheme works for single power supply circuit. In the case of dual power supply, at the expense of additional power routing (and resulting in several benefits) the interpretation scheme for balanced ternary becomes logical -1 is -VDD, logical 0 is 0 Volt (actively driven!) and logical 1 is VDD. For Binary it becomes logical 0 is -VDD and logical 1 is VDD. With this interpreting binary in a ternary signal is simple, it is always the extremes. 

We use the following binary encoded ternary (bet) scheme:
- Logical -1 = 2'b01 (first bit is MSB)
- Logical 0 = 2'b11 
- Logical 1 = 2'b10 
- illegal = 2'b00

The reason for this scheme is that a 1bit DAC implemented with a differential opamp can interpret logical -1 and logical 1 since there is a difference signal. In addition, this scheme allows binary synthesis tools such as ABC to optimize the 2'b00 state. If the circuit is in that state, we know there is an issue. Finally, since all transitions are single bit changes (with 3 states, a property due to balanced ternary arithmethic) power consumption is low. Normally with binary arithmetic, to process negative numbers all bits need to be flipped (inverted) plus one (2's complement conversion) followed by a regular ADD operation. 

In pictures, the inputs and outputs are automatically converted by MRCS from ternary to binary.  Below is a 4 trit to 8 bit conversion as used in this chip. For example x1 is a logical -1 and is encoded as 2'b01. 

![Conversion from 4 trit input to 8 bit input](https://user-images.githubusercontent.com/6376127/236621405-fd88b9b1-8c07-4945-8be1-6441cb919041.png)

The truth table functions are automatically converted from ternary to binary. For example the balanced ternary standard inverter, STI or heptavintimal index 5 is converted to binary encoded ternary as follows: 

![Conversion from ternary function to binary function](https://user-images.githubusercontent.com/6376127/236621746-fec1cedb-9c59-46b9-bf21-82b4dc258ca4.png)

For this image you still have to imagine that the ternary input signal logical 0 is actually encoded as 2'b11. The generated verilog for this function looks like this:

```verilog
module c_STI (
     input [1:0] io_in,
     output [1:0] io_out
);

wire [1:0] tnet_0 = io_in[1:0]; //in

wire [1:0] tnet_1;

assign io_out[1:0] = tnet_1; //out

f_5_bet LogicGate_0 (
.portA(tnet_0),
.out(tnet_1)
);

endmodule

module f_5_bet (
     input wire[1:0] portA,
     output wire[1:0] out
     );

     assign out = 
    (portA == 2'b01) ? 2'b10 :
    (portA == 2'b10) ? 2'b01 :
     2'b11;
endmodule
```


# What is Tiny Tapeout?

TinyTapeout is an educational project that aims to make it easier and cheaper than ever to get your digital designs manufactured on a real chip!

Go to https://tinytapeout.com for instructions!

## How to change the Wokwi project

Edit the [info.yaml](info.yaml) and change the wokwi_id to match your project.

## How to enable the GitHub actions to build the ASIC files

Please see the instructions for:

* [Enabling GitHub Actions](https://tinytapeout.com/faq/#when-i-commit-my-change-the-gds-action-isnt-running)
* [Enabling GitHub Pages](https://tinytapeout.com/faq/#my-github-action-is-failing-on-the-pages-part)

## How does it work?

When you edit the info.yaml to choose a different ID, the [GitHub Action](.github/workflows/gds.yaml) will fetch the digital netlist of your design from Wokwi.

After that, the action uses the open source ASIC tool called [OpenLane](https://www.zerotoasiccourse.com/terminology/openlane/) to build the files needed to fabricate an ASIC.

## Resources

* [FAQ](https://tinytapeout.com/faq/)
* [Digital design lessons](https://tinytapeout.com/digital_design/)
* [Learn how semiconductors work](https://tinytapeout.com/siliwiz/)
* [Join the community](https://discord.gg/rPK2nSjxy8)

## What next?

* Share your GDS on Twitter, tag it [#tinytapeout](https://twitter.com/hashtag/tinytapeout?src=hashtag_click) and [link me](https://twitter.com/matthewvenn)!
