# 16×8-bit Register File

A register file containing **16 registers**, each storing **8 bits**. It supports writing data to a selected register and reading data from a selected register.

## Features

* 16 × 8-bit registers
* 4-to-16 address decoder
* Write enable control
* Read enable control
* Multiplexer-based register selection
* Hexadecimal display for 8-bit data
* Built using Logisim Evolution

## Structure

* `main.circ` — Complete register-file system
* `circuits/`

  * `input_register.circ` — 8-bit register with enable
  * `register_bank.circ` — 16-register storage bank
  * `address_decoder.circ` — 4-to-16 decoder
  * `read_mux.circ` — Selects one register for reading
  * `display.circ` — Displays 8-bit values as hexadecimal digits

## Operation

### Write

The user enters an 8-bit value and a 4-bit address. Activating **Write** stores the value in the selected register.

### Read

The user enters a 4-bit address. Activating **Read** selects the corresponding register and displays its stored 8-bit value.

## Tools

* Logisim Evolution
