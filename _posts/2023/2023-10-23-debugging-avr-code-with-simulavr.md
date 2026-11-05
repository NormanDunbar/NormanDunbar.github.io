---
title: "Debugging AVR Code with Simulavr"
layout: post
date: 2023-10-23 16:02:07+01:00
---

When writing AVR code, it can be difficult to debug problems, especially when adding `Serial.printf()` calls means that the bug vanishes! Actually, only `Serial.begin()` is required to make the bugs vanish. 

**WARNING**: The simulator hangs if you let the code run and there's a `delay()` call in the code. This *may* be an artefact of running under gdb -- I have yet to test what happens if I just run the code. Might be worth bearing this in mind.

### GDB Tutorial

See [https://www.gdbtutorial.com/gdb_commands](https://www.gdbtutorial.com/gdb_commands "https://www.gdbtutorial.com/gdb_commands") for a useful gdb tutorial

### Configuration and Execution

In order to use the option Sketch->Optimize for Debugging in the Arduino IDE, you need to do a little configuration of the IDE to allow that option to have *any* effect on Arduino boards using the ATmega328P microcontroller. See [this post from the future](/2024/04/03/configure-arduino-ide-for-debugging) for details. Once the IDE is correctly configured, you may proceed.

1. In the Arduino IDE, Sketch->Optimize for Debugging. Then rebuild the sketch with verbose compilation enabled in preferences.
1. In a bash session `cd /tmp/arduino/sketches/LONG_HEX_NUMBER` (IDE 1.x.x only) or `~/.cache/arduino/sketches/LONG_HEX_NUMBER` (IDE 2.x.x only) which you can see in the compilation output from the previous step.
1. `simulavr -g -d atmega328 -f SKETCH.ino.elf` to start the simulator. You do not need the Arduino board to be running, we are simulating it.
1. Your terminal will hang, so open another tab and run:
   ```bash
   ## The next line is for IDE 1.x.x only.
   cd /tmp/arduino/sketches/LONG_HEX_NUMBER
   
   ## The next line is for IDE 2.x.x only.
   cd ~/.cache/arduino/sketches/LONG_HEX_NUMBER
   
   ## Altogether again from here on.
   avr-gdb
   file SKETCH.ino.elf
   target remote localhost:1212
   load
   ```

You are now running the sketch in the simulator, and using gdb to set breakpoints etc in the normal manner.

### Useful gdb commands

See also [https://www.gdbtutorial.com/gdb_commands](https://www.gdbtutorial.com/gdb_commands "https://www.gdbtutorial.com/gdb_commands")

* `b location` - sets a breakpoint at `location`.
* `ir` - displays all 32 registers.
* `ir r18 r25` - displays registers `r18` and `r25` only.
* `p variable` - displays the value of a variable.
* `p (short)variable` - displays the value of a variable as a `short` data type.
* `continue`, `cont` or `c` - resumes execution after a breakpoint stop.
* `step` - steps into the next executable instruction.
* `next` - same as `step` but will treat a function call as a single instruction and will stop when the function returns, unlike `step`.
* `x/FMT ADDRESS` - displays a memory dump of `ADDRESS` in the specified `FMT`

#### FMT Specifiers

The `FMT` specifier for the `x` command is in three parts:

1. An optional counter to specify how many "data types" will be displayed.
1. The format of the output:
   * `o` = octal
   * `d` = decimal
   * `x` = hexadecimal
   * `u` = unsigned int
   * `s` = string
   * `t` = binary
1. The data type:
   * `b` = bytes
   * `h` = half words (16 bit)
   * `w` = words (32 bit)
   * `g` = double word (64 bits).
