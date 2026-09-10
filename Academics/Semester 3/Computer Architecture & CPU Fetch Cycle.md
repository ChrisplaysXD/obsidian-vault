---
title: Computer Architecture & The CPU Instruction Cycle
created: 2026-09-09
tags:
  - academic
  - semester-3
  - computer-organization
  - cpu
  - hardware
aliases:
  - CPU Fetch Cycle
  - Computer Organization
type: lecture-note
status: complete
---

# Computer Architecture & The CPU Instruction Cycle

An architectural overview of central processing unit (CPU) subsystems, register pipelines, and the continuous instruction execution lifecycle.

> [!abstract] Core Function
> The primary role of the CPU is to sequentially retrieve binary instructions from system memory, decode their operational intent, and orchestrate execution across internal arithmetic and register pathways.

---

## 1. Primary Hardware Components

```mermaid
graph LR
    Input[Input Devices: Keyboard, Mouse] --> CPU[Central Processing Unit]
    CPU <--> Memory[System RAM]
    CPU --> Output[Output Devices: Monitor, Storage]
```

- **Control Unit (CU)**: Decodes instructions and generates control bus timing signals.
- **Arithmetic Logic Unit (ALU)**: Executes integer math and bitwise logical operations.
- **Registers**: Ultra-low-latency on-die memory storage locations.
  - **Program Counter (PC)**: Stores the memory address of the next instruction awaiting execution.
  - **Instruction Register (IR)**: Latches the fetched instruction op-code and operand while decoding occurs.
  - **Memory Address Register (MAR) / Memory Buffer Register (MBR)**: Interfaces directly with the system address and data buses.

---

## 2. The Instruction Execution Pipeline (Fetch-Decode-Execute)

```mermaid
sequenceDiagram
    autonumber
    participant RAM as System RAM
    participant PC as Program Counter
    participant IR as Instruction Register
    participant ALU as Control Unit / ALU

    PC->>RAM: Assert instruction address via Address Bus
    RAM->>IR: Transfer instruction word via Data Bus
    PC->>PC: Increment Program Counter (PC = PC + 1 word)
    IR->>ALU: Decode Op-Code & fetch operands
    ALU->>ALU: Execute arithmetic/logic operation
```

### Detailed Operational Phases
1. **Fetch**: The control unit transfers the address in the Program Counter (PC) to the address bus. System RAM returns the instruction byte to the data bus, latching it into the Instruction Register (IR). Immediately upon retrieval, the processor increments the PC to index the consecutive instruction address.
2. **Decode**: The decoder logic inside the Control Unit evaluates the instruction bit-pattern, determining the required machine operation, addressing mode, and target register operands.
3. **Execute**: The ALU executes the operation (e.g., adding registers, asserting branch jumps, or reading/writing cache memory).
4. **Store / Write-Back**: The computation result is committed to internal general-purpose registers or main memory.

---

## Related Notes
- [[Academic MOC]]
- [[Data Structures & Algorithms - Fundamentals]]
- [[Hardware Security Keys - FIDO2 & WebAuthn]]
