# 8086 Microprocessor — Midterm Study Notes

_Lecture 3 · Week 3 · Computer Organization & Architecture (Course 0052)_

> [!tip] How this lecture tends to get tested Two very different question styles come from this slide deck:
> 
> 1. **Recall/comparison questions** — "differentiate 8086 vs 8088," "what does BX do," etc. Pure memorization, low risk once reviewed once or twice.
> 2. **Hex calculation questions** — converting between segment:offset and physical address. This is where marks are actually lost, because it's not about memorizing a fact, it's about _not making an arithmetic slip under time pressure_. Section 3.3 below is the highest-value section in this whole note — drill it.

---

## 1. The 8086 Family of Microprocessors

> [!important] Core concept All classic IBM-compatible PCs were built around one chip family. Knowing _which chip powered which machine_ is a classic one-liner exam question.

|Machine|Chip|
|---|---|
|IBM PC|8088|
|PC XT|8088|
|PC AT|80286|
|PS/1|80286|
|PS/2|8086 / 80286 / 80386 / 80486|
|PC-compatible laptops|80186|

### 1.1 8086 vs 8088

|8086|8088|
|---|---|
|First 16-bit microprocessor (1978)|Internally identical to 8086|
|**16-bit** external data bus|**8-bit** external data bus|
|Faster clock rate → better performance|Cheaper to build a computer around → used in the original IBM PC|
|Same instruction set as 8088|Same instruction set as 8086|

> [!warning] Common mistake Students mix up _internal_ vs _external_ bus width. Both chips process data 16 bits at a time **internally** — the difference is only the **external data bus** (how many bits move to/from memory per cycle). If a question says "8088 is a 16-bit processor," the correct nuance is: internally yes, externally it only moves 8 bits at a time to the outside world.

> [!question] Likely exam phrasing "Why was the 8088, not the 8086, chosen for the original IBM PC?" **Answer:** Because its 8-bit external data bus made it cheaper to build supporting circuitry around, even though the 8086 had better raw performance.

### 1.2 80186 vs 80188

|80186|80188|
|---|---|
|Enhanced version of **8086**|Enhanced version of **8088**|
|Adds support chips + some extended instructions|Adds support chips + some extended instructions|

> [!warning] Common mistake Assuming 80186/80188 were a big leap forward. The slide is explicit: **"no significant advantage over the 8086 and 8088"** — they were overshadowed almost immediately by the 80286. If asked "why didn't the 80186 become popular," this is the answer.

### 1.3 The 80286

- 16-bit, introduced **1982**, faster than 8086 (**12.5 MHz vs 10 MHz**)
- **Two operating modes** — a very common short-answer question:

|Real Address Mode|Protected Virtual Address Mode|
|---|---|
|Behaves exactly like an 8086|Enables **multitasking** — several tasks at once|
|Old 8086 programs run unmodified|**Memory protection** — one program's memory can't be corrupted by another|
|—|Addresses **16 MB** of physical memory (vs 1 MB on 8086/8088)|
|—|**Virtual memory** — treats disk as memory, can run programs up to 1 GB (2³⁰ bytes)|

> [!question] Likely exam phrasing "List the two modes of the 80286 and one feature unique to each." **Answer:** Real mode = 8086-compatible execution. Protected mode = multitasking + memory protection + 16MB addressing + virtual memory.

### 1.4 80386 / 80386SX

- **First 32-bit** microprocessor, introduced **1985**
- 32-bit data path, up to **33 MHz**, fewer clock cycles per instruction than 80286
- Also has real & protected modes; in protected mode it can **emulate the 80286**
- Adds a **virtual 8086 mode** — runs multiple 8086 apps simultaneously _under_ memory protection
- Protected mode addresses **4 GB physical / 64 TB virtual** memory
- **80386SX** = same internal structure, but only a **16-bit** external data bus (cost-reduced version — same pattern as 8086/8088!)

> [!warning] Common mistake Confusing "virtual 8086 mode" (386-specific: run _multiple_ 8086 programs safely) with plain "real mode" (386 acting like a _single_ 8086). They are different features — real mode is inherited from the 286, virtual 8086 mode is new to the 386.

