Project Overview
![image](https://github.com/flfl04/SPI_Verilog/assets/105518119/26ab0bb0-1722-4734-ad6e-7a613f9403a7)
Codes Folder
ram.dat: Memory file for the testbench.
run.do: DO file to run simulations in QuestaSim or ModelSim.
RTL Folder
SPI.v: Design of the SPI block.
RAM.v: Design of the RAM block.
instantiation.v: Top module.
run.tcl: TCL script to run the design on Vivado. Generates elaboration_schematic.pdf, synthesized_schematic.pdf, utilization report, timing report, and executes elaboration, synthesis, implementation, and bitstream generation.
Testbench Folder
SPI.v: Verilog file for SPI Slave block.
RAM.v: Verilog file for Single Port Async RAM.
SystemLevel.v: Verilog file that instantiates the RAM and SPI blocks.
ram.dat: Memory file for the testbench.
Schematics
SPI Schematic: Post-synthesis schematic for the SPI block.
RAM Schematic: Post-synthesis schematic for the RAM block.
System Level Schematic: Post-synthesis schematic for the entire system.
Additional Files
basys_master.xdc: Constraint file for the target FPGA.
bitstream file: Generated bitstream file.
netlist file: Netlist file from Vivado.
SPI Slave Module
The SPI slave module is responsible for receiving data from the master device and interacting with the RAM module.

Ports:
clk: Input, 1 bit, Clock signal
rst_n: Input, 1 bit, Active low reset signal
SS_n: Input, 1 bit, Slave Select signal
MOSI: Input, 1 bit, Master-Out-Slave-In data signal
tx_data: Input, 10 bits, Transfer data output signal, stores data to send to RAM
tx_valid: Input, 1 bit, Indicates when tx_data is valid
MISO: Output, 1 bit, Master-In-Slave-Out data signal
rx_data: Output, 10 bits, Received data from the memory
rx_valid: Output, 1 bit, Indicates when rx_data is valid
Single Port Async RAM Module
Implements a memory block with a single data port.

Parameters:
MEM_DEPTH: Default 256, Depth of the memory
ADDR_SIZE: Default 8, Size of the memory address
Ports:
clk: Input, 1 bit, Clock signal
rst_n: Input, 1 bit, Active low reset signal
din: Input, 10 bits, Data input
rx_valid: Input, 1 bit, If HIGH, accepts din[7:0] as address or data
dout: Output, 8 bits, Data output
tx_valid: Output, 1 bit, Indicates a memory read
Commands:
00: Write address
01: Write data
10: Read address
11: Read data, tx_valid HIGH, dout holds the read word
Wire Connections:
rx_data in SPI slave connected to din in RAM.
rx_valid in SPI slave connected to rx_valid in RAM.
dout in RAM connected to tx_data in SPI slave.
tx_valid in RAM connected to tx_valid in SPI slave.
Finite State Machine (FSM)
Implements the control logic for SPI and RAM interactions.
