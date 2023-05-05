![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg) ![](../../workflows/wokwi_test/badge.svg)

# Async Balanced Ternary Calculator
A 2-trit async balanced ternary calculator allowing multiplication, addition and subtraction with negative numbers in binary encoded ternary

## Description
This chip is a 2-trit asynchronous balanced ternary calculator having 2 functions: multiplication and addition/subtraction (which is one function in balanced ternary). It demonstrates how to build ternary logic with binary transistors using binary encoded ternary (BET). 1-trit (3 values) is thus encoded in 2-bits (4 values, 1 is ignored). This inefficient encoding is neccesary since current CMOS processes can only construct binary transistors. Despite this inefficiency, there are several benefits on various levels. We use balanced ternary notation meaning that each trit contains -1, 0 and +1. This allows balanced arithmethic with negative numbers without any special circuitry or convention (eg. 2's complement). Typically designing ternary logic is cumbersome. The open source tool MRCS works with binary and ternary and mixed truth tables (TT) that automatically convert to netlist and verilog. This means a designer does not need to think in binary when making ternary logic. The design can be verified 1) manually in the tool, 2) automated by uploading a CSV with TT input-output pairs, 3) by using Vivado verilog simulator (test bench is included), 4) by deploying on FPGA (constraint file for Xilinx Basys3 is included) or 5) by using HSPICE for analog verification. The HSPICE verification is currently using 3 types of carbon nanotubes transistors (CNTFET) as technology as these are designed for ternary signals. Future versions of MRCS will integrate the various SPICE libs from the Sky130 open PDK. 

## Features: 
- balanced ternary multiplication
- balanced ternary addition/subtraction 

## Interactive simulation 
1) Load MRCS WebGL at https://ternaryresearch.com/mixed-radix-circuit-synthesizer/ or build offline https://github.com/aiunderstand/MixedRadixCircuitSynthesis
2) Click "Import component" and select the TT03_BTCalculator.zip package from this repo
3) Drag and drop the chip on the canvas and click on the inputs to see the computations being done in real-time. 

## FPGA with Digilent Basys3 (Artix-7) and Vivado
0a) [Install Vivado ML Free](https://www.xilinx.com/products/design-tools/vivado.html#editions), [See instructions](https://digilent.com/reference/programmable-logic/guides/installing-vivado-and-vitis)
0b) [Install FPGA Board eg. for Basys3](https://github.com/Digilent/vivado-boards?_ga=2.157791610.1532643487.1683319632-1629076669.1682349043), [manual of Basys3](https://digilent.com/reference/programmable-logic/basys-3/start) 

1) Create new project, choose FPGA board (eg. Basys3) and set top module name to *c_TT3_BTCalculator*
2) Add design source, select */src/c_TT03_BTCalculator.v* 
3) Add simulation source, select */src/c_TT03_BTCalculator_tb.v*
4) Add constraints, select */src/Basys3_FPGA/basys3_constraints_8x8.xdc*
5) Run simulation. Confirming that input-output result is 55->96 and 79->db
6) Run synthesis.
7) Run implementation.
8) Generate bitstream and program
9) Optional: flash the chip permanently by following [these instructions](https://sites.google.com/a/umn.edu/mxp-fpga/home/vivado-notes/programming-the-basys3-boards-non-volatile-flash-memory-through-vivado)


####Simulation View
![Simulation View](https://user-images.githubusercontent.com/6376127/236565410-835f88f1-1256-4e66-8701-5957bad7bad3.png)

####Schematic View
![Schematic View](https://user-images.githubusercontent.com/6376127/236565434-c01e3d6d-c1af-4f6d-a6a7-a920d803c86f.png)

####Layout View
![Layout View](https://user-images.githubusercontent.com/6376127/236565454-211ef783-918f-40f0-82dd-5fbc2cd9bc4f.png)

## Video
2do

## Images
![tt03_BTCalculator](https://user-images.githubusercontent.com/6376127/236537010-23d40e56-3591-4687-bcd3-6532dea8da82.png)

![GDS (die) shot](https://user-images.githubusercontent.com/6376127/236537573-b82ada43-5148-4762-9e68-377a44ea1426.png)

2do Add HSPICE image



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
