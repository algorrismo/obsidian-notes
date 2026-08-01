Tags : #COA 
Date: 2026-07-21

---

> **Course:** COE 3205 — Computer Organization & Architecture
> **Exam relevance:** HIGH — flags questions are a staple of assembly-level exams.

---

## 1. Overview — Why Flags Matter

- The CPU makes decisions based on its **current state**, represented by **9 individual bits (flags)**.
- Flags are stored in the **FLAGS register**.
- Two categories:
  - **Status flags** — reflect the result of the last computation
  - **Control flags** — enable/disable processor operations

**Exam angle:** "Why does a computer need flags?" → They let the CPU perform conditional execution (jumps, branches).

---

## 2. The FLAGS Register — Bit Layout

| Bit | Flag | Type |
|-----|------|------|
| 0 | CF (Carry) | Status |
| 2 | PF (Parity) | Status |
| 4 | AF (Auxiliary Carry) | Status |
| 6 | ZF (Zero) | Status |
| 7 | SF (Sign) | Status |
| 11 | OF (Overflow) | Status |
| 8 | TF (Trap) | Control |
| 9 | IF (Interrupt Enable) | Control |
| 10 | DF (Direction) | Control |
| 1,3,5,12-15 | Reserved | No significance |

**Student trap:** Bits 1, 3, 5, 12–15 have NO significance — don't assign them in answers.

---

## 3. Status Flags — One by One

### 3a. Carry Flag (CF)

| Operation | CF = 1 when |
|-----------|-------------|
| Addition | Carry **out** of MSB |
| Subtraction | Borrow **into** MSB |

**Student trap:** CF is about the **unsigned** interpretation. It tells you the result doesn't fit in the register for unsigned math.

### 3b. Parity Flag (PF)

- PF = 1 → even number of 1-bits in the **low byte only**
- PF = 0 → odd number of 1-bits

**Student trap:** Only the **low byte** matters. For `FFFFh` → low byte = `FF` = `11111111` (8 ones = even) → PF = 1.

### 3c. Auxiliary Carry Flag (AF)

- AF = 1 → carry out of **bit 3** (nibble boundary, bits 0–3 ↔ bits 4–7)
- Used mainly for BCD arithmetic

**Exam angle:** Rarely tested in detail, but know it exists.

### 3d. Zero Flag (ZF)

- ZF = 1 → result is **exactly zero**
- ZF = 0 → result is non-zero

**Student trap:** `MOV AX, -5` does NOT affect ANY flags (MOV never affects flags).

### 3e. Sign Flag (SF)

- SF = 1 → MSB of result is 1 (negative in signed interpretation)
- SF = 0 → MSB is 0 (positive)

### 3f. Overflow Flag (OF)

- OF = 1 → **signed** overflow occurred
- OF = 0 → no signed overflow

---

## 4. Overflow — The Big Topic

### Ranges to memorize:

| Type | 8-bit range | 16-bit range |
|------|-------------|--------------|
| Signed | -128 to 127 | -32768 to 32767 |
| Unsigned | 0 to 255 | 0 to 65535 |

### Four overflow scenarios:

1. **No overflow** — both signed and unsigned are correct
2. **Unsigned overflow only** — CF = 1, OF = 0
3. **Signed overflow only** — CF = 0, OF = 1
4. **Both overflow** — CF = 1, OF = 1

### Key rules:

| Situation | Unsigned overflow | Signed overflow |
|-----------|-------------------|-----------------|
| Addition, carry out of MSB | CF = 1 | — |
| Subtraction, borrow into MSB | CF = 1 | — |
| Same-sign addition, result different sign | — | OF = 1 |
| Different-sign addition | — | OF is **impossible** |
| Carry into MSB ≠ Carry out of MSB | — | OF = 1 |

**Student trap:** "Overflow is impossible when adding numbers with different signs." This is a common exam question.

### Example work-through (know these cold):

**Example 1: Unsigned overflow, no signed overflow**
```
AX = FFFFh, BX = 0001h
ADD AX, BX → 1 0000h → stored as 0000h
CF = 1 (unsigned overflow — result 65536 > 65535)
OF = 0 (signed: -1 + 1 = 0, correct)
```

**Example 2: Signed overflow, no unsigned overflow**
```
AX = 7FFFh, BX = 7FFFh
ADD AX, BX → FFFEh
CF = 0 (unsigned: 32767+32767 = 65534, fits in 16 bits)
OF = 1 (signed: 32767+32767 = 65534 > 32767, overflow!)
```

---

## 5. How Instructions Affect Flags

| Instruction | Flags affected |
|-------------|----------------|
| `MOV`, `XCHG` | **NONE** |
| `ADD`, `SUB` | **ALL** status flags |
| `INC`, `DEC` | All **EXCEPT CF** |
| `NEG` | All (CF = 1 unless result is 0; OF = 1 if operand is 8000h/80h) |

