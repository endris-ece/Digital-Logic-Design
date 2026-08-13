# 02 - 8-bit Multiplier

An 8-bit unsigned hardware multiplier designed in **Logisim Evolution**.

The multiplier uses sequential digital logic to perform binary multiplication over multiple clock cycles. The design is controlled by a finite state machine (FSM) and uses registers, an accumulator, a ripple-carry adder, and a loop counter to implement the multiplication process.

## Features

* 8-bit unsigned multiplication
* 16-bit multiplication result
* Sequential multi-cycle operation
* FSM-based control
* Multiplicand register
* Multiplier register with shifting
* 8-bit accumulator
* Ripple-carry addition
* Loop counter
* Clock-controlled operation
* Reset/start control
* Decimal input display
* 5-digit hexadecimal output display
* Multiplication-complete indicator

## Project Architecture

The project contains the following custom subcircuits within a single Logisim Evolution project.

### Multiplicand Register

Stores the 8-bit multiplicand.

Inputs:

* 8-bit data input
* `Enable`
* `CLK`

The register loads the input when `Enable` is active. Once disabled, the stored value remains unchanged.

The FSM controls the enable signal during the `Idle` state.

### Multiplier Register

Stores the 8-bit multiplier and provides its least significant bit (`Q0`) to the FSM.

Inputs:

* 8-bit data input
* `Enable`
* `Shift Enable`
* `CLK`

The register loads a new multiplier when enabled and can shift its stored contents when the `Shift` control signal is active.

The FSM uses the multiplier's current `Q0` value to determine whether an addition operation is required.

### Ripple Carry Adder

An 8-bit ripple-carry adder used to add the multiplicand to the accumulator.

Inputs:

* 8-bit multiplicand
* 8-bit accumulator value

Outputs:

* 8-bit sum
* `C7` carry-out

The resulting 9-bit value (`C7`, `S7...S0`) is supplied to the accumulator.

### Accumulator

Stores the intermediate multiplication result.

Inputs include:

* 9-bit result from the ripple-carry adder
* `Clear`
* `Add Enable`
* `Shift Enable`
* `CLK`

The accumulator is built using D flip-flops.

It can:

* Clear its stored value
* Load an addition result
* Shift its contents
* Maintain its current value

The accumulator provides:

* 8 individual outputs to the ripple-carry adder
* A 16-bit output to the output display

### Loop Counter

Controls the number of multiplication iterations.

The counter uses three D flip-flops and receives:

* `Clear`
* `CLK`
* `Shift Enable`

The counter output is used by the FSM to determine when the required number of multiplication cycles has been completed.

### Finite State Machine

The FSM controls the operation of the multiplier.

It uses two JK flip-flops to implement four states:

* `Idle`
* `Add`
* `Shift`
* `Done`

Inputs:

* `CLK`
* Multiplier `LSB (Q0)`
* `Start`
* `Count_Done`

Outputs:

* `Idle`
* `Add`
* `Shift`
* `Done`

The FSM determines when the circuit should load inputs, perform addition, shift the registers, and finish the multiplication.

### Input Display

Displays the decimal equivalent of the 8-bit input values.

The user enters the multiplicand and multiplier using DIP switches, while the input display provides a readable representation of the selected values.

### Output Display

Displays the 16-bit multiplication result using five hexadecimal digit displays.

A `Done` signal from the FSM is connected to an LED to indicate that the multiplication operation has completed.

When operating at a low clock frequency, the intermediate state of the accumulator can be observed during the multiplication process. The final product is considered valid once the `Done` signal becomes active.

## Operation

The user provides two 8-bit unsigned values using DIP switches.

The general operation is:

1. Set the multiplicand and multiplier using the DIP switches.
2. The input displays show the selected values.
3. Apply the clock signal.
4. Activate the `Start` input.
5. The FSM begins controlling the multiplication process.
6. The multiplier register is examined and shifted.
7. The multiplicand is added to the accumulator when required.
8. The loop counter tracks the multiplication cycles.
9. After the required iterations, the FSM enters the `Done` state.
10. The final 16-bit product is displayed.

## Control Flow

The FSM coordinates the major stages of the multiplication:

             ┌─────────┐
      Start ─►   Idle  │
             └────┬────┘
                  │
                  ▼
             ┌─────────┐
             │   Add   │
             └────┬────┘
                  │
                  ▼
             ┌─────────┐
             │  Shift  │
             └────┬────┘
                  │
            Count Done?
             ┌────┴────┐
            No         Yes
             │          │
             └──► Shift │
                        ▼
                   ┌─────────┐
                   │  Done   │
                   └─────────┘

## Number Representation

This project performs **unsigned 8-bit multiplication**.

Each input can represent:

0 to 255

The maximum product is:

255 × 255 = 65025

Therefore, a **16-bit result** is required to represent the complete product.

## Concepts Practiced

* Sequential digital logic
* Unsigned binary multiplication
* Finite state machines
* JK flip-flops
* D flip-flops
* Registers
* Shift registers
* Accumulators
* Ripple-carry adders
* Counters
* Clocked operations
* Control signals
* State-based control
* Multi-cycle hardware operations
* DIP switch inputs
* Hexadecimal displays
* LED status indicators
* Modular circuit design
* Custom subcircuits in Logisim Evolution

## Tool

**Logisim Evolution**

The complete multiplier is implemented in a single `.circ` project containing the custom subcircuits used to construct the hardware multiplier.
