---
course: CSC 2106 - Computer Organization and Architecture
lecture: 1
topic: Microcomputer Systems
tags:
  - csc2106
  - COA
---

# Lecture 1 — Microcomputer Systems (Exam Prep)

> [!info] Scope
> Based on Lecture 1 slides only. Every topic from the PDF is covered below. ⭐ = high-yield exam topic.

**Lecture outline (know these 4 threads — questions map to them):**
1. Architecture of microcomputers and the IBM PC
2. Peripherals and their relation to software/programs
3. What the computer does while executing instructions
4. Advantages & disadvantages of assembly language programming

---

## 1. Components of a Microcomputer System ⭐

### Summary
- **System unit** — the main box housing the internal electronics.
- **I/O devices (peripherals)** — keyboard, display unit, disk drives.
- **Integrated Circuit (IC)** — contains transistors; digital circuits that work in binary.
- **Bit (binary digit)** — smallest unit, value 0 or 1.
- **CPU** — the "brain"; controls all operations; a single-chip processor = **microprocessor**.
- **Memory circuits** — store information.
- **I/O circuits** — communicate with I/O devices.

> [!warning] Common Mistakes
> - Confusing **microprocessor** (single chip CPU) with **microcomputer** (the whole system).
> - Forgetting that the CPU is *one* component — memory and I/O circuits are separate.
> - Thinking a bit can hold more than 0/1.

> [!question] How It May Come in the Exam
> - MCQ: "Which component is called the brain of the computer?" → **CPU (microprocessor)**
> - "List the main components of a microcomputer system."
> - "A bit can have how many values?" → **2 (0 or 1)**

> [!success] Model Answer (list question)
> A microcomputer system consists of: (1) the system unit, (2) I/O devices/peripherals such as keyboard, display, and disk drives, and (3) integrated circuits (ICs) inside the system unit — namely the CPU (microprocessor), memory circuits, and I/O circuits.

---

## 2. The System Board (Motherboard)

### Summary
- Resides inside the **system unit**.
- Contains the **microprocessor and memory circuits**.
- Has **expansion slots** to connect additional circuit boards called **add-in cards / add-in boards**.
- **I/O circuits are located on add-in cards.**

> [!warning] Common Mistakes
> - Saying I/O circuits sit directly on the motherboard — per the slides, they are on **add-in cards** plugged into expansion slots.
> - Mixing up "expansion slot" (the connector) with "add-in card" (the board you plug in).

> [!question] How It May Come
> - "What is the purpose of expansion slots?" → to connect add-in cards/boards.
> - True/False: "I/O circuits are located in add-in cards." → **True**

---

## 3. Memory: Bytes and Words ⭐

### Summary
- A memory circuit element stores **one bit** (0 or 1).
- Memory is organized in groups of **8 bits = 1 byte**.
- Each memory byte has an **address** — like the street address of a house.
- **Word = 2 bytes** (in this microcomputer/IBM PC context).
- To store a word, the IBM PC needs **a pair of successive memory bytes**.
- The **lower address** of the two bytes is the word's address.
  - Example: a word at address 2 = bytes 2 and 3.
- The microprocessor can tell from the address whether to read a byte or a word.

> [!warning] Common Mistakes
> - Writing "1 byte = 16 bits" — it's **8 bits**; a **word** is 16 bits (2 bytes).
> - Thinking a word's address is the higher byte — it's the **lower** address.
> - Assuming "word" size is universal — here it is defined as 2 bytes for the IBM PC.

> [!question] How It May Come
> - "How many bits in a byte / word?" → 8 / 16.
> - "A word stored at address 6 uses which bytes?" → **6 and 7** (lower address = word address).

---

## 4. Address vs Contents ⭐⭐ (classic exam trap)

### Summary
| Property | Address | Contents |
|---|---|---|
| What it is | Identifier/location of a memory byte | The data stored in that byte |
| Uniqueness | **Fixed and unique** (no two bytes share an address) | **NOT unique** (same data can appear in many bytes) |
| Size | Number of bits **depends on the processor** | **Always 8 bits** (1 byte) |
| Examples | Intel 8086 → **20-bit** address; Intel 80286 → **24-bit** address | Any 8-bit pattern |

