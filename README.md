# Intel 8086 Microprocessor Based System

## Project Overview
This project is a practical implementation of an Intel 8086 microprocessor-based system, designed to provide hands-on experience with microprocessor architecture, memory interfacing, and I/O control. The project consists of multiple experiments that gradually build a functional microcomputer using the Intel 8086 processor, essential supporting components, and assembly programming.

## Project Goals
- Understand the fundamental architecture and operation of the Intel 8086 microprocessor.
- Learn to design and implement a clock generator circuit.
- Develop skills in buffering and bus interfacing.
- Interface memory with the microprocessor to store and execute programs.
- Implement input and output operations using standard ICs and programmable peripheral interfaces.
- Write and execute assembly language programs on the microprocessor.

## Components Required
To build this project, the following components are required:
- **Intel 8086 Microprocessor** – The core processing unit.
- **Clock Generator (8284)** – Provides the necessary clock signal for the microprocessor.
- **EEPROM (AT28C16)** – Used to store program instructions.
- **Buffers and Latches** (74HCT573, 74LS245, 74LS138, 74LS244, 74LS374) – For stabilizing and managing data and address buses.
- **Power Supply (7805 Regulator)** – Supplies a steady 5V to the circuit.
- **Push Buttons and LEDs** – Used for input and output demonstration.
- **Breadboard and Jumper Wires** – For circuit assembly and prototyping.

## Experiments and Implementation
The project is divided into four main stages, each representing a core experiment:

### 1. Clock Generator Circuit
The first step in building an 8086-based microcomputer is generating a stable clock signal. The 8284 Clock Generator IC is used to generate a 1.3 MHz clock signal required for the Intel 8086 CPU.

**Implementation Steps:**
1. Assemble the clock circuit using the 8284 clock generator and a quartz crystal.
2. Power up the circuit and measure the generated clock signal using an oscilloscope.
3. Ensure the clock signal is stable before proceeding.

**Expected Outcome:**
The oscilloscope should display a stable periodic waveform with a frequency of approximately 1.3 MHz.

---

### 2. Intel 8086 Buffering & Address Bus Scanning
This experiment focuses on setting up address and data buses using buffering techniques to ensure proper communication between the CPU and peripheral components.

**Implementation Steps:**
1. Identify and classify the pins of the Intel 8086 CPU (Power, Address, Data, and Control).
2. Buffer the address and data lines using latch and buffer ICs.
3. Observe the address bus operation using an oscilloscope and a logic analyzer.

**Expected Outcome:**
- The address and data buses should be correctly latched and buffered.
- The signals should correspond to the execution cycle of the CPU.

---

### 3. Memory Interfacing with the 8086
In this experiment, a non-volatile EEPROM (AT28C16) is interfaced with the microprocessor to store and execute programs.

**Implementation Steps:**
1. Connect the EEPROM chips to the buffered address and data buses.
2. Write a simple assembly program and store it in the EEPROM.
3. Observe the CPU fetching instructions from memory.

**Sample Assembly Code:**
```assembly
ORG 0000H      ; Set start address
START:
    JMP START  ; Infinite loop
    HLT        ; Halt CPU (not reached)
END
```
**Expected Outcome:**
- The address bus should show repetitive addresses, confirming that the CPU is fetching and executing the looping instruction.

---

### 4. Input/Output (I/O) Interfacing
This experiment enables the microprocessor to interact with external devices such as LEDs and push buttons. Two approaches are used:

#### Approach 1: Using Buffers
- An **input port** is created using the 74LS244 unidirectional buffer.
- An **output port** is created using the 74LS374 latch.
- Push buttons are connected to the input port, and LEDs to the output port.

**Sample Assembly Code:**
```assembly
ORG 0000H
START:
    IN AL, 00H   ; Read from input port
    OUT 00H, AL  ; Output to LED port
    JMP START    ; Repeat
END
```
**Expected Outcome:**
Pressing a button should turn ON the corresponding LED.

#### Approach 2: Using the 82C55 PPI
Instead of individual buffers, a **Programmable Peripheral Interface (PPI)** is used for more flexibility.

**Sample Assembly Code:**
```assembly
MOV AL, 90H     ; Configure PPI (PORTA input, PORTB output)
OUT 03H, AL     ; Send configuration to PPI control register
START:
    IN AL, 00H   ; Read input from PORTA (push buttons)
    OUT 01H, AL  ; Output to PORTB (LEDs)
    JMP START    ; Loop continuously
END
```
**Expected Outcome:**
The LEDs will mirror the button presses, demonstrating successful data transfer between I/O devices and the microprocessor.

---

## Conclusion
This project serves as a hands-on implementation of a basic Intel 8086 microcomputer. It covers fundamental concepts such as:
- Clock signal generation.
- Address and data bus buffering.
- Memory interfacing and instruction execution.
- Input and output handling using buffers and programmable interfaces.

By completing this project, one gains practical experience in microprocessor system design, making it an essential learning experience for embedded systems and computer engineering enthusiasts.

## References
- Intel 8086 Datasheet
- 8284 Clock Generator Datasheet
- AT28C16 EEPROM Datasheet
- 82C55 PPI Datasheet