### 1.5 80486 / 80486SX

- 32-bit, introduced **1989**, fastest/most powerful in this family
- Incorporates all 386 functions **plus**:
    - Built-in **numeric (floating-point) processor**, equivalent to an 80387
    - **8-KB cache memory** to buffer data from slower main memory
- Roughly **3× faster** than the 386 at the same clock speed
- **80486SX** = same core, but **no floating-point processor**

> [!question] Pattern to notice across the whole family Every "SX" or budget variant (8088, 80386SX, 80486SX) removes something _external or auxiliary_ (bus width or FPU) to cut cost, while keeping the same internal core. If you see an unfamiliar "SX" chip on the exam, apply this pattern.

---

## 2. Architecture of the 8086 — Register Overview

> [!important] Core concept The 8086 has **14 registers, all 16-bit**, split into 4 functional groups:

|Group|Registers|Purpose|
|---|---|---|
|**General registers**|AX, BX, CX, DX|Hold data for operations|
|**Segment registers**|CS, DS, SS, ES|Hold segment numbers (addresses)|
|**Pointer/Index registers**|SP, BP, SI, DI, IP|Hold offset addresses|
|**Status register**|FLAGS|Current processor status|

> [!tip] Reassurance from the slide itself The lecturer explicitly says you don't need to memorize the register layout diagram — familiarity comes with practice. Focus your memorization effort on **what each register is _for_** (Section 3), not on redrawing the diagram.

Also remember the 3-way register classification by **function**:

- **Data register** — holds data for an operation
- **Address register** — holds an address (instruction or data)
- **Status register** — holds current processor status

---

## 3. Registers and Their Special Functions

### 3.1 General Purpose Registers (AX, BX, CX, DX)

Each is 16-bit and splits into two 8-bit halves (e.g., AX → AH + AL).

|Register|Full name|Special function(s)|
|---|---|---|
|**AX**|Accumulator|Generates the _shortest machine code_ → preferred for arithmetic/logic/data-transfer. **Multiplication & division** always involve AX or AL. **I/O** operations require AL or AX.|
|**BX**|Base|Address register — used in **table look-up** (`XLAT` instruction)|
|**CX**|Counter|**Loop counter**; controls string operations via **REP** (repeat) prefix; **CL** specifically holds the count for bit shift/rotate instructions|
|**DX**|Data|Used alongside AX in **multiplication/division**; also used in **I/O operations**|

> [!question] Verbatim slide prompt — very likely to reappear **"List one special function of AX, BX, CX, and DX."** **Model answer:**
> 
> - AX — required operand register for multiplication/division, and for I/O
> - BX — used for table look-up (XLAT)
> - CX — loop/string-repeat counter (CL = shift/rotate count)
> - DX — paired with AX in multiply/divide; used in I/O operations

> [!warning] Common mistake Students often say "AX is just for adding numbers." The exam-worthy detail is _why_ AX is preferred (shortest machine code) and the **specific mandatory role** in multiply/divide and I/O — that specificity is what earns marks, not a vague description.

### 3.2 Segment Registers (CS, DS, SS, ES)

> [!important] Core concept — why segments exist at all The 8086 has a **20-bit physical address bus** → can address **2²⁰ = 1 MB** of memory. But its registers are only **16-bit**. Segmentation is the trick used to fit a 20-bit address into 16-bit registers.

- A **segment** = a block of **64 KB (2¹⁶)** of consecutive memory
- Each segment has a **16-bit segment number** (0000h–FFFFh)
- Inside a segment, a location is given by its **offset** (also 16-bit: 0000h–FFFFh)
- Written as **segment:offset** — called a **logical address**
    - Example: `A4FB:4872h` = offset 4872h within segment A4FBh

|Segment register|Holds address of|
|---|---|
|**CS**|Code Segment — instructions|
|**DS**|Data Segment — program data|
|**SS**|Stack Segment — the stack|
|**ES**|Extra Segment — second data segment (commonly used as destination in string ops)|