> [!warning] Common Mistakes
> - Saying contents are unique — they are **not**; addresses are.
> - Saying address size is fixed for all machines — it **depends on the processor**.
> - Saying contents size depends on the processor — contents of a memory byte are **always 8 bits**.
> - Mixing up 8086 (20-bit) with 80286 (24-bit).

> [!question] How It May Come
> - "Differentiate between address and contents." (short answer — use the table)
> - MCQ: "The contents of a memory byte are always ___ bits." → **8**
> - "Intel 8086 uses how many bits for an address?" → **20**

---

## 5. Memory Byte Addressing — the 2ⁿ Calculation ⭐⭐

### Summary
- A bit has 2 possible values → an *n*-bit address can address **2ⁿ** bytes.
- Example from slides: 20-bit address → 2²⁰ = **1,048,576 bytes = 1 MB**.
- In computer terminology, **2²⁰ = 1 Mega** (not 1,000,000!).

> [!warning] Common Mistakes
> - Writing 2²⁰ = 1,000,000 — it is **1,048,576**.
> - Forgetting to state the unit (bytes) in the answer.
> - Arithmetic slips with exponents — remember the anchor values: 2¹⁰ = 1K = 1,024; 2²⁰ = 1M = 1,048,576.

> [!question] How It May Come
> - "A processor uses 20 bits for an address. How many memory bytes can it address?" (exactly the slide example)
> - Variation: "A processor uses a 24-bit address — how many bytes?" → 2²⁴ = 16,777,216 bytes = 16 MB.

> [!success] Model Answer
> Each bit can be 0 or 1, so an n-bit address has 2ⁿ combinations. With 20 bits: 2²⁰ = 1,048,576 bytes. Since 2²⁰ = 1 Mega in computer terminology, the processor can address **1 MB** of memory.

---

## 6. Bit Positions in a Byte and Word ⭐

### Summary
- Bit positions are numbered **right to left** (bit 0 = rightmost).
- **Bits 0–7 = low byte** → stored at the **lower address** of the word.
- **Bits 8–15 = high byte** → stored at the **higher address** of the word.

> [!warning] Common Mistakes
> - Numbering bits left to right — always **right to left**, starting at **bit 0** (not bit 1).
> - Swapping low/high byte with the addresses: low byte → **lower** address; high byte → **higher** address.

> [!question] How It May Come
> - MCQ: "Which bits form the low byte of a word?" → **bits 0–7**
> - "Bit positions are numbered from ___ to ___." → right to left.

---

## 7. Memory Operations (Read vs Write) ⭐⭐

### Summary
The processor performs exactly **two** operations on memory:
1. **Read / Fetch** — processor gets a **copy** of the data; the **original contents are unchanged** (non-destructive).
2. **Write / Store** — new data becomes the contents; the **previous contents are lost** (destructive).

> [!warning] Common Mistakes
> - Thinking reading erases the data — it does **not**; reading copies.
> - Thinking old data survives a write — it is **lost/overwritten**.
> - Swapping the terms: read = fetch, write = store.

> [!question] How It May Come
> - True/False: "Reading a memory location destroys its contents." → **False**
> - "Which memory operation is destructive and why?" → Write, because the previous contents are lost.

---

## 8. RAM vs ROM ⭐⭐

### Summary
| | RAM (Random Access Memory) | ROM (Read Only Memory) |
|---|---|---|
| Access | Can be **read and written** | **Read only** — once initialized, can't be changed |
| Volatility | **Volatile** — contents lost when power is off | **Non-volatile** — retains values without power |
| Holds | Program instructions and data | Start-up programs |
| Special term | — | ROM-based programs = **firmware** |

> [!warning] Common Mistakes
> - Forgetting the keyword **firmware** for ROM-based programs — examiners love this term.
> - Saying RAM keeps data after power-off — it doesn't (volatile).
> - Saying ROM can be written to — per these slides, no.

> [!question] How It May Come
> - "Differentiate RAM and ROM." (very common short answer — give 3–4 points from the table)
> - "What is firmware?" → Programs stored in ROM, responsible for loading start-up programs.

