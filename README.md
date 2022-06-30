# CHIP-8 test suite

_A single ROM image containing six distinct tests that will aid you in developing
your own CHIP-8, SCHIP or XO-CHIP interpreter (or "emulator")_

* [Download the ROM here](./bin/chip8-test-suite.ch8?raw=true), give it a spin and
see if your interpreter is doing the right thing! 😄
* Or [run the test suite in Octo](https://timendus.github.io/chip8-test-suite/) to
see what it **should** be doing 🙄 (it's set to "Cosmac VIP" CHIP-8 mode)

![The test suite running in CHIP-8 mode on Octo](./pictures/animation.gif)

## Table of contents

  * [Introduction](#introduction)
  * [Controls](#controls)
  * [Auto-starting a specific test](#auto-starting-a-specific-test)
  * [About the tests](#about-the-tests)
  * [Community response](#community-response-)

## Introduction

I found it hard to find reliable sources on what is the right behaviour and what
is not, especially with the subtle differences between the original "Cosmac VIP"
CHIP-8 and the HP84's SCHIP (or "superchip"). Now that I have written and ported
a couple of interpreters as well as a few programs and games for the platform, I
thought it was time to put that knowledge into code.

If you're having issues with your interpreter, you can find help in the [EmuDev
discord channel `#chip-8`](https://discord.gg/dkmJAes). If you discover a
problem with this test ROM, feel free to file an issue or open a pull request.
It's open source, licensed under the GPLv3, and you're welcome to contribute.

## Controls

When you see the CHIP-8 splash screen, press any CHIP-8 key to get to the main
menu:

![The menu for the CHIP-8 test suite](./pictures/menu.png)

In the menu, you can move the cursor up and down with CHIP-8 keys `5` and `8`
and select an item with `6`. On a PC keyboard those generally map to `W` and `S`
or `Up` and `Down` to move the cursor and `E` or `Space` to select.

Alternatively, for tests 1-4 you can press the corresponding CHIP-8 key to jump
to those tests immediately. Note that this doesn't work for the keypad test
because the `5` key is already in use for moving the cursor up.

I wanted to allow users with limited keys (like a game controller) to be able to
use this ROM too, so I needed to have a cursor and I kinda had to make this
concession. So just so you know, this is not a bug, it's a feature 😄

## Auto-starting a specific test

When you're repeatedly testing the same thing, if you're just starting out and
you have very few opcodes implemented, or if you're trying to automate your
tests, having to use the menu gets in the way. In that case, you can force the
ROM to immediately start a specific test by setting a magic value in RAM. It
will then skip waiting for a keypress and the menu entirely. To do so:

  1. Load the ROM file in memory at address `0x200` (`512`) like you normally do
  2. Set the specific test you wish to run by loading a value between 1 and 5 in
     memory at address `0x1FF` (`511`)
  3. Start execution of the ROM from address `0x200` like you normally do

## About the tests

Each test has its own page. Either [start with the first](./docs/chip8-logo.md)
or choose which one you would like to know more about:

  * [CHIP-8 splash screen](./docs/chip8-logo.md)
  * [IBM logo](./docs/ibm-logo.md)
  * [Corax89's opcode test](./docs/corax89.md) (improved version)
  * [Flags test](./docs/flags.md)
  * [Quirks test](./docs/quirks.md)
  * [Keypad test](./docs/keypad.md)

## Community response 😄

[![DUDE THANKS! I was writing a CHIP-8 emulator and THIS HELPED ME SO FRICKING MUCH, THANKS! / same here, this is amazing](./pictures/testimonial1.png)](https://github.com/Timendus/chip8-test-suite/issues/1)

[![Really nice to have new tests (flags, quirks). Especially the quirks. Fixing some bugs in my impl as we speak thanks to that.](./pictures/testimonial2.png)](https://www.reddit.com/r/EmuDev/comments/viri5r/i_wrote_a_chip8_test_suite/idet6in/?utm_source=reddit&utm_medium=web2x&context=3)

[![Really nice to have new tests (flags, quirks). Especially the quirks. Fixing some bugs in my impl as we speak thanks to that.](./pictures/testimonial3.png)](https://www.reddit.com/r/EmuDev/comments/viri5r/i_wrote_a_chip8_test_suite/idt41f1/?utm_source=reddit&utm_medium=web2x&context=3)

[![Really nice to have new tests (flags, quirks). Especially the quirks. Fixing some bugs in my impl as we speak thanks to that.](./pictures/testimonial4.png)](https://www.reddit.com/r/EmuDev/comments/viri5r/comment/idugp4j/?utm_source=reddit&utm_medium=web2x&context=3)
