# Halvin
A (currently) 4 bit Minecraft computer.

<img alt="PC Overview" src="img/pc-main.png">

## About
<img src="https://img.shields.io/badge/build-passing-brightgreen" /> <img src="https://img.shields.io/badge/coverage-78%25-yellowgreen" /> <img src="https://img.shields.io/badge/contributors-4-brightgreen" /><br>
About this project.<br><br>

## Parts
The PC has multiple parts which are also available separately. The following schematics are available:
- `parts/4bit_decoder` - A 4 bit decoder used in the instructions and the 7 segment display.
- `parts/7seg_dual_display` - A 7 segment dual digit display. Does not include decoder.
- `parts/ALU_comparator` - ALU capable of subtracting and adding two 4 numbers. The ALU is also able to compare two numbers with equal and greater than outputs.
- `parts/Bus_piece` - Piece of the bus used to connect all components. The bus can extend redstone pulses bidirectionally.
- `Instruction_board` - Board that is used for programming. Includes a decoder for a 4 bit program counter value.
- `PC_overwritable` - Program counter that can either be overwritten with a custom value.
- `parts/RAM_XX` - RAM modules.
- `parts/Register` - Register used in different parts of the computer.

## Instructions
The instructions are programmed through the instruction board, which use levers to store an instruction. Currently, there are 9 working instructions in the Halvin with some OP codes left open for future instructions. In the current full computer build, a program can consist of 16 instructions.

### Instruction bit layout
Instructions in the Halvin are 12 bits wide.
<img alt="Instruction layout" src="img/instr-layout.png" width="1000">

### OP codes
##### constant -> register
`0b0001` - Moves a constant to a register. The first `register selection bit` is used to determine what register is used, and the constant is programmed in the `constant bits`.
##### constant -> ram 
`0b0010` - Moves a constant to an address in memory. The `memory address bits` are used to select a ram cell, and the constant is put in the `constant bits`.
##### register -> ram 
`0b0011` - Moves value from register to an address in memory. The first `register selection bit` is used to determine what register is used, the `memory address bits` are used to select a ram cell.
##### ram -> register 
`0b0100` - Moves value from an address in memory to register. The same bits are used as in the `register -> ram` instruction.
##### register + register
`0b0101` - Adds the value of one register to another. The first value is taken from the register selected in the first `register selection bit`, the second value is taken from the second `register selection bit`. The resulting value is loaded into the register selected in the first `register selection bit`.
##### register - register
`0b0110` - Subtracts the value of one register to another. The bit layout is the same as the `register + register` instruction. The value in the second selected register is subtracted from the first selected register.
##### compare
`0b1000` - Compares the value of the first selected register with the one in the second selected register. The ALU tests whether the first value is greater than the second, and whether they are equal. The results of this instruction are stored in temporary flag registers inside the ALU and are not accessible to a program.
##### jump if equal
`0b1001` - Updates the `program counter` to point to an address in program memory if the `equal flag` is raised in the ALU. The address the `program counter` jumps to is given in the `constant bits`. Because this instruction is dependent on the `compare` instruction, `compare` should always be called before this instruction. Alternatively, a `register + register` or `register - register` instruction can be executed instead of `compare`, as those instructions also correctly update the ALU flag bits.
##### jump if greater
`0b1010` - Updates the `program counter` to point to an address in program memory if the `greater than flag` is raised in the ALU. The bit layout is the same as the `jump if equal` instruction. This instruction too should be preceeded by the instructions mentioned in the `jump if equal` instruction.


## Screenshots
<p>Below are some screenshots of the computer from different angles.<br>
  <img alt="PC RAM" src="img/pc-ram.png" width="400">
  <img alt="PC Screens" src="img/pc-digit-binary-screens.png" width="400">
  <img alt="PC ALU" src="img/pc-alu-and-bus.png" width="400">
  <img alt="PC Instructions" src="img/pc-instructions.png" width="400"><br>
</p>