> [!warning] Common mistake Only **4 segments are active at any given time** (one per segment register), even though a program can _reference_ more by changing register contents. Don't say "the 8086 can only use 4 segments total" — it's 4 **active at once**, out of many possible.

### 3.3 ⭐ The Big One: Segment:Offset ↔ Physical Address (calculation questions)

> [!important] The formula — memorize this cold **Physical Address = (Segment × 10h) + Offset** In practice: **shift the segment left by one hex digit (append a 0)**, then add the offset.

Rearranged forms you'll also need:

- **Offset = Physical Address − (Segment × 10h)**
- **Segment = (Physical Address − Offset) ÷ 10h**

> [!warning] Where marks are actually lost
> 
> - Forgetting to **pad the segment with a trailing 0** before adding (i.e. adding the offset to the _unshifted_ segment number)
> - Simple **hex addition/subtraction slips** (borrowing/carrying in base 16 instead of base 10)
> - Mixing up which formula to use — always ask "am I solving for physical, offset, or segment?" before starting

#### Key vocabulary (easy free marks if asked to define)

- **Logical address** — the segment:offset pair as written (e.g. `A4FB:4872h`)
- **Physical address** — the actual single 20-bit address in memory
- **Paragraph** — 16 bytes (a segment always starts on a paragraph boundary)
- **Paragraph boundary** — any address divisible by 16 (i.e., ends in hex `0`)

> [!question] "What is the highest possible 20-bit physical address?" 20 bits → 2²⁰ = 1,048,576 addresses, numbered 0 to 1,048,575. **Answer: `FFFFFh`**

#### Worked example — segment:offset → physical address

**Given:** `ABC4:12BAh`

```
Segment ABC4h × 10h = ABC40h
Offset             =  12BAh
                    --------
Physical address   = ACEFAh
```

**Answer: `ACEFAh`**

#### Worked example — physical address of `0A51:CD90h`

```
Segment 0A51h × 10h = 0A510h
Offset              =  CD90h
                     --------
Physical address    = 172A0h
```

**Answer: `172A0h`**

#### Worked example — find the offset

**Given:** physical address `4A37Bh`, segment `40FFh`

```
Offset = Physical − (Segment × 10h)
       = 4A37Bh − 40FF0h
       = 938Bh
```

**Answer: `938Bh`**

#### Worked example — find the segment

**Given:** physical address `4A37Bh` (continuing the same problem set), offset `123Bh`

```
Segment = (Physical − Offset) ÷ 10h
        = (4A37Bh − 123Bh) ÷ 10h
        = 49140h ÷ 10h
        = 4914h
```

**Answer: `4914h`** _(Check: 4914h × 10h + 123Bh = 49140h + 123Bh = 4A37Bh ✓)_

> [!question] How this question is usually phrased on an exam "A memory location has physical address `XXXXXh`. If the segment number is `YYYYh`, find the offset." — or the reverse (given offset, find segment) — or the reverse-reverse (given segment:offset, find physical). **All three use the same one formula rearranged.** Learn the formula, not three separate procedures.

> [!important] Conceptual point worth a definition/short-answer mark Because segments overlap (they start every 16 bytes, not every 64 KB), **more than one segment:offset pair can point to the same physical address.** If asked "can two different logical addresses refer to the same physical byte?" — the answer is **yes**, and you should be able to explain why using the paragraph-boundary idea above.

### 3.4 Program Segments (how CS/DS/SS/ES are actually used)

- Machine-language programs = instructions + data
- **Code** → loaded into the **Code Segment**
- **Data** → loaded into the **Data Segment**
- **Stack** (used for procedure calls) → loaded into the **Stack Segment**
- A second data segment, if needed, uses **ES**

> [!warning] Common mistake A segment does **not** have to fill the entire 64 KB — real program segments are usually smaller and packed close together, which is _why_ they overlap and only 4 are active ("visible") to the processor at once. A program can still reach other memory by changing what its segment registers point to.

### 3.5 Pointer and Index Registers (SP, BP, SI, DI)

> [!important] Core concept These four registers hold **offset addresses**. Unlike segment registers, they **can** be used directly in arithmetic and other instructions.