---

## 9. Buses ⭐⭐

### Summary
- The processor communicates with memory and I/O devices via **signals**, which travel along sets of wires called **buses**.
- **Three buses, matched to three signals:**
  - **Address bus** — CPU places the *address* of the memory location on it.
  - **Data bus** — CPU *receives the data* sent by memory circuits on it.
  - **Control bus** — CPU sends *control signals* (e.g., the read command) on it.

> [!warning] Common Mistakes
> - Swapping which signal goes on which bus (memorize: Address→Address bus, Data→Data bus, Control→Control bus).
> - Saying the CPU *sends* data on the data bus during a read — during a read it **receives**.
> - Forgetting the control bus carries the read/write command itself.

> [!question] How It May Come
> - "Name the three types of buses and state the function of each." (standard short answer)
> - Trace a read operation: address placed on address bus → control signal on control bus → data returns on data bus.

---

## 10. CPU, Machine Language & Instruction Set

### Summary
- CPU controls the computer by **executing programs** (system or application).
- Each instruction the CPU executes is a **bit string**.
- **Machine language** = the language of 0s and 1s.
  - Instructions are designed to be **simple** — sequences of very basic operations.
- **Instruction set** = the complete set of instructions a CPU can perform.
  - ⭐ **The instruction set is unique for each CPU.**

> [!warning] Common Mistakes
> - Assuming instruction sets are interchangeable between different CPUs — they are **unique per CPU**.
> - Defining machine language vaguely — say "the language of 0s and 1s / bit strings."

> [!question] How It May Come
> - "What is an instruction set?" → The set of all instructions a CPU can execute; unique to each CPU.
> - "What is machine language?" → Bit strings of 0s and 1s that the CPU executes directly.

---

## 11. Intel 8086 Microprocessor Organization ⭐⭐⭐ (most detailed slide — expect a question)

### Summary
The 8086 has **two units**:

**Execution Unit (EU)**
- Contains the **ALU** → performs **arithmetic and logical operations**.
- Data for operations is stored in **registers**.
- A register is like a memory location, but referred to **by name, not by number**.
- EU registers: **AX, BX, CX, DX, SI, DI, SP, BP**
- Also has **temporary registers** (hold operands for the ALU) and the **FLAGS register**.
- **FLAGS register**: individual bits reflect the **result of a computation**.

**Bus Interface Unit (BIU)**
- Enables **communication between the EU and memory / I/O circuits**.
- Primarily responsible for transmitting **address, data, and control signals** on the buses.
- BIU registers: **CS, DS, ES, IP** — these **hold addresses** of memory locations.

**How EU & BIU work together**
- Connected by an **internal bus**; they work in parallel.
- While the EU executes an instruction, the BIU **fetches up to 6 bytes** of the next instruction(s) into the **instruction queue (IQ)**.
- This is called **instruction prefetch** — its purpose is to **speed up the processor**.
- If the EU needs to communicate with memory, the BIU **suspends prefetch** and performs the required operation.

