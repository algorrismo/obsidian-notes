---
tags:
  - "#COA"
course: Computer Organization and Architecture (Course Code 0052)
lecture: Lecture 4 of 5 — Assembly Language Programming (Week 4, Summer 25'26)
---
---

# Assembly Language Programming: Exam Guide

> [!info] How to use this
> This is written the way I'd review it with you before a midterm: every topic from the slide gets a plain-English summary, the exact traps this professor built into their own examples, and a prediction of how it becomes a question. 
> 
> Sections marked ⭐ are the ones I'd bet money on appearing on the exam — they're either repeated 4-5 times across the slide (MOV/ADD/SUB pattern) or they're a "gotcha" the professor clearly designed on purpose (the hex numbers, LEA vs MOV, memory-to-memory).

## 0. The Big Picture — why this lecture exists

Everything in this lecture builds toward **one skill**: taking a simple idea ("add 1 to a variable", "print a message", "swap two values") and expressing it using only the primitive tools assembly gives you.

The professor's own "Four Steps" (from the Overview slide) is basically the exam's table of contents:

1. Learn syntax (the 4 fields)
2. Variable declarations (DB/DW, EQU)
3. Basic data movement (MOV, XCHG, ADD, SUB, INC, DEC, NEG)
4. Program organization (Stack/Data/Code segments)

> [!tip] Also memorize this framing sentence "Assembly instructions are so basic that I/O is much harder than in high-level languages — so we use **DOS functions (INT 21h)** for I/O because they're easy to invoke and fast." This exact idea ("why do we need INT 21h") is a common short-answer/definition question.

---

## 1. Statement Syntax — The Four Fields ⭐

Every line of code is a **statement**, and a statement is either:

- an **instruction** → gets translated into machine code (e.g. `MOV`, `ADD`)
- a **directive / pseudo-op** → tells the assembler to _do something_, but is **not** translated into machine code (e.g. `PROC`, `DB`, `EQU`)

A statement can have up to **four fields, in this exact order**:

```
Name        Operation      Operand(s)      ;Comment
START       MOV            CX,5            ; initialize counter
```

- Fields must be separated by **at least one blank or tab**.
- Assembly is **not case-sensitive** (but uppercase is used by convention to make code stand out).

> [!question] Likely question "List the four fields of an assembly statement, in order" or "Identify the Name/Operation/Operand/Comment field in this line of code." [!tip] How to answer Just walk left to right: label/name → opcode/directive → operand(s) → everything after `;`.

### 1a. Name Field — legality rules ⭐⭐⭐ (very testable)

- Used for instruction labels, procedure names, and variable names.
- **1 to 31 characters**, made of letters, digits, and the special characters **`? . _ @ $`**
- The period `.` may **only appear as the first character** of a name (this is the rule the professor is hiding inside the "illegal" example `A45.28`).
- **Cannot begin with a digit.**
- **No embedded blanks** (spaces).
- Case doesn't matter (`TwoWords` = `TWOWORDS`).

**Legal examples from the slide:** `COUNTER1`, `$1000`, `Done?`, `.TEST` **Illegal examples from the slide:** `TWO WORD` (space), `2AB` (starts with digit), `A45.28` (period not in first position), `ME &YOU` (space, and `&` is not a legal special character)

> [!warning] Common mistake Students assume _any_ punctuation is fine because `.TEST` and `Done?` look "weird" but legal. The rule isn't "no punctuation" — it's "**only** `? . _ @ $`, and `.` only as the very first character."

#### Worked exercise (from the slide's "Solve the Following")

|Name|Verdict|Why|
|---|---|---|
|`TWO_WORDS`|✅ Legal|underscore is allowed, no spaces|
|`TwoWOrDs`|✅ Legal|just letters, case doesn't matter|
|`?1`|✅ Legal|starts with `?` — only _digits_ are banned as the first character|
|`.@?`|✅ Legal|period is the first character (allowed), `@` and `?` are legal special chars|
|`$145`|✅ Legal|starts with `$` (a legal special char), same pattern as the `$1000` example given|
|`LET'S_GO`|❌ **Illegal**|the apostrophe `'` is **not** one of the allowed special characters|
|`T = .`|❌ **Illegal**|contains spaces and `=`, which aren't valid inside a single name token|

> [!question] Likely question A list of 5-7 names, "circle the legal ones" / "state why each illegal one is illegal." [!tip] How to answer Run every name through this 4-point checklist: (1) only letters/digits/`? . _ @ $`? (2) period only in position 1? (3) doesn't start with a digit? (4) no spaces? If it fails any point, it's illegal — and say _which_ point it fails, since partial credit usually comes from the reason, not just the verdict.

### 1b. Operation Field

- Holds the **opcode** (for instructions, e.g. `MOV`, `ADD`) — this _is_ translated to machine code.
- Holds a **pseudo-op** (for directives, e.g. `PROC`, `DB`) — this is **not** translated to machine code, it just instructs the assembler.

> [!question] Likely question "Is `PROC` translated into machine code? Why or why not?" → No — it's a pseudo-op / directive; it only tells the assembler to do something (like create a procedure), it doesn't correspond to a CPU instruction.

### 1c. Operand Field

- An instruction can have **zero, one, or two** operands (`NOP` / `INC AX` / `ADD WORD1,2`).
- **Two-operand order is always: `destination, source`.**
- The source is (usually) left unmodified; the destination gets overwritten with the result.

> [!warning] Common mistake Reversing destination/source when translating English into assembly. "Add AX to WORD1" is `ADD WORD1,AX` — the thing being changed (WORD1) comes **first**.

### 1d. Comment Field

- Starts with `;`. Everything after `;` on that line is ignored by the assembler.
- Not graded content by itself, but expect a T/F or fill-in-the-blank: "What character starts a comment in assembly?" → `;`

---

## 2. Representing Data: Numbers & Characters ⭐⭐⭐ (guaranteed trap)

The processor only understands binary, but you can _write_ numbers three ways:

|Type|Rule|Example|
|---|---|---|
|Binary|bit-string ending in `B`/`b`|`1010B`|
|Decimal|digit string, optional trailing `D`/`d` (or nothing)|`1234`|
|Hex|**must begin with a decimal digit (0-9)**, ends in `H`/`h`|`12ABh`|

Character strings go in single **or** double quotes (`'A'` or `"hello"`) and are translated straight to ASCII — `'A'` is _identical_ to `41h` or `65d` to the assembler.

> [!danger] THE classic trap in this lecture A hex number **must start with a digit 0–9**, not a letter. So `FFFEh` and `Bh` as literally written are **illegal** — they must be re-written with a leading zero: `0FFFEh` and `0Bh`. This exists specifically so the assembler can tell a hex number apart from a name/label. This trick shows up almost verbatim as an exam question.

#### Worked exercise (from the slide)

|Written|Legal?|Type / Fix|
|---|---|---|
|`246`|✅|Decimal|
|`246h`|✅|Hex (starts with digit `2`)|
|`1001`|✅|Decimal (no `B` suffix → not read as binary)|
|`1,001`|❌|Commas are never allowed in a numeric literal|
|`2A3h`|✅|Hex (starts with digit `2`)|
|`FFFEh`|❌|Starts with letter `F` → must be written `0FFFEh`|
|`0Ah`|✅|Hex (starts with `0`)|
|`Bh`|❌|Starts with letter `B` → must be written `0Bh`|
|`1110b`|✅|Binary|

> [!question] Likely question Same table format with different numbers, e.g. `ACE h`, `9h`, `2,500`, `101b`, `E2h`. Or: "Rewrite this illegal hex number so it's legal." [!tip] How to answer Check trailing letter first (B/D/H → tells you the family), **then** check the very first character of a hex number is 0-9 — if not, mentally prepend a `0`.

---

## 3. Variables — DB and DW

- **`DB`** (Define Byte): allocates **1 byte**, range **2⁸ = 256** possible values. `?` means "uninitialized." `ALPHA DB 4`
- **`DW`** (Define Word): allocates **2 bytes (1 word)**, range **2¹⁶ = 65536**. `WRD DW -2`

> [!question] Likely question "What is the range of values a byte/word variable can hold?" → byte: 2⁸ = 256 (0–255 unsigned, or −128 to 127 signed). word: 2¹⁶ = 65536 (0–65535 unsigned, or −32768 to 32767 signed).

### 3a. Arrays

An array is just a run of consecutive DB's or DW's; the name refers to the **first** element, and you reach later elements with `name+offset`.

```
B_ARRAY DB 10h, 20h, 30h      ; if B_ARRAY is at address 200:
```

|Name|Address|Value|
|---|---|---|
|B_ARRAY|200|10h|
|B_ARRAY+1|201|20h|
|B_ARRAY+2|202|30h|

> [!warning] Common mistake **Byte arrays step by 1**, **word arrays step by 2** (because each element is 2 bytes). This is the #1 arithmetic slip on this topic.

#### Worked exercise: word array starting at 500

`MY_W_ARRAY DW 2000,323,4000,1000`

|Name|Address|Value|
|---|---|---|
|MY_W_ARRAY|500|2000|
|MY_W_ARRAY+2|502|323|
|MY_W_ARRAY+4|504|4000|
|MY_W_ARRAY+6|506|1000|

> [!question] Likely question "Given a starting address and a list of values, declare the array and give the address table" — for either a byte array (DB, step 1) or a word array (DW, step 2). Expect them to swap DB↔DW to see if you remember the step size changes.

### 3b. High / Low bytes of a word (little-endian) ⭐⭐

```
WORD1 DW 1234H
```

- **Low byte** → symbolic address `WORD1` → contains **34h**
- **High byte** → symbolic address `WORD1+1` → contains **12h**

> [!danger] Common mistake This looks backwards to most students the first time — the **least significant byte is stored at the lower address** (x86 is "little-endian"). It is _not_ `WORD1 = 12h, WORD1+1 = 34h`. Memorize it as: _low address = low byte_.

### 3c. Character strings

`LETTER DB 'ABC'` is identical to `LETTER DB 41h,42h,43h`. You can also mix literal strings and individual byte codes in one `DB`: `MSG DB 'HELLO', 0Ah, 0Dh, '$'`

> [!tip] Note on newline order This particular slide example writes `0Ah, 0Dh` (LF then CR). The professor's own **worked full program** later in the deck uses the standard order **CR then LF** (`0Dh` then `0Ah`, i.e. `\r\n`) to actually move the cursor to a new line. If you're writing your own "go to new line" code, use CR-then-LF (0Dh, 0Ah) like the working example — that's the one that's proven to actually work in the program.

### 3d. Named constants — `EQU`

```
LF EQU 0Ah          ; LF now means 0Ah everywhere after this line
PROMPT EQU 'Type Your Name'
```

> [!warning] Common mistake **`EQU` allocates NO memory.** It's just a text substitution/name for a constant — don't confuse it with `DB`/`DW`, which _do_ reserve memory. "Does EQU take up memory? Why/why not?" is a very plausible short-answer question. Answer: No — it's a compile-time substitution, not a variable.

---

## 4. Data Movement & Arithmetic Instructions ⭐⭐⭐⭐⭐ (heart of the exam)

This whole block of the lecture (MOV, XCHG, ADD, SUB, INC, DEC, NEG) is drilled with near-identical "solve the following" exercises — **expect this exact format on the exam, with different numbers.**

### 4a. The universal legality rule (learn this ONCE, apply everywhere)

For any **two-operand** instruction (`MOV`, `XCHG`, `ADD`, `SUB`, ...):

> [!danger] The rule that generates 80% of the "legal/illegal" questions **You can never have two memory operands in the same instruction.** (`MOV W1,W2`, `ADD W1,W2`, `XCHG W1,W2`, `SUB W1,W2` are ALL illegal.) At least one operand must be a register (or the source can be a constant).

Plus, only for **MOV** (segment registers make this special):

- A **constant cannot be moved directly into a segment register** (`MOV DS,1000h` ❌ — must go through a general register: `MOV AX,1000h` then `MOV DS,AX`)
- **Segment register → segment register is illegal** (`MOV CS,ES` ❌)
- Segment register ↔ general register and segment register ↔ memory **are** legal.

**And always, everywhere (the "Agreement of Operands" rule):**

> [!danger] Size/type must match The two operands of a two-operand instruction must be the **same size** (both byte, or both word). `MOV AX,BYTE1` is illegal if `BYTE1` is declared `DB` (byte) but `AX` is a word register. `MOV AH,'A'` is legal (byte↔byte). A literal constant like `'A'` used as a source is flexible and can match whatever size the destination needs — but a _declared_ variable's size is fixed.

### 4b. MOV — copy a value

`MOV destination, source` → copies source into destination; **source is unchanged**.

**Legal combination table (MOV):**

|Source → / Dest. ↓|General Reg|Segment Reg|Memory|Constant|
|---|---|---|---|---|
|General Register|✅|✅|✅|—|
|Segment Register|✅|❌|✅|—|
|Memory|✅|✅|❌ (`MOV W1,W2` illegal)|—|
|Constant|✅|❌|✅|—|

**Worked exercise:**

- `MOV BX,A` (A is a word, value 24h) → **BX = 0024h**, **A unchanged = 0024h**
- Then `MOV AX,BX` → **AX = 0024h**, **BX unchanged = 0024h**
- `MOV DS,AX` → ✅ Legal (general reg → segment reg)
- `MOV DS,1000h` → ❌ Illegal (constant → segment register not allowed)
- `MOV CS,ES` → ❌ Illegal (segment reg → segment reg not allowed)
- `MOV W1,DS` → ✅ Legal (segment reg → memory)
- `MOV W1,B1` → ❌ Illegal _if_ W1 is a word and B1 is a byte (size mismatch)

### 4c. XCHG — swap two values

`XCHG destination, source` → **both** operands change (they trade values).

**Legal combinations:** general register ↔ general register ✅, general register ↔ memory ✅, memory ↔ memory ❌. (No "constant" column — you can't exchange with a literal, it has nowhere to store the old value.)

> [!question] Likely question "How do you swap the contents of two memory variables, W1 and W2, if `XCHG W1,W2` is illegal?" [!tip] How to answer — memorize this exact 3-line pattern
> 
> ```
> MOV AX, W1
> XCHG AX, W2
> MOV W1, AX
> ```
> 
> This "route it through a register" trick is the single most reusable idea in this whole lecture — it also solves the memory-to-memory MOV/ADD/SUB problem the same way.

### 4d. ADD / SUB — arithmetic

`ADD dest,source` → dest = dest + source. `SUB dest,source` → dest = dest − source. Source is unchanged; same legality table as MOV minus the segment-register rows (arithmetic only works on general registers/memory/constants).

**Worked exercise (ADD):** BX=5h, A=9h

- `ADD BX,A` → **BX = 0Eh (14)**, A unchanged = 9h
- `ADD AX,BX` (given AX=9h) → **AX = 9h+0Eh = 17h**, BX unchanged = 0Eh
- `ADD B1,B2` ❌ illegal (memory-memory) · `ADD AL,56H` ✅ legal (register + constant)

**Worked exercise (SUB):** BX=Fh(15), A=9h

- `SUB BX,A` → **BX = Fh−9h = 6h**, A unchanged = 9h
- `SUB AX,BX` (given AX=9h) → **AX = 9h−6h = 3h**, BX unchanged = 6h
- `SUB B1,B2` ❌ illegal (memory-memory) · `SUB AL,56H` ✅ legal

> [!warning] Common mistake Doing hex subtraction in decimal by accident (e.g., forgetting `F = 15`, `A = 10`). Convert to decimal, subtract, convert back if you're not confident doing hex math directly — but **show the hex answer**, that's what's graded.

### 4e. INC / DEC — single-operand ±1

`INC dest` (dest = dest+1), `DEC dest` (dest = dest−1). One operand only.

**Worked exercise:** BX=3h, A=9h

- `INC BX` → BX = **4h** · `INC A` → A = **Ah (10)**
- `DEC BX` → BX = **2h** · `DEC A` → A = **8h**

### 4f. NEG — two's complement (negate)

`NEG dest` → replaces the value with its **two's complement** (invert all bits, then add 1). Same method the CPU uses for signed negation.

**Worked exercise (16-bit, e.g. BX):** BX=3h (0003h) → invert = FFFCh → +1 = **FFFDh** **Worked exercise (word-sized A=9h → 0009h):** invert = FFF6h → +1 = **FFF7h** _(If your version of "A" is byte-sized instead: 09h → invert F6h → +1 = **F7h**. Use whichever size your instructor declared A as — the method is identical either way.)_

> [!question] Likely question "Trace the value of two registers through 4-5 sequential instructions" (mixing MOV/ADD/SUB/INC/DEC/NEG), or "is this instruction legal, and if not, why + how would you fix it?" [!tip] How to answer — step-by-step method
> 
> 1. Write down starting values of every register/variable mentioned.
> 2. Process instructions **one at a time, top to bottom** — update only the destination, unless it's XCHG (updates both).
> 3. For legality questions: check (a) two memory operands? (b) size mismatch? (c) segment register + constant, or segment+segment (MOV only)? Any "yes" → illegal, and say which rule it broke.
> 4. Do hex arithmetic digit-by-digit (or convert to decimal, compute, convert back) — **always double check by re-adding your answer**.

---

## 5. Translating High-Level Code → Assembly ⭐⭐⭐ (high-value, easy to miss)

This is the payoff of everything above, and it's exactly the kind of question that separates people who memorized rules from people who understand them.

**The one idea that unlocks this whole section:** _You almost never operate directly on two memory variables. Load one into a register (usually AX), do your arithmetic against the register, then store the register back into the destination._

|High-level statement|Assembly translation|Why|
|---|---|---|
|`B = A`|`MOV AX,A` <br> `MOV B,AX`|Can't do `MOV B,A` directly — that's memory→memory, illegal. Route through AX.|
|`A = 5 - A`|**Option 1:** `MOV AX,5` / `SUB AX,A` / `MOV A,AX` <br> **Option 2:** `NEG A` / `ADD A,5`|Two valid solutions exist! Option 2 works because NEG/ADD with one memory operand + one register/constant is legal — no register needed.|
|`A = B - 2*A`|`MOV AX,B` <br> `SUB AX,A` <br> `SUB AX,A` <br> `MOV A,AX`|No `MUL` was taught, so "2×A" is done by **subtracting A twice** (2A = A+A). Clever reuse of SUB instead of needing multiplication.|

> [!tip] Reassurance for the exam Translation questions usually have **more than one correct answer** (see `A = 5-A` above). If your version obeys all the legality rules and produces the mathematically correct result, it should earn full credit even if it doesn't match "the" answer key exactly.

> [!question] Likely question "Translate `X = Y + Z` / `A = A + B - C` / `X = 3*A - B` (no MUL taught, so do repeated ADD) into assembly." or "Translate `TEMP = X; X = Y; Y = TEMP` (a classic swap) into assembly" — this is literally the XCHG-through-a-register trick from section 4c wearing a different hat.

---

## 6. Program Structure ⭐⭐

A program is built from **three parts**, and each becomes a memory _segment_: **Stack, Data, Code.**

The size of code/data is set with `.MODEL memory_model`. This lecture only covers: `.MODEL SMALL` → code fits in ONE segment, data fits in ONE segment.

> [!warning] Common mistake The directive **order matters** and is a common ordering/fill-in-the-blank question: `.MODEL` → `.STACK` → `.DATA` → `.CODE`.

### 6a. Stack Segment

```
.STACK size        ; e.g. .STACK 100H
```

- Reserve enough space for the stack at its _maximum_ size.
- `.STACK 100H` → 256 bytes, "reasonable for most applications" per the slide.
- **If size is omitted → 1KB (1024 bytes) is allocated by default.**

> [!question] Likely question "What happens if you write `.STACK` with no size?" → 1 KB is allocated automatically.

### 6b. Data Segment

```
.DATA
WORD1 DW 2
BYTE1 DB 1
MSG   DB 'THIS IS A MESSAGE'
MASK  EQU 10010001B
```

All variable **and** constant declarations live here (constants via `EQU` don't consume memory, as noted earlier).

### 6c. Code Segment

```
.CODE name          ; name is optional, and not needed for SMALL model
name PROC
   ; body
name ENDP
```

- `PROC` / `ENDP` are pseudo-ops that bracket a procedure — they are **not** translated to machine code themselves.

### 6d. Full skeleton (memorize this shape)

```
.MODEL SMALL
.STACK 100H
.DATA
    ; data definitions here
.CODE MAIN
    MAIN PROC
        ; instructions go here
    MAIN ENDP
    ; other procedures go here
END MAIN
```

> [!danger] Common mistake **The very last line of the program must be `END` followed by the name of the main procedure** (`END MAIN`). Forgetting this, or forgetting `MAIN ENDP`, is a classic "spot the bug" question.

---

## 7. I/O via DOS Interrupts — `INT 21h` ⭐⭐⭐

`INT interrupt_number` interrupts normal execution to run a service routine. To request a specific DOS service: **put the function number in `AH`, then execute `INT 21h`.**

|AH (function #)|Routine|Input|Output|
|---|---|---|---|
|1|single-key input|AH=1|AL = 0 if no input, else ASCII of the key pressed|
|2|single-character output|AH=2, **DL** = ASCII of char to print|prints it; AL also ends up = ASCII of the char|
|9|character-string output|AH=9, **DX** = address of string ending in **`$`**|prints the whole string|

> [!danger] Trap: function 9 needs an address, not a value Function 9 requires `DX` to hold the **offset address** of a string (not the string's content!) — so you need `LEA DX, MSG` (see next section). The string **must be terminated with `$`** or it will print garbage past the end. The worked example in this lecture only demonstrates functions 1 and 2 — function 9 is left for the homework, which strongly suggests it's fair game for the exam.

> [!question] Likely question "Which AH value do you use to print a whole string vs. a single character vs. read a key?" or "What must a string end with to use function 9, and why?"

---

## 8. Full Worked Example — read a character, echo it on the next line

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    ; display prompt to the user
    MOV AH,2        ; display character function
    MOV DL,'?'       ; character is '?'
    INT 21H          ; display the DL char (?)

    ; input a character
    MOV AH,1         ; read character function
    INT 21H          ; character is in AL
    MOV BL,AL        ; save input to BL reg

    ; go to new line
    MOV AH,2
    MOV DL,0Dh       ; carriage return
    INT 21H
    MOV DL,0Ah       ; line feed
    INT 21h

    ; display character
    MOV DL,BL        ; retrieve character
    INT 21h

    ; return to DOS
    MOV AH,4Ch       ; terminate process, return control to DOS
    INT 21h
MAIN ENDP
END MAIN
```

> [!tip] Notice what's absent This program has **no `.DATA` section**, so it never needs `MOV AX,@DATA` / `MOV DS,AX`. It only uses registers and immediate constants. Compare this with section 9 below — the moment you add a `.DATA` section, that boilerplate becomes **mandatory**.

> [!question] Likely question "Trace this program's output for a given keypress" or "modify this program to also do X" or a fill-in-the-blank version with 2-3 lines removed. [!tip] How to answer Narrate it function-by-function: AH=2 always prints whatever's in DL; AH=1 always reads into AL; termination is always `MOV AH,4Ch` + `INT 21h`. `0Dh` then `0Ah` = "go to start of next line" (carriage return + line feed).

### Assemble/Link pipeline

```
Editor  →  source.ASM  →  Assembler  →  .OBJ  →  Linker  →  .EXE
```

> [!question] Likely question "Put these in order" or "what file extension comes out of the assembler vs. the linker?" → Assembler produces `.OBJ`; Linker produces `.EXE`.

---

## 9. LEA — Load Effective Address ⭐⭐⭐ (classic MOV vs LEA confusion)

```
LEA destination, source
```

`LEA` copies the **offset address** of the source into the destination — **not the value stored there.**

```asm
LEA DX, MSG     ; DX now holds the ADDRESS of MSG, not MSG's contents
```

> [!danger] The single most common conceptual mistake in this topic **`MOV` moves a _value_. `LEA` moves an _address_.** If you write `MOV DX,MSG` when you meant to point at a string for `INT 21h` function 9, you're loading the wrong thing. This is exactly why function 9 needs `LEA DX,MSG` before `INT 21h`, not `MOV`.

> [!question] Likely question "What's the difference between MOV and LEA?" / "Why does printing a string with INT 21h/9 require LEA instead of MOV?" [!tip] How to answer One sentence: _MOV copies the value stored at an address; LEA copies the address itself_ — you need LEA whenever a DOS function (like AH=9) expects a **pointer** to data rather than the data.

---

## 10. Program Segment Prefix (PSP) & the `DS` setup boilerplate ⭐⭐

- The **PSP** holds information about the program so DOS can manage it.
- DOS automatically loads the PSP's segment number into `DS` and `ES` before your program runs — **but that is NOT the same as your `.DATA` segment's address.**
- So **any program that declares variables in `.DATA` must explicitly point `DS` at that data segment**, using this exact two-line idiom near the top of `MAIN PROC`:

```asm
MOV AX,@DATA     ; @DATA = the address of the segment defined by .DATA
MOV DS,AX        ; can't load a segment register directly with MOV AX,@DATA→DS in one step (MOV const→segreg is illegal!) so we route through AX
```

> [!danger] Why this is two lines, not one Notice this is exactly the "constant → segment register is illegal" rule from Section 4b in action — you cannot do `MOV DS,@DATA` directly, you must stage it through a general register first.

> [!question] Likely question "Why does every program with a `.DATA` section start with `MOV AX,@DATA` / `MOV DS,AX`?" or "This program is missing 2 lines and its string output is garbled — what's missing?" [!tip] How to answer DS isn't automatically pointed at your data segment; without these two lines, any reference to a `.DATA` variable (like `LEA DX,MSG`) would read the wrong segment. Also mention _why_ it's two instructions, not one (segment register can't take a constant directly).

---

## 11. Homework Problems — worked solutions (very likely to reappear)

### HW 1 — Print `HELLO!` on the screen

This is the natural place to test **function 9** (string output), which the worked example never actually used.

```asm
.MODEL SMALL
.STACK 100H
.DATA
    MSG DB 'HELLO!$'          ; must end in $
.CODE
MAIN PROC
    MOV AX,@DATA               ; required because we now HAVE a .DATA section
    MOV DS,AX

    LEA DX,MSG                 ; DX = address of MSG (not its value!)
    MOV AH,9                   ; string output function
    INT 21h

    MOV AH,4Ch
    INT 21h
MAIN ENDP
END MAIN
```

### HW 2 — Convert a lower-case letter typed by the user to upper-case

**Key fact to know cold:** in ASCII, lower-case letters are exactly **`20h` (32 decimal) higher** than their upper-case equivalent (`'a'=61h`, `'A'=41h`). So subtracting `20h` converts lower→upper.

```asm
.MODEL SMALL
.STACK 100H
.DATA
    PROMPT DB 'ENTER A LOWER-CASE LETTER: $'
    MSG2   DB 0Dh,0Ah,'IN UPPERCASE IT IS: $'
.CODE
MAIN PROC
    MOV AX,@DATA
    MOV DS,AX

    LEA DX,PROMPT
    MOV AH,9
    INT 21h

    MOV AH,1                   ; read the character
    INT 21h                    ; AL = the character typed
    SUB AL,20h                 ; convert to uppercase

    MOV BL,AL                  ; save the converted char

    LEA DX,MSG2
    MOV AH,9
    INT 21h

    MOV DL,BL                  ; print the converted character
    MOV AH,2
    INT 21h

    MOV AH,4Ch
    INT 21h
MAIN ENDP
END MAIN
```

> [!question] Likely question "Write a program that reads X and does Y" using only the instructions and INT 21h functions taught in this lecture. Almost certainly one string-output (AH=9, needs `$` and `LEA`) and one single-char I/O (AH=1/AH=2) will both be required, plus the `.DATA`→`MOV AX,@DATA`/`MOV DS,AX` boilerplate. [!tip] How to answer Build it in this fixed order every time: `.MODEL SMALL` → `.STACK` → `.DATA` (declare every string, ending user-facing ones in `$`) → `.CODE` → `MAIN PROC` → `MOV AX,@DATA`/`MOV DS,AX` (only if `.DATA` is non-empty) → your logic → `MOV AH,4Ch`/`INT 21h` to terminate → `MAIN ENDP` → `END MAIN`.

---

## 12. 🔥 Top Exam Traps — final cheat sheet

|#|Trap|Correct rule|
|---|---|---|
|1|`FFFEh`, `Bh` "look like" legal hex|Hex literals must **start with a digit 0-9** → `0FFFEh`, `0Bh`|
|2|`MOV W1,W2` / `ADD W1,W2` / `XCHG W1,W2`|**Memory-to-memory is always illegal** — route through a register|
|3|`MOV DS,1000h`|Can't load a segment register with a constant directly — stage through a general register|
|4|`MOV CS,ES`|Segment register → segment register is illegal|
|5|Word `1234H` → thinking `WORD1=12h, WORD1+1=34h`|Little-endian: **low address holds the low byte** → `WORD1=34h, WORD1+1=12h`|
|6|Byte array vs word array offsets|Byte array steps by **1**; word array steps by **2**|
|7|Confusing `LEA` and `MOV`|`MOV` copies a **value**; `LEA` copies an **address**|
|8|Forgetting `MOV AX,@DATA` / `MOV DS,AX`|Required whenever the program has a `.DATA` section (not required if it doesn't)|
|9|Forgetting the `$` terminator on strings used with `INT 21h`/AH=9|Function 9 prints until it hits `$` — no `$` means it prints garbage memory|
|10|`MOV AX,BYTE1`|Two-operand instructions need **matching operand sizes** (byte↔byte, word↔word)|
|11|Missing `.STACK` size|Defaults to **1 KB**, not zero|
|12|Missing final line|Program must end with `END MAIN` (name of the main procedure)|

---

## 13. Rapid-fire self-test (cover the answers, then check yourself)

1. What are the four fields of a statement, in order? → _Name, Operation, Operand(s), Comment_
2. Why is `2AB` an illegal name? → _starts with a digit_
3. Why is `FFFEh` illegal as written? → _hex literal doesn't start with a decimal digit_
4. What does `EQU` allocate in memory? → _nothing — it's a text substitution_
5. Byte array vs. word array: how much does the address increase per element? → _1 byte vs. 2 bytes_
6. `WORD1 DW 1234H` — what's at address `WORD1+1`? → _12h (the high byte)_
7. Is `XCHG W1,W2` legal? → _No, memory-to-memory not allowed_
8. How do you swap two memory variables? → _`MOV AX,W1` / `XCHG AX,W2` / `MOV W1,AX`_
9. What's illegal about `MOV DS,1000h`? → _can't move a constant directly into a segment register_
10. What does `LEA DX,MSG` put into DX? → _the address of MSG, not its value_
11. What must a string end with to use `INT 21h` function 9? → _`$`_
12. Which two lines does almost every `.DATA`-using program start with, and why? → _`MOV AX,@DATA` / `MOV DS,AX` — because DS isn't automatically pointed at your data segment_
13. What terminates a DOS program? → _`MOV AH,4Ch` then `INT 21h`_
14. What's the last line of every program? → _`END` followed by the main procedure's name_

---

_Good luck — this lecture is really just one repeated skill (route memory-to-memory operations through a register) wearing different costumes (MOV, XCHG, ADD, SUB, translation problems). Once that clicks, most of this becomes mechanical._
