# Details for Tetris

This is a side project I've been working on to build a physical tetris device; I've been targeting a myRIO, but the code should be similar regardless. It uses the Actor Framework, and is saved in LabVIEW 2017.

## General architecture

This isn't thoroughly fleshed out, but a few key concepts are as follows:

* Every actor inherits from an error handling class. This allows us to handle all errors in one location, regardless of where they come from
* The input device is _not_ an actor, because we don't want to get input async. Instead, we manually poll each time we want an update.
* Our display device, however, is an actor; we don't want to hang the game waiting for a draw to occur.
* Abstract classes define and provide core functionality for both display and input device classes. You /must/ extend these to make anything work.

## Work needed

* Build a simulated display and joystick. I'm envsioning host side code that serves as the display and input. I'll probably use a network stream to get data to the display and a shared variable to get gamepad values.
* Integrate actual hardware. The myRIO allows you to use standard USB gamepads, so that's mostly done. I'll likely  have two different display methods:
  * An array of individually addressable RGB LEDs; I'll use the FPGA to build pulsetrains to control them.
  * An LCD display I have sitting around. Once again, pulsetrains on the FPGA.