> [!warning] Common Mistakes
> - **Register mix-up** (the #1 trap): AX/BX/CX/DX/SI/DI/SP/BP belong to the **EU**; CS/DS/ES/IP belong to the **BIU**. Expect an MCQ exactly on this.
> - Saying the ALU is in the BIU — it's in the **EU**.
> - Saying FLAGS holds data — its bits reflect the **result/status** of computation.
> - Writing "prefetch fetches 6 instructions" — it's **up to 6 bytes**, into the **instruction queue**.
> - Forgetting the purpose of prefetch: to **speed up** the processor.

> [!question] How It May Come
> - "Describe the internal organization of the Intel 8086." (long answer — EU + BIU + prefetch)
> - MCQ: "Which of the following is a BIU register?" → CS / DS / ES / IP.
> - "What is instruction prefetch and why is it used?" → BIU fetches up to 6 bytes of upcoming instructions into the instruction queue while EU executes; speeds up the processor.
> - "What happens to prefetch when the EU needs memory?" → BIU suspends prefetch.

> [!success] Model Answer (long answer skeleton)
> The 8086 is divided into two units. The **Execution Unit (EU)** contains the ALU (arithmetic/logic), registers AX, BX, CX, DX, SI, DI, SP, BP, temporary registers, and the FLAGS register whose bits reflect computation results. The **Bus Interface Unit (BIU)** handles communication with memory and I/O via the address, data, and control buses, using registers CS, DS, ES, and IP which hold memory addresses. The two units work in parallel: while the EU executes, the BIU prefetches up to 6 bytes of the next instruction into the instruction queue (instruction prefetch) to speed up processing; prefetch is suspended when the EU needs memory access.

---

## 12. I/O Ports — Serial vs Parallel ⭐

### Summary
- **I/O ports** are the **transfer points** between the CPU and I/O devices; devices connect through them.

| | Serial port | Parallel port |
|---|---|---|
| Transfer | **1 bit at a time** | **8 or 16 bits at a time** |
| Speed | Slower | Faster |
| Wiring | Fewer connections | **Requires more wiring** |
| Used for | **Slow devices** (e.g., keyboard) | **Fast devices** (e.g., disk drive) |

> [!warning] Common Mistakes
> - Swapping the bit counts: serial = **1 bit**, parallel = **8 or 16 bits** at a time.
> - Saying the disk drive connects to the serial port — fast devices → **parallel**; keyboard (slow) → **serial**.
> - Forgetting the trade-off: parallel is faster but needs **more wiring**.

> [!question] How It May Come
> - "Differentiate serial and parallel ports." (table question)
> - MCQ: "A keyboard is typically connected to a ___ port." → serial.

---

## 13. Instruction Execution & the Fetch–Execute Cycle ⭐⭐⭐

### Summary
- A machine-language instruction has **two parts**:
  - **Opcode** — the *type of operation* to perform.
  - **Operands** — the *data* to be operated on (**memory addresses are used**).
- **Fetch–execute cycle:**
  1. **Fetch** an instruction from memory.
  2. **Decode** the instruction to determine the operation.
  3. **Fetch data** from memory if necessary.
  4. **Execute**: perform the operation on the data.
  5. **Store the result** if needed.

> [!warning] Common Mistakes
> - Swapping opcode and operand — opcode = *what to do*, operand = *what to do it to*.
> - Missing the **decode** step when listing the cycle.
> - Saying operands are always raw data — per slides, **memory addresses** are used to locate data.

> [!question] How It May Come
> - "What are the two parts of a machine instruction?" → opcode and operands.
> - "Describe the fetch–execute cycle." (very likely short/long answer — list the 5 steps in order)

---

## 14. Timing — Clock Period & Clock Rate ⭐⭐ (calculation topic)

### Summary
- A **clock circuit** generates a train of **clock pulses** so execution steps happen in an orderly fashion.
- **Clock period** = the *time interval between two pulses*.
- **Clock rate/speed** = the *number of pulses per second*, measured in **MHz/GHz**.
- **1 MHz = 1,000,000 (1 million) pulses per second.**

**Slide's worked example:** a 2.3 GHz processor →
2.3 × 1,000,000,000 = **2,300,000,000 pulses per second** (2.3 × 10⁹).

> [!warning] Common Mistakes
> - Confusing clock **period** (time between pulses) with clock **rate** (pulses per second) — they are inverses of each other.
> - Unit errors: GHz = 10⁹ pulses/sec, MHz = 10⁶. A common exam variation uses MHz (e.g., 4 MHz → 4 × 10⁶).
> - Miscounting zeros — write it in scientific notation to be safe.

> [!question] How It May Come
> - "A computer has a 2.3 GHz processor. How many pulses are generated per second?" (straight from the slide — memorize the method)
> - "Define clock period and clock rate."

> [!success] Model Answer
> Clock rate is the number of pulses per second. 1 GHz = 10⁹ pulses/second, so a 2.3 GHz processor generates 2.3 × 10⁹ = 2,300,000,000 pulses per second.

---

## 15. Programming Languages — Machine vs Assembly vs High-Level ⭐⭐

### Summary
| | Machine language | Assembly language | High-level language |
|---|---|---|---|
| Form | Bit strings (0s and 1s) | **Symbolic names** for operations, registers, memory locations (e.g., `MOV AX, A`) | More **natural-language** text |
| Translator needed | None (executed directly) | **Assembler** | **Compiler** |

> [!warning] Common Mistakes
> - **Assembler vs Compiler swap** (guaranteed trap): assembly → **assembler**; high-level → **compiler**.
> - Thinking assembly runs directly on the CPU — it must first be translated into machine language.

> [!question] How It May Come
> - "Which translator converts assembly language to machine language?" → assembler.
> - "Which translator converts a high-level language?" → compiler.
> - "Give an example of an assembly instruction." → `MOV AX, A`.

---

## 16. Advantages: High-Level vs Assembly ⭐⭐⭐ (explicitly in the lecture outline — expect it)

### Summary
| High-level language — advantages | Assembly language — advantages |
|---|---|
| Closer to natural language → easier to convert algorithms | Very close to machine language → programs are **faster and shorter** |
| Fewer instructions and less time needed than assembly | Easy to read/write **specific memory locations and I/O ports** |
| **Portable** — programs can run on any machine | Can be used as a **subprogram** of a high-level language |
| | Gives deeper understanding — "how the computer thinks" |

> [!warning] Common Mistakes
> - Saying assembly is portable — it's the **high-level** language that runs on any machine; assembly is machine-specific.
> - Saying high-level programs are faster — **assembly** programs are faster and shorter.
> - Only listing one side — the question usually asks to *compare*, so give both columns.

> [!question] How It May Come
> - "Discuss the advantages and disadvantages of assembly language programming compared to high-level languages." (matches outline point 4 — highest-probability long question)
> - "Why would a programmer still use assembly language?" → speed, smaller size, direct hardware/memory/I/O access, deeper control.

> [!success] Model Answer (comparison skeleton)
> Assembly language programs are faster and shorter because they are very close to machine language; they allow easy access to specific memory locations and I/O ports, can be embedded as subprograms in high-level programs, and teach how the computer works internally. However, high-level languages are closer to natural language (easier algorithm conversion), require fewer instructions and less development time, and are portable across machines — whereas assembly is machine-specific and harder to write.

---

## ⚡ Rapid Revision Checklist (drill these the night before)

- [ ] 8 bits = 1 byte; 2 bytes = 1 word; word address = **lower** byte address
- [ ] Address = fixed & unique; contents = always 8 bits, **not** unique
- [ ] 8086 → 20-bit address → 2²⁰ = 1,048,576 bytes = **1 MB**; 80286 → 24-bit
- [ ] Bits numbered **right → left**; bits 0–7 low byte (lower address), 8–15 high byte (higher address)
- [ ] Read = copy, original **unchanged**; Write = previous contents **lost**
- [ ] RAM = volatile, read+write; ROM = non-volatile, read-only, holds **firmware**
- [ ] 3 buses: address / data / control — know who sends what during a read
- [ ] Instruction set is **unique per CPU**
- [ ] 8086: EU = ALU + AX/BX/CX/DX/SI/DI/SP/BP + FLAGS; BIU = CS/DS/ES/IP
- [ ] Prefetch: BIU grabs **up to 6 bytes** → instruction queue; purpose = **speed**; suspended when EU needs memory
- [ ] Serial = 1 bit, slow, keyboard; Parallel = 8/16 bits, fast, disk drive, more wiring
- [ ] Instruction = **opcode + operands**; fetch → decode → fetch data → execute → store
- [ ] Clock period vs clock rate; 1 MHz = 10⁶ pulses/s; 2.3 GHz = 2.3 × 10⁹ pulses/s
- [ ] Assembly → **assembler**; high-level → **compiler**
- [ ] Assembly = fast/short/hardware access; High-level = natural/easy/portable

## 📚 References (from the slides)
- Ytha Yu & Charles Marut, *Assembly Language Programming and Organization of the IBM PC*, McGraw Hill, 1992.
- Linda Null & Julia Lobur, *Essentials of Computer Organization and Architecture* (3rd ed.).
- W. Stallings, *Computer Organization and Architecture: Designing for Performance*, 6th ed., Prentice Hall of India, 2003.
- John P. Hayes, *Computer Organization and Architecture*.
