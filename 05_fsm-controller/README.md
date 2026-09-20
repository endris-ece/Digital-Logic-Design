FSM Controller

A synchronous 4-state finite state machine (FSM) designed in Logisim. The controller demonstrates state storage, conditional state transitions, and state-based outputs.

Features

- 4-state FSM
- Synchronous state transitions
- External condition input ("X")
- Reset to "IDLE"
- LED output indicating the current state
- Implemented using flip-flops and combinational logic

States

State| Code
IDLE| "00"
READ| "01"
PROCESS| "10"
DONE| "11"

Transition Table

Current State| X = 0| X = 1
IDLE| IDLE| READ
READ| READ| PROCESS
PROCESS| IDLE| DONE
DONE| IDLE| READ

Example

With "X = 1":

IDLE → READ → PROCESS → DONE → READ → ...

With "X = 0":

IDLE → IDLE
READ → READ
PROCESS → IDLE
DONE → IDLE

The reset input forces the FSM back to "IDLE".

Architecture

        X
        │
        ▼
Next-State Logic
        │
      D1,D0
        │
        ▼
 State Register
        │
      Q1,Q0
       /   \
      ▼     ▼
Next-State  Output
   Logic     Logic
              │
              ▼
             LEDs

Circuit Structure

circuits/
├── state_register.circ
├── next_state_logic.circ
└── output_logic.circ

Tools

- Logisim Evolution