# 01 - 8-bit Signed Arithmetic Unit

An 8-bit signed arithmetic and comparison unit designed in **Logisim Evolution**.

The project operates on 8-bit two's-complement numbers and supports signed addition, subtraction, and comparison. The circuit is built from reusable custom subcircuits within a single Logisim Evolution project.

## Features

* 8-bit signed addition
* 8-bit signed subtraction
* Signed magnitude comparison
* Two's-complement number representation
* Signed overflow detection
* Conditional two's-complement conversion
* Input value display
* Output value display
* Negative-result indication
* Modular subcircuit design

## Project Architecture

The project contains the following custom subcircuits:

### Full Adder

A one-bit full adder with:

* Inputs: `A`, `B`, `Cin`
* Outputs: `S`, `Cout`

The full adder is used as the basic building block for the ripple-carry adder.

### Ripple Carry Adder

An 8-bit ripple-carry adder constructed by cascading eight `Full_Adder` subcircuits.

It produces:

* `S7 ... S0` — 8-bit sum
* `V` — signed overflow indicator

Signed overflow is detected using:

V = Cout6 XOR Cout7

where `Cout6` is the carry from bit 6 and `Cout7` is the final carry from bit 7.

### Two's Complement

An 8-bit conditional two's-complement circuit.

Inputs:

* `I7 ... I0`
* Activation signal `A`

When the activation signal is inactive, the original input is passed through. When activated, the input is converted to its two's-complement representation.

This subcircuit is reused by the addition, subtraction, and comparison circuits.

### Input Display

Converts an 8-bit two's-complement input into a displayable decimal representation using:

* Sign detection
* Two's-complement conversion when required
* Division by 10
* Remainder extraction
* Hex Digit Display components

The circuit provides three 4-bit outputs for displaying the value.

LED indicators are also used to show the sign of the input.

### Output Display

Similar to the input display circuit, but its two's-complement activation is controlled by the arithmetic operation's result rather than directly by the input MSB.

This allows signed arithmetic results to be displayed correctly.

### Adder Circuit

The addition circuit combines:

* Two `Two_s_Complement` subcircuits
* `Ripple_Carry_Adder`
* `Output_Display`

The inputs are conditionally converted when required, and the resulting sum is passed to the output display.

The circuit also determines when the result should be interpreted as negative and provides a sign indicator.

### Subtractor Circuit

Subtraction is implemented using two's-complement arithmetic:

A - B = A + (~B + 1)

The first input is passed directly while the second input is converted to its two's complement before being supplied to the `Ripple_Carry_Adder`.

The result is then passed to the `Output_Display`, with additional logic used for signed-result and sign detection.

### Comparator Circuit

The comparator determines the signed relationship between the two 8-bit inputs:

* `A > B`
* `A = B`
* `A < B`

Both inputs are processed using two's-complement conversion and then supplied to a magnitude comparator.

Additional sign-handling logic is used to produce the correct result for signed numbers.

The comparison results are represented using LEDs.

## Main Circuit

The main circuit provides the user interface for the arithmetic unit.

Two 8-bit inputs are provided using DIP switches.

A[7:0] ──┐
         ├──► Arithmetic / Comparison Circuits
B[7:0] ──┘

The inputs are simultaneously connected to:

* Input displays
* Adder circuit
* Subtractor circuit
* Comparator circuit

The arithmetic results are displayed using Hex Digit Displays, while LEDs indicate:

* Input signs
* Negative results
* Comparison results

## Signed Number Representation

The project uses **8-bit two's-complement representation**.

Therefore, the representable signed range is:

-128 to +127

The most significant bit (`MSB`) is used as the sign bit:


0 → non-negative
1 → negative


## Concepts Practiced

* Two's-complement representation
* Signed binary arithmetic
* Full adders
* Ripple-carry adders
* Carry propagation
* Signed overflow detection
* Conditional two's-complement conversion
* Signed comparison
* Multiplexing and control logic
* Encoders and priority encoders
* Binary-to-display conversion
* Seven-segment / Hex Digit Displays
* LED indicators
* Modular digital circuit design
* Hierarchical circuit construction in Logisim Evolution

## Tool

**Logisim Evolution**

The entire project is contained in a single `.circ` file, with the individual components implemented as reusable custom subcircuits within the project.
