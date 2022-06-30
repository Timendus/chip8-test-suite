[ [Index](../README.md) | [Next](./ibm.md) ]

# CHIP-8 splash screen

The first test is a very simple splash screen. It is very similar to the often
used [IBM ROM](./ibm.md), but it is actually a bit easier to get running. First,
it doesn't use the "add value to register" opcode (`7XNN`) and second it only
draws aligned sprites to the screen, so you don't have to shift the bits of the
sprite to align with your display buffer.

![CHIP-8 logo, shown on the display](../pictures/chip-8-logo.png)

Run the ROM for 39 cycles to see this splash screen on the display.

This first test can tell you if you're interpreting these opcodes properly:

  * `00E0` - Clear the screen
  * `6XNN` - Load normal register with immediate value
  * `ANNN` - Load index register with immediate value
  * `DXYN` - Draw sprite to screen (only aligned)

[ [Index](../README.md) | [Next](./ibm.md) ]
