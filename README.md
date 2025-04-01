# UART-Communication-Protocol-

## Overview
This project implements a Universal Asynchronous Receiver-Transmitter (UART) in Verilog, with functional verification using SystemVerilog. The design includes a transmitter, a receiver, a finite state machine (FSM), a baud rate generator, and shift registers for serial-to-parallel and parallel-to-serial conversion.

## Features
- UART Transmitter and Receiver
- Baud Rate Generator
- FSM-based control logic
- Parallel-In Serial-Out (PISO) and Serial-In Parallel-Out (SIPO) shift registers
- Fully functional and verified using SystemVerilog

---

## UART Protocol Basics
UART is a widely used asynchronous serial communication protocol that transmits data one bit at a time over a single wire. It consists of two main components:
1. **Transmitter**: Converts parallel data into a serial stream and transmits it over the communication channel.
2. **Receiver**: Receives the serial data, reconstructs the original parallel data, and provides it to the receiving system.

### UART Frame Format
Each UART frame consists of:
- **Start Bit (1-bit)**: Indicates the beginning of data transmission (always 0).
- **Data Bits (5-8 bits)**: The actual payload being transmitted.
- **Parity Bit (optional)**: Used for error detection.
- **Stop Bit(s) (1-2 bits)**: Indicates the end of transmission (always 1).

## Design Details
### Block Diagram:

![]()

### 1. UART Transmitter (`uart_tx.v`)
The transmitter is responsible for sending data serially. It consists of the following key components:
- **FSM Controller**: Handles the different transmission states (Idle, Start, Data, Parity, Stop)
- **Shift Register (PISO)**: Converts parallel data into a serial bitstream
- **Baud Rate Synchronization**: Ensures proper timing for sending each bit

#### **Transmitter FSM States**
1. **IDLE**: Waits for a new data input
2. **START**: Sends the start bit
3. **DATA**: Serially transmits 8-bit data
4. **PARITY (Optional)**: Sends the parity bit if enabled
5. **STOP**: Sends stop bits before going back to IDLE


### 2. UART Receiver (`uart_rx.v`)
The receiver reconstructs parallel data from the serial input. It consists of:
- **FSM Controller**: Handles the receive states (Idle, Start Detect, Data, Parity Check, Stop)
- **Shift Register (SIPO)**: Converts incoming serial bits into parallel data
- **Baud Rate Synchronization**: Ensures correct sampling of bits

#### **Receiver FSM States**
1. **IDLE**: Waits for the start bit
2. **START DETECT**: Detects the start bit and synchronizes
3. **DATA RECEIVE**: Receives 8-bit data serially
4. **PARITY CHECK (Optional)**: Verifies the received data using parity
5. **STOP CHECK**: Ensures proper stop bit reception

### 3. Baud Rate Generator (`baud_generator.v`)
The baud rate generator ensures the correct timing for UART transmission and reception. It generates clock enable signals to ensure synchronization.

---

## Simulation and Verification
The design has been verified using a SystemVerilog testbench (`uart_tb.sv`). The testbench performs:
- Transmission and reception of data
- Verification of correct start, stop, and parity bits
- Checking error handling mechanisms
