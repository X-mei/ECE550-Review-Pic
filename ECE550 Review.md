# ECE550 Review

## Chapter 1 Foundamentals
- Processors are made of transistors
- Abstraction: divide interface from implementation
- Build larger components from smaller ones
- Reuse component

## Chapter 2 Gates
- Basic building block NMOS and PMOS
- NMOS conduct when input is high, PMOS conduct when input is low
![chap2-1](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap2-1.png?raw=true)
- Switching delays occur due to Voltage, Resistance and Capacitance.
- Paradigm: use PMOS on PUN and NMOS on PDN.
- Some basic boolean gates:
![chap2-2](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap2-2.png?raw=true)
- Moore's law: Transistor density doubles roughly every 18 months.
- Hooking up two output get short circuits.
- If input is not hooked up, it behaves kind of randomly.
- Get formula by computing sum of product.
- Simplification using the following rule: 
![chap2-3](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap2-3.png?raw=true)
- DeMorgan's Law:
![chap2-4](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap2-4.png?raw=true)

## Chapter 3 Number and Arithmetic
### Basics
- For computer, everything is a number
- 1 bit in hexadecimal is 4 bit in binary; 1 bit in octal is 3 bit binary.
- Encoder: converting 2^N bits one hot to N bits binary
- Decoder: converting N bits binary to 2^N bits one hot
- With basic computation component: addition, substraction, bit-wise operation, shift, we have a ALU
### Addition and Substraction
#### Basic Idea
- Substraction is done by taking 2's complement of the substractor.
- 1's complement: flip every bit
- 2's complement: flip every bit then add 1
- Overflow occur when the computation result goes out of bound.
- If signed: carry out of the signed bit and carry out of the most-significant bit should be equal.
- If unsigned: there shouldn't be a carry out for the most significant bit.
#### Implementation
- Using basic building blocks of Full Adder, have 2 gate delays.
- Chain together to form Ripple Carry Adder to perform multiple bit addition
![chap3-1](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap3-1.png?raw=true)
- Use Carry Select Adder to cut off some gate delays, as a trade off, takes up more power memory.
![chap3-2](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap3-2.png?raw=true)
- To do substraction, add a control bit to determine whether to flip B.
![chap3-3](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap3-3.png?raw=true)
### Bit Shift
#### Basic Idea
- Left shift: moves left, brining in 0s at right, excess bits "fall off".
- Logical(Unsigned) Right shift: moves bits right, bringing in 0s at left, excess bits "fall off".
- <font color=red>Arithmetic(Signed) right shift: moves bits to right, Bringing in (sign bit) at left.</font>
![chap3-4](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap3-4.png?raw=true)

### Floating Point Numbers
- IEEE representation: 
![chap3-5](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap3-5.png?raw=true)
- Floats cannot hold all ints, doubles can represent all 32-bit ints but not all 64-bit ints.
- When representing 0, +/-0 is the same. Exponent is demoralized.
- Exponent 11111111 is not standard.

## Chapter 4 Storage
### Basic Idea
- We need some component to store values.
- Output of the circuit is a function of the input and a function of a stored value (state)
### SR latch
- Circuit and truth table:
![chap4-1](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap4-1.png?raw=true)
- When S and R are set at once, the output is undetermined.
- It has a bad interface.
### D latch
- Circuit and truth table:
![chap4-2](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap4-2.png?raw=true)
- This is level triggered, could mass up the data in later steps unintentionally.
### D Flip Flop
- Circuit and way of function:
![chap4-3](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap4-3.png?raw=true)
- Still have to ensure signals reach DFF before clk rises. (solved by synthesis tool like quartus to make timing)
- Could do both rising and falling edge trigger
- To fix timing misses: 
![chap4-4](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap4-4.png?raw=true)
### Register
- Using DFF as basic component
- Use a decoder on the input side to convert the read signal into a one-hot control bit to realize selected writing.
- Use a decoder at the output end and combine it with a tristate buffer(can produce Z high impedance) to realize reading.
## Chapter5 Finite State Machine
- Input combined with current state produce output and new state.
### State Diagram
- Circles for states, arrows fro transitions (Input).
### Transition Function
- Is the function of next state with respect to the input and current state.
- Could use counter to represent similar states.
### Output Function
- Compute as function of inputs and state.
### Mealy Machine and Moore Machine
- Mealy machine is a finite-state machine whose output values are determined both by its current state and the current inputs.
![chap5-1](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap5-1.png?raw=true)
- Moore machine, whose output values are determined solely by its current state.
![chap5-2](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap5-2.png?raw=true)
- For both of them, excitation table is the relation between current and next state with input.
![chap5-3](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap5-3.png?raw=true)
## Chapter 6 ISAs and MIPS(a form of ISAs)
### Basic Idea
- Assembly language is a very low level language but is still not machine language.
- Register store data to be used by the program.
- Instruction it self is also numbers and are translated from assembly language into its binary form by the compiler.
- Instruction opcode, location of operands and result, data type and size, what instruction comes next should be specified by it.
### ISA(Instruction Set Architecture)
- It set the contract between hardware and software.
- specifies instruction encoding, memory endian-ness and so on.
#### CISC
- Comes first, people directly wrote assembly.
- Variable length instruction encoding (sometimes quite complex)
- Many addressing modes, some quite complex
- Side-effecting and/or complex instructions
- Few registers (e.g., 8)
- Various operand models
- Can operate directly on memory
- Addressing mode:
![chap6-1](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap6-1.png?raw=true)
#### RISC
- Write in high level, let complier to compile and optimize.
- Simple, fixed length instruction encoding
- Few memory addressing modes
- Instructions have one effect
- “Many” registers (e.g., 32)
- Three-operand arithmetic (dest = src1 op src2)
- Load-store ISA: have specific instructions to access memory rather than using memory operands.
- Addressing mode:
![chap6-2](https://github.com/X-mei/ECE550-Review-Pic/blob/main/chap6-2.png?raw=true)