**Student trap #1:** `INC` and `DEC` do NOT change the Carry Flag. This is a very common exam trick.

**Student trap #2:** `MOV` never affects flags. If a question asks "what flags are set after `MOV AX, -5`", the answer is "none."

### NEG special cases:
- `NEG 8000h` → result is still `8000h` (its own two's complement) → OF = 1 because no sign change occurred.
- CF is always 1 after NEG unless the result is 0.

---

## 6. Worked Examples (Exam-Style)

### Example 1: ADD AX, BX (FFFFh + FFFFh)
```
  FFFFh
+ FFFFh
-------
 1FFFEh → stored as FFFEh

SF = 1 (MSB = 1)
PF = 0 (low byte = FE = 11111110, 7 ones = odd)
ZF = 0 (non-zero)
CF = 1 (carry out of MSB)
OF = 0 (carry INTO MSB = 1, carry OUT = 1, they match → no signed overflow)
```

### Example 2: ADD AL, BL (80h + 80h)
```
  80h = 10000000b
+ 80h = 10000000b
--------
 100h = 1 00000000b → stored as 00h

SF = 0 (MSB of stored result = 0)
PF = 1 (low byte = 00, 0 ones = even)
ZF = 1 (result is zero)
CF = 1 (carry out of MSB)
OF = 1 (both negative, result positive → sign changed → overflow)
```

### Example 3: NEG AX (AX = 8000h)
```
  8000h = 1000 0000 0000 0000
1's comp = 0111 1111 1111 1111
+ 1
2's comp = 1000 0000 0000 0000 = 8000h

SF = 1
PF = 1 (low byte = 00, even parity)
ZF = 0
CF = 1 (NEG always sets CF unless result = 0)
OF = 1 (8000h is its own negation → no sign change → overflow)
```

---

## 7. DEBUG Program & Flag Symbols

| Flag | Set (1) | Clear (0) |
|------|---------|-----------|
| CF | CY (carry) | NC (no carry) |
| PF | PE (even parity) | PO (odd parity) |
| AF | AC (auxiliary carry) | NA |
| ZF | ZR (zero) | NZ (nonzero) |
| SF | NG (negative) | PL (plus) |
| OF | OV (overflow) | NV (no overflow) |
| DF | DN (down) | UP (up) |
| IF | EI (enable interrupts) | DI (disable) |

**Exam angle:** You may be shown DEBUG output and asked to interpret the flag symbols.

---

## 8. Class Work Problems (Practice These)

1. `SUB AX, BX` where AX = 8000h, BX = 0001h
2. `INC AL` where AL = FFh
3. `MOV AX, -5`

**Answers to check yourself:**

1. `SUB AX, BX`: AX = 7FFFh. SF=0, ZF=0, CF=0 (no borrow into MSB — actually check carefully), OF=1 (8000h - 0001h = 7FFFh: negative - positive = positive? Wait: 8000h is -32768, 0001h is 1, so -32768 - 1 = -32769 which overflows → OF=1).

2. `INC AL` where AL = FFh: AL becomes 00h. ZF=1, SF=0, PF=1, OF=0. **CF is NOT affected** (INC doesn't touch CF).

3. `MOV AX, -5`: **No flags affected.** MOV never affects flags.

---

## 9. Common Exam Question Patterns

### Pattern 1: "Given these register values, determine all flag values after the instruction."
→ Work through the binary addition/subtraction, check each flag rule.

### Pattern 2: "Which instruction does NOT affect the carry flag?"
→ Answer: `INC`, `DEC`, `MOV`, `XCHG`

### Pattern 3: "Explain the difference between signed and unsigned overflow."
→ Unsigned overflow = CF=1, signed overflow = OF=1. They are independent.

### Pattern 4: "Is overflow possible when adding a positive and a negative number?"
→ **No.** Overflow in addition is only possible when both operands have the same sign.

### Pattern 5: "What is the result of NEG on 8000h? Why is OF=1?"
→ 8000h is its own two's complement, so negating it gives the same value. No sign change → OF=1.

### Pattern 6: Show the DEBUG flag symbols for a given FLAGS register value.
→ Memorize the CY/NC, PE/PO, ZR/NZ, NG/PL, OV/NV table.

---

## 10. Quick Reference Cheat Sheet

```
CF → unsigned overflow (carry out/borrow in)
OF → signed overflow (carry into MSB ≠ carry out)
ZF → result is zero
SF → MSB of result (signed sign)
PF → even/odd parity of low byte
AF → carry from bit 3 (BCD)

MOV/XCHG → affects NOTHING
INC/DEC → affects ALL except CF
ADD/SUB → affects ALL
NEG → affects ALL (CF=1 unless result=0)
```

---

## Related Lectures

- [[Lecture 4 - 8086 Addressing Modes]]
- [[Lecture 6 - Arithmetic Instructions]]
