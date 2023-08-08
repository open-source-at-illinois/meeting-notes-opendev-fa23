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


### Considerations

Will the FPGA be able to run linux?



### Resources
Phils Lab FPGA Design Sequence

Altium Designer Channel FPGA Pin Out Guides

https://github.com/enjoy-digital/litex 

https://github.com/litex-hub/linux-on-litex-vexriscv

https://www.contrib.andrew.cmu.edu/~somlo/BTCP/glsomlo_cresct_2020.pdf

https://www.intel.com/content/www/us/en/content-details/775363/fpgas-for-dummies-2nd-intel-special-edition.html
