# Keypad test

This test allows you to test all three CHIP-8 key input opcodes. It shows you a
little menu, asking which opcode you would like to test:

![Choosing the opcode to test in the keypad test](../pictures/keypad-menu.png)

## 1. `EX9E DOWN`

`EX9E` skips the next instruction if the key indicated in `vX` is currently
pressed. In the test, when you press a key, the corresponding value lights up on
the screen.

![The `EX9E` keypad test, when pressing keys 1 and 6](../pictures/keypad-down.png)

_Pressing keys 1 and 6_

## 2. `EXA1 UP`

`EXA1` skips the next instruction if the key indicated in `vX` is currently
**not** pressed. In the test, when you are **not** pressing a key, the
corresponding value lights up on the screen.

![The `EXA1` keypad test, when pressing keys 1 and 6](../pictures/keypad-up.png)

_Pressing keys 1 and 6_

## 3. `FX0A GETKEY`

`FX0A` waits for a key press and returns the pressed key in `vX`.

The test asks you to press a key on the CHIP-8 keypad. When you do, it checks
for two issues that are easy to accidentally introduce when implementing this
opcode. If all is well, you should be seeing a checkmark and "all good" on the
screen:

![The `FX0A` keypad test, when all is good](../pictures/keypad-getkey.png)

Otherwise, you can get either of these errors:

* `NOT HALTING` - Your implementation immediately returns the value of any
  currently pressed keys in `vX`, instead of halting the interpreter until a key
  is pressed (note that this needs timer support to be accurate)
* `NOT RELEASED` - Your implementation doesn't wait for the pressed key to be
  released before resuming

See [this
article](https://laurencescotford.com/chip-8-on-the-cosmac-vip-keyboard-input/)
for more information.

## Auto starting

To auto-start this test, load the value `5` into memory at `0x1FF` and load the
ROM in memory starting from `0x200`. Additionally, you can also force the target
opcode by loading a value between 1 and 3 into memory at the address `0x1FE`
(510).
