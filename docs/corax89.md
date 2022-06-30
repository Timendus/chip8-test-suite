# Corax89's opcode test

This ROM is also a famous one, [written by
Corax89](https://github.com/corax89/chip8-test-rom). Many people use this ROM to
prove to themselves that their interpreter runs as it should. However, there are
a couple of [minor issues with the
ROM](https://github.com/corax89/chip8-test-rom/pulls) and Corax89 doesn't really
seem to be maintaining this ROM anymore. So I've taken the liberty to include it
in this suite, with those issues fixed and some minor cosmetic improvements.

To auto-start, load the value `2` into memory at `0x1FF`, load the ROM in memory
starting from `0x200` and start your interpreter.

![Corax89's opcode test](../pictures/corax89.png)

The codes on the screen correspond to the functioning of these opcodes:

```
3XNN	00EE	8XY5
4XNN	8XY0	8XYE
5XY0	8XY1	8XY6
7XNN	8XY2	FX55
9XY0	8XY3	FX33
2NNN	8XY4	1NNN
```

If you see `OK`, they're at least somewhat functional in the happy path. If you
see `NO` you can be sure that you have an issue with that opcode.

If you are having trouble figuring out how each opcode is supposed to behave,
check out [Tobias' guide](https://tobiasvl.github.io/blog/write-a-chip-8-emulator/#instructions).
