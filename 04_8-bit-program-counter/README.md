8-bit Program Counter

An 8-bit program counter designed in Logisim. The circuit stores the current program address and supports reset, load, hold, and increment operations.

Features

- 8-bit program counter
- Reset to "0"
- Load a custom 8-bit value
- Hold the current value
- Increment by "1"
- Priority-based control logic
- Built using flip-flops and combinational logic

Operations

Operation| Description
RESET| Clears the program counter to "0"
LOAD| Loads an external 8-bit value
HOLD| Keeps the current value
INCREMENT| Increases the current value by "1"

Control priority:

RESET > LOAD > HOLD > INCREMENT

Control Encoding

S1| S0| Operation
0| 0| Reset
0| 1| Load
1| 0| Hold
1| 1| Increment

Architecture

The program counter is divided into four main parts:

- PC Register — stores the current 8-bit program address.
- Incrementer — adds "1" to the current PC value.
- PC MUX — selects the next value to be stored in the register.
- Control Logic — determines the required operation based on the control inputs and their priority.

Operational Flow

Control Inputs
      │
      ▼
Control Logic
      │
    S1,S0
      │
      ▼
   PC MUX ◄──── Load Input
      ▲
      │
   PC Register
      │
      ▼
 Incrementer
      │
      └──────────► PC MUX

The selected value is loaded into the PC register on the clock edge.

Circuit Structure

06-8bit-program-counter/
├── main.circ
├── circuits/
│   ├── pc_register.circ
│   ├── incrementer.circ
│   ├── pc_mux.circ
│   └── control_logic.circ
└── README.md

Tools

- Logisim Evolution