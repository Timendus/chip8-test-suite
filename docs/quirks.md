# Quirks test

CHIP-8, SCHIP and XO-CHIP have subtle differences in the way they interpret the
bytecode. We often call these differences quirks. This test detects which quirks
your interpreter implements, and if those quirks match the platform you're
trying to target. This is one of the hardest parts to "get right" and often a
reason why "some games work, but some don't".

To auto-start this test, load the value `4` into memory at `0x1FF` and load the
ROM in memory starting from `0x200`. Additionally, you can also force the target
platform by loading a value between 1 and 3 into memory at the address `0x1FE`
(`510`). Otherwise the test asks you to choose one:

![Choosing a target platform in the quirks test](../pictures/quirks-platform.png)

This menu works exactly the same as the main menu in terms of
[controls](../README.md#controls).

The test will now run through a couple of steps, which you will see on the
screen as some garbage and a bunch of smiley faces. After about two seconds, you
should see this screen:

![Showing the active quirks](../pictures/quirks.png)

The screen shows you if the following quirks are detected as active ("on", "off"
or "err" if inconsistent or broken) and if that matches your chosen target
platform (a checkmark or a cross).

* `vF reset` - The AND, OR and XOR opcodes (`8XY1`, `8XY2` and `8XY3`) reset the
  flags register to zero
* `Memory` - The save and load opcodes (`FX55` and `FX65`) increment the index
  register (more information [here](https://laurencescotford.com/chip-8-on-the-cosmac-vip-loading-and-saving-variables/) and [here](https://tobiasvl.github.io/blog/write-a-chip-8-emulator/#fx55-and-fx65-store-and-load-memory))
* `Display wait` - Drawing sprites to the display waits for the vertical blank
  interrupt, limiting their speed to max 60 sprites per second (more information
  [here](https://laurencescotford.com/chip-8-on-the-cosmac-vip-drawing-sprites/))
* `Clipping` - Sprites drawn at the bottom edge of the screen get clipped instead
  of wrapping around to the top of the screen (more information
  [here](https://laurencescotford.com/chip-8-on-the-cosmac-vip-drawing-sprites/))
* `Shifting` - The shift opcodes (`8XY6` and `8XYE`) only operate on `vX`
  instead of storing the shifted version of `vY` in `vX` (more information
  [here](https://tobiasvl.github.io/blog/write-a-chip-8-emulator/#8xy6-and-8xye-shift))
* `Jumping` - The "jump to some address plus `v0`" instruction (`BNNN`) doesn't
  use `v0`, but `vX` instead where `X` is the highest nibble of `NNN` (more
  information [here](https://tobiasvl.github.io/blog/write-a-chip-8-emulator/#bnnn-jump-with-offset))

Note that you need timer support for this test to run.