|Register|Paired segment|Function|
|---|---|---|
|**SP** — Stack Pointer|SS|Used with SS to access the stack|
|**BP** — Base Pointer|(normally SS)|Used to access data _on_ the stack; unlike SP, **BP can be used to access data in other segments** too|
|**SI** — Source Index|DS|Points into the data segment; incrementing SI walks through consecutive memory locations — used as the **source** in string operations|
|**DI** — Destination Index|ES|Points to memory; string operations use DI to access memory addressed by **ES** (the **destination**)|

> [!warning] Common mistake Mixing up SI and DI's paired segment: **SI → DS (source)**, **DI → ES (destination)**. This SI/DS vs DI/ES pairing is a classic fill-in-the-blank or matching question.

### 3.6 Instruction Pointer (IP)

- Paired with **CS** to fetch instructions: CS = segment, IP = offset of the _next instruction_
- Updated automatically after every instruction executes
- **Cannot be directly manipulated by an instruction** — it can never appear as an operand

> [!question] Classic true/false trap "You can write an instruction like `MOV IP, 0500h` to jump to a new address." **False** — IP is unique among the pointer/index registers in that it **cannot be an instruction operand.** (Jumps work by other means, e.g. CALL/JMP, which the processor uses to update CS:IP internally.)

### 3.7 FLAGS Register

> [!important] Two categories — a common short-answer pairing question
> 
> |Type|Purpose|Example|
> |---|---|---|
> |**Status flags**|Reflect the _result_ of an instruction|`ZF` (Zero Flag) — set to 1 if e.g. `AX − BX` results in 0|
> |**Control flags**|Enable/disable certain processor operations|`IF` (Interrupt Flag) — if cleared (0), keyboard input is ignored|

> [!question] Likely exam phrasing "Differentiate between status flags and control flags, with one example of each." **Answer:** Status flags passively _report_ the outcome of an operation (e.g. ZF after a subtraction); control flags actively _change processor behavior_ (e.g. IF turning keyboard interrupts on/off).

---

## 4. Overall Structure of the IBM PC

> [!important] Core concept A computer = **hardware + software**, coordinated by the **Operating System**.

### 4.1 The Operating System — job list (good for a "list the functions of an OS" question)

- Reads and executes user-typed commands
- Performs I/O operations
- Generates error messages
- Manages memory and other resources

### 4.2 DOS specifics

- Designed specifically for the **8086**
- Could manage only **1 MB** of memory
- Does **not** support multitasking
- Handles reading/writing files on disk
- Every file has a **name (1–8 characters) + extension**, extension indicates file type

> [!warning] Common mistake Confusing what DOS manages vs what BIOS manages — see the comparison directly below, this distinction shows up often as a matching/definition question.

### 4.3 BIOS

- Performs **I/O operations** for the PC
- **Machine-specific** (unlike DOS, which works across the whole PC family)
- Also does **circuit checking** and **loads DOS** at startup
- The addresses of BIOS routines are called **interrupt vectors**

> [!question] Likely exam phrasing "What is the key difference between DOS and BIOS routines?" **Answer:** DOS routines work across the entire PC family (hardware-independent); BIOS routines are specific to the machine's actual hardware. BIOS also runs first at startup — it checks the system and loads DOS.

---

## 5. Memory Organization of the PC

> [!important] Core concept The 8086/8088 can address **1 MB** total, but **not all of it is free for programs** — parts are reserved for system use.

|Reserved area|Address range|
|---|---|
|Interrupt vectors|`00000h`–`003FFh` (first 1 KB)|
|BIOS & DOS data, DOS, application area|above `00400h`|
|Video memory|`A0000h`–`B0000h`+|
|Reserved (system)|`C0000h`–`E0000h`|
|**BIOS**|`F0000h`–`FFFFFh`|

### 5.1 Disjoint segments

- Memory splits into **16 disjoint 64 KB segments**: `0000h, 1000h, 2000h, … F000h`
- Each spans e.g. `0000:0000`–`0FFFFh`, then `1000:0000`–`1FFFFh`, etc.
- **Only the first 10 segments (`0000h`–`9000h`) are used by DOS** for loading/running applications
- 10 segments × 64 KB = **640 KB** — this is the famous "640 KB conventional memory" figure
- PC memory size is described in terms of these segments (e.g., a 512 KB PC = 8 of these segments)

