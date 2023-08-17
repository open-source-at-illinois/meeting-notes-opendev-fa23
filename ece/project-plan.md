# Building a wholly open source computing platform based on RISC-V

The ECE project for OSAI's program is to develop an FPGA based 
Single Board Computer from the ground up using a completely open source
toolchain. Our ultimate goal is to design a printed Circuit Board using a powerful enough FPGA chip to run an open source Softcore RTL Design implementing
rv64gc/rv32gc. It should be feasible to opt for rv64gc since such designs do exist and have been used on FPGA development board. rv64gc also has the perk
of being able to run a full functional Linux Distro (almost completely unmodified) and an upstream kernel!

However, the significant hurdle of this project is to design the board itself.
We will be using KiCAD, an open source EDA (Electronic Design Automation) software to do so. This portion of the project will have to be thorough, and
meeting will include extended discussions of the electronics theory to do as such, and the development of the board will be a distributed effort done using assigned pull requests. 

The actual CPU is an existing design, and our OS will be Linux. While I don't
anticipate great difficulty in this area, our margin for error with regards to wiring are zero, and therefore if we miss something our board is effectively a paperweight and wouldn't be able to run any software of any kind!
## Tools
- EDA:
    - KiCAD
- CPU Designs:
    - SonicBOOM (rv64gc) (implements interesting out of order execution algorithms and is very fast): By far the best option, and an interesting study?
    - In General, SiFive and UC Berkely collaborate on a lot of designs. The most advanced of these in SonicBOOM (3rd generation of the Berkeley Out-of-Order Machines)
    - https://github.com/chipsalliance/rocket-chip (Uses SiFive Rocket Design to come up with an SoC)
    - https://github.com/riscvarchive/riscv-cores-list for more
    - VexRiscv (rv32gc)
    - Alibaba XuanTie Series (high end designs that can't feasibly be run, but interesting to look at)
- IP (for peripherals and interfaces to make a fully functional SBC):
    - LiteX (also provides toolchain to interface with the board)
    - SiFive IP Blocks

## Components
### FPGA Chip

Requirements:
- ~100K Logic Cells
- 8-10 Mb RAM
- \>400Mhz Clock Frequency
- Best Value:
  - https://www.digikey.com/en/products/detail/efinix-inc/TI180J361C4-ES/21263464
  - Efinix Titanium Ti180 (currently out of stock)
  - This chip is available in many variants and packages and pin layouts. We 
    will have to understand the pinouts and match them up with our design very carefully
    - We can also explore using the Saphire RISCV SoC (based on RV32GC VexRISCV)

An FPGA board requires you to take your designs and turn them into a 'bitstream'
using software provided by the manufacturer that uploads the design to the chip.
Every manufacturer has a different toolchain. For Xilinx (AMD) we use Vivado, 
for Efinix we have the Efinity IDE. The Efinity platform also includes IP blocks,
but perhaps we can go for something open source.
### Memory
We will require ~2GB of DRAM. This should be fairly inexpensive.
The FPGA has a DDR4 interface so we should be okay. ~$10

### Oscillator

We will require a crystal oscillator to provide a base frequency for
all components on the board

### Peripherals
- Ethernet, USB-C and HDMI Interfaces (not too costly)

### Estimated Costs 
FPGA Chip: $70

Everything Else: $60

Fabrication per board: $40

Total: ~180

### Parts Procurement Logistics
When ordering from Digikey,
any items ships in 3-5 business days.
Any product out of stock will be available within the manufacturer's lead time, which is a generally accurate estimate for when the product will be in Digikey's stock.

Our Development board is in stock, and while FPGA IC and Memory has been fixed, the exact layout variant is yet to be decided and this will be done in the initial stages of the layout design.

FPGA: Lead Time ~8 Weeks
In Stock for certain pinouts

Memory: Readily in stock (in the thousands)

Interfaces:
PCBWay has component supply services that should work
for Ethernet (modular adapter), USB-C (SMT)

Capacitors:
SMT Capacitors are readily available through PCBWay

### Board Production

We will be using PCBWay and production will be straightforward once we have to schematic ready. Production and Delivery once we submit the design take ~20 days.

We can estimate building 3 board (if the design before doesn't work) fully assembled.

### Considerations

Will the FPGA be able to run linux?

What software for PCB design?

How to implement USB, ethernet etc
- how it connects on the PCB

### Lesson plan
- Week 1: Introduction to FPGAs and PCBs: What is a computer as a semiconductor device? What parts make a modern computing machine? Meta: What is an ISA and what role does it play in the computing stack? What is an FPGA as a semiconductor device? How can it be used? Overview of the PCB Design process: Making a schematic, and then routing. What electronics theory is necessary?

- Week 2: FPGA Deepdive: Break down the internal layout of a modern FPGA. Who makes FPGAs and how? What is a hard/soft core? What is a bitstream? How can someone use an HDL to run a program on an FPGA? How are the FPGA's memory and peripherals used?

- Week 3: Demo running picoriscv32 on the FPGA Development board. Show a RISCV validation program running on the device.

- Week 4: Introduction to KiCad and abstract overview of the PCB Design process.

- Week 5: Setting up a board, and numerating our components and compartmentalising them into groups. What groups? Power, Signals, Memory, I/O.

- Week 6: FPGA Subsystem: Understanding all pinouts and banks of our FPGA. Set certain pins to certain purposes ahead of time since we should have a prototype schematic ready. Understanding how we will use Efinix's propreitary subsystems to program it.

- Week 7: Power. How to power the components of the circuit? How to thing about voltage and power as a PCB Designer? How to use buck converters and to ensure stable power supply to components

- Week 8: Connecting the FPGA to Memory. Understanding DDR3 pin layout, and connect it to FPGA.

- Week 9: I/O: Connecting FPGA to USB-C and Ethernet.

- Week 10: PCB Layout Phase: Make the 3d model of the Circuit. Explain layout, layers, traces and silkscreens.

(get PCB assembled)

- Week 11: Program FPGA and upload SonicBOOM with LiteX IP using Efinix Efinity. Demo

(This schedule is very airtight and we can add more time between weeks to get work done)

### Resources
Phils Lab FPGA Design Sequence

Altium Designer Channel FPGA Pin Out Guides

https://github.com/enjoy-digital/litex 

https://github.com/litex-hub/linux-on-litex-vexriscv

https://www.contrib.andrew.cmu.edu/~somlo/BTCP/glsomlo_cresct_2020.pdf

https://www.intel.com/content/www/us/en/content-details/775363/fpgas-for-dummies-2nd-intel-special-edition.html
