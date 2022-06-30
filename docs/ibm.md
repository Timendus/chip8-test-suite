[ [Previous](./chip8-logo.md) | [Index](../README.md) | [Next](./corax89.md) ]

# IBM logo

The first test that is in the menu is the classic IBM ROM. If the splash screen
works as expected, this test should be pretty easy to pass, but it is a rite of
passage for any CHIP-8 developer.

I did not write this ROM, it's probably decades old and I'm not sure who wrote
it so I can't really credit them. The code in this suite is a re-implementation
in Octo-mnemonics by my own hand, but it compiles to the exact same bytes as the
original.

![IBM logo, shown on the display](../pictures/ibm-logo.png)

Run the ROM for 64 cycles to see the IBM logo on the display. If you can see the
IBM logo, you are properly interpreting these opcodes in addition to the opcodes
used by the [CHIP-8 splash screen](./chip8-logo.md):

  * To get to the IBM logo code from the CHIP-8 splash screen:
    * `1NNN` - Jump
    * `FX65` - Load register from memory
    * `4XNN` - Skip next instruction if unequal
  * To show the IBM logo:
    * `7XNN` - Add immediate value to normal register
    * `DXYN` - Draw sprite to screen (un-aligned)

## Auto starting

To auto-start, load the value `1` into memory at `0x1FF`, load the ROM in memory
starting from `0x200` and start your interpreter.

[ [Previous](./chip8-logo.md) | [Index](../README.md) | [Next](./corax89.md) ]
