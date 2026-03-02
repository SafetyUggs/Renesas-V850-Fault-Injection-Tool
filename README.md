# Renesas-V850-Fault-Injection-Tool
A tool used to extract read protected firmware from Renesas V850 MCU's

Hardware required: Sipeed Tang 9k FPGA dev stick (Aliexpress, $15). FDN337N N-Channel MOSFET. Other logic level mosfets of similar rds will work, but glitch width and delay values may need to be adjusted due to different gate capacitance and rds / switching speed.

FPGA Pins used: 
FPGA 25 - Mosfet Gate drive signal, active high
FPGA 26 - MCU Reset signal, active low
FPGA 27 - MCU UART TX
FPGA 28 - MCU UART RX

The MCU will require GND and 5v.

MCU FLMD0 must be connected to 5v.

MOSFET Drain to MCU REGC (Remove all REGC decoupling caps)
MOSFET Source to GND. Keep all MOSFET wires as short as possible.

This application can scan for suitable pulse width and delay values, and auto extract the firmware upon a match. Once the values are known, successful glitches can be triggered in a few seconds, 9600 baud extractions speed - ~8min for 384kbytes.

Gowin Tang 9k must be flashed with the glitcher firmware (.fs file) before use.

Note: You are deliberately crashing the code executing in the MCU. There is the risk of jumping to the MCU's internal erase code and triggering a chip or sector erase. Once you know the correct pulse parameters there is very little risk of this happening and has not been experienced by me in the hundreds of ours of glitch pulse scanning, though one user reported triggering a chip erase with extremely small delay values.
