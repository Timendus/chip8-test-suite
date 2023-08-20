# Why does version 5 "break compatibility"?

Interpreters that successfully pass all the tests in versions one through four
will almost certainly fail the `Display wait` test on the fifth and later
editions of this test suite. Why is that?

It has to do with how SUPER-CHIP low resolution mode works, and a feature of
that mode that's long been overlooked.

## The "hidden feature" of `lores` mode

We've all come to know the high and low resolution modes of SUPER-CHIP as
`hires` and `lores`, thanks to the instructions with those same names in Octo
and the descriptions of these opcodes in various sources. However, in [the
original description](https://groups.google.com/g/comp.sys.handhelds/c/fPUzuAkDdVs?pli=1)
of SUPER-CHIP's opcodes, the author Erik Bryntse calls this "extended screen
mode" and describes that it is used for "enabling higher speed and full screen
(64x128) resolution".

So `lores` mode, being the inverse of that, uses the lower resolution and also
_restricts the speed of the interpreter_ to 60 sprites drawn per second
(technically maybe 64, but let's not go there now 😉).
[Gulrak](https://github.com/gulrak) discovered this when running the test suite
on his HP48SX and HP48GX calculators, with the original SUPER-CHIP interpreter,
and not passing the SUPER-CHIP quirks test:

![The test suite version 4 breaking on an HP48SX](./pictures/broken-on-hp48.jpg)

And it works this way with the SUPER-CHIP 1.0, SUPER-CHIP 1.1 and CHIP48
interpreters, so it's definitely a feature, not a bug.

Probably a better way to describe `lores` mode would be "compatibility mode", as
SUPER-CHIP tries to be compatible (at least in the way of resolution and speed)
with the original Cosmac VIP interpreter in this mode.

Since the test suite ran entirely in `lores` mode until version five, it
accidentally triggered the "compatibility mode" of SUPER-CHIP and enabled the
`Display wait` quirk in the interpreter. The test would then report an error,
because SUPER-CHIP wasn't supposed to have `Display wait` enabled, according
to conventional wisdom.

## Fixing the problem

After discovering this issue, I could not possibly pretend that the quirks test
of the test suite was correct for SUPER-CHIP, since it gave an error on the
original platform. So I decided to extend the quirks test by running the
`Display wait` and `Clipping` tests in both `lores` and `hires` modes.

For SUPER-CHIP, it now expects the `Display wait` quirk to be enabled in `lores`
mode and to be disabled in `hires` mode. Otherwise, the test will fail. The
`Clipping` quirk, it turns out, should be enabled for both modes.

This gives us the expected result with the SUPER-CHIP 1.0, SUPER-CHIP 1.1 and
CHIP48 interpreters on the original hardware:

![Test suite version 5 working on HP48SX](./pictures/HP48SX-quirks.JPG)

## I'm sorry!

I'm aware that this is an annoyance for many people. And that implementing this
new quirk for SUPER-CHIP will probably make some (modern) games run
worse<super>1</super>.

However, one of the main goals of this test suite is to keep the CHIP-8
interpreters in our community from diverging even further. Every interpreter
that tries to be compatible but introduces a new problem (or "quirk" if you want
to be polite) and then has ROMs written for it, fragments the space further.
Making development even harder for future generations trying to run those ROMs.

So if the test suite encourages interpreter developers to diverge from the
original behaviour of SUPER-CHIP, then it fragments the space and it is clearly
wrong in doing so.

That's why I thought this was the "right" solution, and I hope you agree.

Happy coding!


1) You're now probably thinking of implementing yet another configurable quirk
in your interpreter, to enable this behaviour to pass the test and to disable it
when running games. I would advise againt that. Instead, try running those games
in XO-CHIP's `lores` mode, which does not restrict the drawing speed. I bet most
will run just fine with that preset. If you don't have XO-CHIP support yet, this
could be a good reason to get started 😉

