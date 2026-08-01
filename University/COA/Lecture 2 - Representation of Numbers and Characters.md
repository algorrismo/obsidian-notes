# Lecture 2: Representation of Numbers and Characters

> **Course:** COE 3205 - Computer Organization & Architecture
> **Exam Weight:** HIGH - This is a foundational lecture with lots of calculation-based questions

---

## Table of Contents
1. [[#1. Number Systems]]
2. [[#2. Conversion Between Number Systems]]
3. [[#3. Addition and Subtraction]]
4. [[#4. Integer Representation in Computer]]
5. [[#5. ASCII Code]]

---

## 1. Number Systems

### 1.1 Decimal Number System
- **Base:** 10
- **Digits:** 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
- Positional number system: each digit associated with a power of 10
- Example: `3245 = 3×10³ + 2×10² + 4×10¹ + 5×10⁰`

### 1.2 Binary Number System
- **Base:** 2
- **Digits:** 0, 1
- Example: `11010₂ = 1×2⁴ + 1×2³ + 0×2² + 1×2¹ + 0×2⁰ = 26₁₀`

### 1.3 Hexadecimal Number System
- **Base:** 16
- **Digits:** 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F
- Example: `4A₁₆ = 4×16¹ + A×16⁰ = 64 + 10 = 74₁₀`

> [!important] Why Hexadecimal?
> - Binary numbers are too long and hard to read (e.g., 16 bits for 8086 word)
> - Decimal is difficult to convert to binary
> - **16 = 2⁴**, so each hex digit maps to exactly **4 binary bits** → easy conversion!

### Hex-Binary Quick Reference Table

| Hex | Binary | | Hex | Binary |
|-----|--------|-|-----|--------|
| 0   | 0000   | | 8   | 1000   |
| 1   | 0001   | | 9   | 1001   |
| 2   | 0010   | | A   | 1010   |
| 3   | 0011   | | B   | 1011   |
| 4   | 0100   | | C   | 1100   |
| 5   | 0101   | | D   | 1101   |
| 6   | 0110   | | E   | 1110   |
| 7   | 0111   | | F   | 1111   |

> [!warning] Common Student Mistake
> Confusing hex digits A-F with their decimal values. **A=10, B=11, C=12, D=13, E=14, F=15**. Don't treat them as 1-digit numbers in calculations!

---

## 2. Conversion Between Number Systems

### 2.1 Binary → Decimal
**Method:** Multiply each bit by its positional power of 2, then sum.

> **Example:** Convert `1110₂` to decimal
> 1×2³ + 1×2² + 1×2¹ + 0×2⁰ = 8 + 4 + 2 + 0 = **14₁₀**

### 2.2 Decimal → Binary
**Method:** Repeated division by 2, read remainders **bottom to top**.

> **Example:** Convert `25₁₀` to binary
> ```
> 25 ÷ 2 = 12  remainder 1  ↑
> 12 ÷ 2 = 6   remainder 0  ↑
> 6  ÷ 2 = 3   remainder 0  ↑
> 3  ÷ 2 = 1   remainder 1  ↑
> 1  ÷ 2 = 0   remainder 1  ↑
> ```
> Answer: **11001₂**

> [!warning] Common Student Mistake
> Reading remainders top-to-bottom instead of **bottom-to-top**! Always reverse the order of remainders.

### 2.3 Hexadecimal → Decimal
**Method:** Multiply each hex digit (converted to decimal) by positional power of 16.

> **Example:** Convert `589₁₆` to decimal
> 5×16² + 8×16¹ + 9×16⁰ = 1280 + 128 + 9 = **1417₁₀**

### 2.4 Decimal → Hexadecimal
**Method:** Repeated division by 16, read remainders bottom to top.

> **Example:** Convert `415₁₀` to hex
> ```
> 415 ÷ 16 = 25  remainder 15 (F)  ↑
> 25  ÷ 16 = 1   remainder 9   ↑
> 1   ÷ 16 = 0   remainder 1   ↑
> ```
> Answer: **19F₁₆**

### 2.5 Hex → Binary
**Method:** Replace each hex digit with its 4-bit binary equivalent.

> **Example:** Convert `39A2₁₆` to binary
> ```
> 3    9    A    2
> 0011 1001 1010 0010
> ```
> Answer: **0011100110100010₂**

### 2.6 Binary → Hex
**Method:** Group bits into sets of 4 **from right to left**, then convert each group.

> **Example:** Convert `1000011001000011₂` to hex
> ```
> 1000   0110   0100   0011
> 8      6      4      3
> ```
> Answer: **8643₁₆**

> [!warning] Common Student Mistake
> When grouping binary into 4-bit chunks for hex, always group **from right to left**. If the leftmost group has fewer than 4 bits, **pad with leading zeros**.

> [!danger] Exam Hotspot
> Conversion questions are **GUARANTEED** to appear. Practice all 6 directions. The exam may ask you to convert in any direction, including chained conversions (e.g., binary → hex → decimal).

---

## 3. Addition and Subtraction

### 3.1 Hex Addition

**Key Rule:** When sum ≥ 16₁₀, write (sum - 16) and carry 1.

> **Example:** `5B39₁₆ + 7AF4₁₆`
> ```
>   5 B 3 9
> + 7 A F 4
> ---------
>   D 6 2 D
> ```
> - 9+4 = 13₁₀ = **D** (no carry)
> - 3+F = 3+15 = 18₁₀ = 16₁₀+2 → write **2**, carry **1**
> - B+A+1 = 11+10+1 = 22₁₀ = 16₁₀+6 → write **6**, carry **1**
> - 5+7+1 = 13₁₀ = **D**

> [!warning] Common Student Mistake
> Forgetting the carry in hex addition! When the sum of a column is ≥ 16, you MUST carry 1 to the next column. Also, remember that carries are in hex (16₁₀), not decimal (10₁₀).

### 3.2 Binary Addition

**Rules:**
| A | B | Carry In | Sum | Carry Out |
|---|---|----------|-----|-----------|
| 0 | 0 | 0        | 0   | 0         |
| 0 | 1 | 0        | 1   | 0         |
| 1 | 0 | 0        | 1   | 0         |
| 1 | 1 | 0        | 0   | 1         |
| 1 | 1 | 1        | 1   | 1         |
| 0 | 1 | 1        | 0   | 1         |
| 1 | 0 | 1        | 0   | 1         |
| 0 | 0 | 1        | 1   | 0         |

> **Example:** `100101111₂ + 110110₂`
> ```
>   100101111
> + 000110110  (pad with leading zeros)
> -----------
>   101100101
> ```

> [!warning] Common Student Mistake
> Forgetting to **pad with leading zeros** on the smaller number before adding. Always align numbers to the same length.

### 3.3 Hex Subtraction

**Key Rule:** When top digit < bottom digit, **borrow 1** from the next column (which equals 16₁₀ in that position).

> **Example:** `D26F₁₆ - BA94₁₆`
> ```
>   D 2 6 F
> - B A 9 4
> ---------
>   1 7 D B
> ```
> - F-4 = 11₁₀ = **B**
> - 6 < 9 → borrow: (6+16)-9 = 22-9 = 13₁₀ = **D**
> - 2 becomes 1 (after borrow): (1+16)-A-1 = 18-10-1 = 7 → **7**
>   Wait, actually: 12₁₆ - A₁₆ - 1(borrow) = 18₁₀ - 10₁₀ - 1₁₀ = 7₁₀ = **7**
> - D becomes C (after borrow): C-B-1 = 12-11-1 = 0 → **1** (recalculated in slides as 1)
>   Actually: Dh - Bh - 1(borrow) = 13-11-1 = 1₁₀ = **1**

> [!danger] Exam Hotspot
> Hex and binary subtraction with borrowing is where **most students lose marks**. Practice extensively. The slide shows: `D26F - BA94 = 17DB`.

### 3.4 Binary Subtraction

Same principle: borrow = 2 in binary (since base is 2).

> **Example:** `11011₂ - 10110₂`
> ```
>   11011
> - 10110
> -------
>   00101
> ```

> [!danger] Exam Hotspot
> You will definitely get at least one addition AND one subtraction problem. Could be hex or binary. Know both!

---

## 4. Integer Representation in Computer

### 4.1 Key Terminology
| Term | Meaning |
|------|---------|
| **LSB** | Least Significant Bit - rightmost bit (bit 0) |
| **MSB** | Most Significant Bit - leftmost bit (bit 15 for 16-bit) |
| **Byte** | 8 bits |
| **Word** | 16 bits (in 8086 context) |

> [!tip] Quick Rule
> If **LSB = 1** → number is **ODD**. If **LSB = 0** → number is **EVEN**.

### 4.2 Unsigned Integers
- Non-negative only (0 and positive)
- **Largest unsigned byte:** `11111111₂ = 255₁₀ = FF₁₆`
- **Largest unsigned word:** `1111111111111111₂ = 65535₁₀ = FFFF₁₆`

### 4.3 Signed Integers
- Can be positive or negative
- **MSB is the sign bit:**
  - MSB = 0 → **Positive**
  - MSB = 1 → **Negative**
- Negative integers stored using **Two's Complement**

### 4.4 One's Complement
- **Method:** Flip every bit (0→1, 1→0)
- Example: `5 = 0000000000000101₂`
- One's complement: `1111111111111010₂`

> [!warning] Common Student Mistake
> One's complement is NOT the same as Two's complement! One's complement = just flip bits. Two's complement = flip bits + 1.

### 4.5 Two's Complement
- **Method:** One's Complement + 1
- Example: `5 = 0000000000000101₂`
  - One's complement: `1111111111111010₂`
  - Add 1: `1111111111111011₂` ← This is -5 in two's complement

> [!important] Key Property of Two's Complement
> If you add a number N and its two's complement (-N), the result is **0** (with the carry bit overflowing and being lost).
>
> Example: `5 + (-5)` in 16-bit:
> ```
>   1111111111111011   (-5 in two's complement)
> + 0000000000000101   (5)
> = 10000000000000000  (17 bits - MSB carry is LOST)
>   → 0000000000000000 = 0  ✓
> ```

> [!important] Another Key Property
> - Adding N + One's Complement of N = **all 1s** (16 ones for 16-bit)
> - Adding N + Two's Complement of N = **all 0s** (16 zeros for 16-bit)

### 4.6 Subtraction Using Two's Complement Addition

**Method:** `A - B = A + (Two's Complement of B)`

> **Example:** AX = 21FCh, BX = 5ABCh, find AX - BX
> 1. AX = `0010000111111100₂`
> 2. BX = `0101101010111100₂`
> 3. One's complement of BX = `1010010101000011₂`
> 4. Two's complement of BX = `1010010101000100₂` = A544₁₆
> 5. AX + (Two's complement of BX) = 21FCh + A544h = **C740h**

> [!danger] Exam Hotspot
> Two's complement questions are the **most frequently tested** topic. Expect:
> - Find two's complement of a given number
> - Represent a signed decimal in 8-bit or 16-bit two's complement
> - Express result in hex
> - Perform subtraction using two's complement addition
>
> **Practice these tasks from the slides:**
> - Find two's complement of -97, -120, -40000, -128, 65536 in 8-bit and 16-bit
> - 16-bit representation of 234, -16, 31634, -32216 in hex

> [!warning] Common Student Mistake
> - Not extending to the required bit-width before taking complement (always write the full 8 or 16 bits first)
> - Forgetting that the MSB is the sign bit
> - Getting confused about overflow when a number can't fit in the given bits (e.g., -40000 or 65536 in 16-bit)

---

## 5. ASCII Code

### 5.1 Key Facts
- ASCII uses **7 bits** → 2⁷ = **128 characters**
- Codes **32 to 126** (95 characters) are **printable**
- Codes 0-31 and 127 are **non-printable** (control characters)

### 5.2 Important ASCII Values to Remember

| Character | ASCII (Dec) | ASCII (Hex) | ASCII (Binary) |
|-----------|-------------|-------------|----------------|
| '0'       | 48          | 30          | 0110000        |
| '9'       | 57          | 39          | 0111001        |
| 'A'       | 65          | 41          | 1000001        |
| 'Z'       | 90          | 5A          | 1011010        |
| 'a'       | 97          | 61          | 1100001        |
| 'z'       | 122         | 7A          | 1111010        |
| Space     | 32          | 20          | 0100000        |

> [!tip] Memory Trick
> - Uppercase A-Z: **65-90** (41h-5Ah)
> - Lowercase a-z: **97-122** (61h-7Ah)
> - Difference between 'A' and 'a' = **32** (20h) → just flip bit 5!

### 5.3 String in Memory
Characters are stored **sequentially** in memory, one byte per character.

> **Example:** `"RG 2z"` in memory:
> | Address | Character | ASCII (Dec) | Binary |
> |---------|-----------|-------------|--------|
> | 0       | R         | 82          | 01010010 |
> | 1       | G         | 71          | 01000111 |
> | 2       | Space     | 32          | 00100000 |
> | 3       | 2         | 50          | 00110010 |
> | 4       | z         | 122         | 01111010 |

> [!danger] Exam Hotspot
> You may be asked to show how a string like `"Hello World"` would be stored in memory. You need to:
> 1. Know the ASCII code for each character
> 2. Show sequential memory addresses
> 3. Express in hex or binary as requested

---

## Exam Strategy & Prediction

### Question Types Expected:

| Question Type | Likelihood | Marks (est.) |
|--------------|------------|---------------|
| Number system conversion (any direction) | **100%** | 5-10 |
| Hex/Binary Addition | **100%** | 5-8 |
| Hex/Binary Subtraction | **100%** | 5-8 |
| Two's Complement problems | **100%** | 8-12 |
| Signed integer representation (8/16-bit) | **Very High** | 5-10 |
| Subtraction via two's complement addition | **High** | 5-8 |
| ASCII / String in memory | **Moderate** | 3-5 |

### Key Formulas / Shortcuts to Memorize

```
# Decimal to Binary: divide by 2, read remainders BOTTOM to TOP
# Decimal to Hex: divide by 16, read remainders BOTTOM to TOP
# Hex to Binary: each hex digit → 4 binary bits
# Binary to Hex: group 4 bits from RIGHT to LEFT
# One's complement: flip all bits
# Two's complement: flip all bits + 1
# Subtraction via two's complement: A - B = A + (~B + 1)
# Largest unsigned byte: FF₁₆ = 255₁₀
# Largest unsigned word: FFFF₁₆ = 65535₁₀
```

### Practice Checklist
- [ ] Can convert between all 6 pairs (dec↔bin, dec↔hex, bin↔hex)
- [ ] Can do hex addition with carries
- [ ] Can do binary addition with carries
- [ ] Can do hex subtraction with borrows
- [ ] Can do binary subtraction with borrows
- [ ] Can find one's and two's complement
- [ ] Can represent signed integers in 8-bit and 16-bit two's complement
- [ ] Can express results in hex as required
- [ ] Can perform subtraction using two's complement addition
- [ ] Can write ASCII codes for common characters
- [ ] Can show string storage in memory

---

> [!quote] Final Tip
> This lecture is **purely calculation-based**. The more you practice, the faster and more accurate you'll be. Focus on TWO'S COMPLEMENT and CONVERSIONS — they carry the most marks.
