# 4-bit ALU Design

This project documents a 4-bit Arithmetic Logic Unit (ALU) built with standard 74-series TTL ICs. The ALU accepts two 4-bit inputs, `A` and `B`, and produces a 4-bit output for one of five operations:

- Addition
- Subtraction
- Bitwise AND
- Bitwise OR
- Bitwise XOR

## Operation Selection

Three control inputs determine the selected operation:

- `S1`
- `S0`
- `A/S`

The ALU computes all possible results in parallel and uses multiplexers to select the final 4-bit output. This parallel approach reduces extra gating and inputs compared to a control-circuit structure.

## ICs Used

- `7486` - Quad XOR: Used to conditionally invert `B` bits for subtraction and to compute the XOR operation.
- `74283` - 4-bit adder: Computes `A + B` or `A - B` using two's complement arithmetic.
- `7408` - Quad AND: Computes bitwise `A AND B`.
- `7432` - Quad OR: Computes bitwise `A OR B`.
- `74153` - Dual 4-to-1 MUX: Selects the correct result for output bits.

Two `74153` chips are used to cover all four output bits, with one chip handling bits 0 and 1 and the other handling bits 2 and 3.

## Design Highlights

- Addition and subtraction share the same adder stage.
- Subtraction is implemented by inverting `B` using XOR with the `A/S` signal and setting the adder carry-in to `A/S`.
- Bitwise operations use dedicated quad-gate chips, avoiding extra logic and minimizing IC use.
- Output selection uses a dual 4-to-1 multiplexer arrangement, matching the four operation options with two select lines.

## Operation Truth Table

| Operation    | S1 | S0 | A/S | Result          |
|-------------|----|----|-----|-----------------|
| Addition    | 0  | 0  | 0   | `A + B`         |
| Subtraction | 0  | 0  | 1   | `A - B`         |
| AND         | 0  | 1  | X   | `A AND B`       |
| OR          | 1  | 0  | X   | `A OR B`        |
| XOR         | 1  | 1  | X   | `A XOR B`       |

## Results and Testing

Simulation test cases verified all five operations. Example cases include:

- Addition: `0101 + 0011 = 1000`
- Subtraction: `0111 - 0011 = 0100`
- AND: `1100 AND 1010 = 1000`
- OR: `1100 OR 1010 = 1110`
- XOR: `1100 XOR 1010 = 0110`

## Conclusion

The final ALU design uses seven ICs and satisfies the required operations with efficient use of gates and multiplexers. The design is organized to minimize wiring and IC count, and it was validated through simulation.

## Potential Improvements

- Add a carry-out output from the `74283` for overflow indication.
- Extend the ALU to support additional operations (e.g., NAND/NOR) by using a larger multiplexer such as the `74151`.


## Usage
- Open the LabFinal (1).circ file in LogiSim evolution. Use the latest version for compatibility.