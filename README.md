# Rubik’s Cube Solver using Finite State Machines (FSM)

A hardware Finite State Machine (FSM) that guides a user through solving a Rubik’s Cube after the first two layers are completed. The system uses combinational logic, sequential logic, and LED-based visual instructions to provide step-by-step guidance.

This project was designed, simulated, and implemented as a physical digital logic circuit.

---
## Project Overview

This system assists the user in solving the final layer of a Rubik’s Cube through four structured FSM stages:

1. Create the Yellow Cross  
2. Align Yellow Edges  
3. Position Yellow Corners  
4. Orient Yellow Corners (Final Solve)

At each stage, the user provides binary inputs describing the cube’s current configuration. The FSM then:
- Indicates which cube face to orient forward
- Displays the correct solving algorithm via LEDs
- Detects invalid or impossible cube states
- Advances automatically once a stage is completed

---

## System Inputs and Outputs

### Inputs
- 8 total binary inputs
  - 4 inputs for yellow edges
  - 4 inputs for yellow corners

Inputs are reused across stages to represent:
- Presence of yellow edges
- Edge-to-center alignment
- Correct corner positioning
- Correct corner orientation

### Outputs
- Face-orientation LEDs (Red, Blue, Green, Orange)
- Algorithm instruction LEDs
  - 4 LEDs (Stages 1–2)
  - 5 LEDs (Stage 3)
  - 8 LEDs (Stage 4)
- Status LEDs
  - Green: stage complete
  - Red: invalid or impossible state

---

## FSM Stages

### Stage 1 — Create the Yellow Cross
Identifies one of four cases (dot, hook, line, cross) based on edge inputs and outputs the appropriate algorithm:

- Line: `F R U R' U' F'`
- Hook: `F U R U' R' F'`
- Dot: Line → `U U` → Hook  

If the cross already exists, the FSM signals completion.

---

### Stage 2 — Align Yellow Edges
Ensures each yellow edge matches its corresponding center color.

- Outputs either:
  - Sune algorithm: `R U R' U R U2 R'`
  - Modified Sune
- Impossible configurations trigger an error signal.

---

### Stage 3 — Position Yellow Corners
Determines whether corners are in their correct positions (orientation ignored).

- Implemented as a two-substage FSM
- Uses a memory flip-flop to store intermediate state
- Algorithms include:
  - `R U L U' R' U L' U'`
  - Special case: `L U' R U L' U' R' U`

---

### Stage 4 — Orient Yellow Corners (Final Solve)
Orients all yellow corners to face upward.

- Uses repeated applications of the Lefty algorithm:
  - `L' U' L U`
- FSM outputs an LED sequence guiding repetitions and U turns
- Completion signals a fully solved cube

---

## FSM Architecture

- 3-bit binary counter for stage progression
- 3-to-8 decoder to activate stage logic
- D flip-flops for state memory
- 2-to-4 decoder for face orientation
- Each stage implemented with independent combinational logic
- All stages integrated into a single hardware system

---

## Simulation and Hardware

- Fully verified using digital logic simulation
- Implemented on physical breadboards
- Includes FSM logic, decoders, flip-flops, and LED-based instruction system

Simulation screenshots and hardware photos are included in the project documentation.

---

## Documentation

- `Documentation Rubik's Cube.pdf` — Full report including design decisions, algorithms,