> [!question] Likely exam phrasing "Why is conventional DOS memory limited to 640 KB even though the 8086 can address 1 MB?" **Answer:** Only the first 10 of the 16 disjoint 64 KB segments (10 × 64 KB = 640 KB) are allocated to DOS/applications — the remaining 6 segments (`A000h`–`F000h`) are reserved for video memory, system use, and BIOS.

---

## 6. I/O Ports, DOS, and BIOS — Startup Sequence

> [!important] Power-up sequence — a strong candidate for a step-by-step or fill-in-the-blank question
> 
> 1. PC powers up → 8086/8088 enters **reset state**
> 2. Registers set to: **CS = FFFFh, IP = 0000h**
> 3. First instruction executes at physical address **`FFFF0h`** (CS:IP → FFFF0 + 0 = FFFF0h) — this is in **ROM**
> 4. ROM instruction transfers control to the **BIOS routines**
> 5. BIOS checks for **system and memory errors**
> 6. BIOS **initializes interrupt vectors and BIOS data area**
> 7. BIOS **loads the operating system**:
>     - Step 1: BIOS loads the **boot program**
>     - Step 2: boot program loads the actual **OS routines** ("boot" = computer pulling itself up by its bootstraps)
> 8. Once the OS is loaded, **COMMAND.COM** is given control

> [!warning] Common mistake Getting **CS and IP reversed**, or forgetting that `FFFF0h` (not `FFFFFh` or `F0000h`) is where execution actually starts. Compute it yourself instead of memorizing: CS(FFFFh) × 10h = FFFF0h, + IP(0000h) = **FFFF0h**. This is a perfect mini application of the Section 3.3 formula, so an exam may test both ideas in one question.

---

## 🎯 Quick-Fire Recall Sheet (night-before review)

- 8086 = 16-bit bus, 8088 = 8-bit external bus, same internals & instruction set
- 80186/80188 = enhanced 8086/8088, no real advantage, overshadowed by 80286
- 80286 = real mode (8086-like) / protected mode (multitasking, memory protection, 16MB, virtual memory)
- 80386 = first 32-bit, adds virtual 8086 mode, 4GB physical / 64TB virtual
- 80486 = 386 + built-in FPU + 8KB cache, ~3× faster than 386
- "SX" variants = same core, cheaper external bus or missing FPU
- 14 registers total, all 16-bit: 4 general, 4 segment, 5 pointer/index, 1 flags
- AX = accumulator (mult/div/I-O), BX = base (table lookup), CX = counter (loops/strings), DX = data (mult/div/I-O)
- CS/DS/SS/ES = code/data/stack/extra segment
- **Physical = Segment×10h + Offset** — the one formula, rearrange as needed
- Highest 20-bit address = `FFFFFh`; segments start every 16 bytes (paragraph boundary)
- SP↔SS, BP↔stack (but can cross segments), SI↔DS (source), DI↔ES (destination)
- IP can never be a direct instruction operand
- FLAGS: status (reports result, e.g. ZF) vs control (enables/disables behavior, e.g. IF)
- DOS = 1MB max, no multitasking, hardware-independent; BIOS = machine-specific, does I/O + startup checks
- Only 10 of 16 64KB segments used by DOS → **640 KB** conventional memory
- Boot sequence: CS=FFFFh, IP=0000h → executes at `FFFF0h` (ROM) → BIOS → boot program → OS → COMMAND.COM

## 📋 Predicted Question Formats

- **Comparison table** — "differentiate X and Y" (8086/8088, 80186/80188, 80386/80386SX, 80486/80486SX)
- **Calculation** — segment:offset ⇄ physical address (practice with fresh random hex numbers, not just the ones above)
- **Fill-in-the-blank / matching** — register → special function
- **Definition** — logical address, physical address, paragraph, paragraph boundary, interrupt vector
- **Short answer** — DOS vs BIOS, status vs control flags, real vs protected mode
- **Sequence/ordering** — the startup boot process