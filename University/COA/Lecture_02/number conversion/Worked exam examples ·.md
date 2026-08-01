tags : #COA 
date : 2026-07-02

---
# WORKED EXAM EXAMPLES

## How a Professor Would Solve These (Step-by-Step)

---

## **SECTION A: BINARY → DECIMAL**

### Problem A1: Convert 11010 to decimal

**What the question is asking:** "In base 2, what does 11010 mean in base 10?"

**My approach as a professor:** Let me use the positional notation principle:

```
Step 1: Write the binary number with position markers
Binary:    1  1  0  1  0
Position:  4  3  2  1  0  ← (count from RIGHT, starting at 0)

Step 2: Write powers of 2 for each position
Position:  4    3    2    1    0
Power:     2⁴   2³   2²   2¹   2⁰
Value:     16   8    4    2    1

Step 3: Multiply each binary digit by its power
        1×16 + 1×8 + 0×4 + 1×2 + 0×1

Step 4: Add them up
        = 16 + 8 + 0 + 2 + 0
        = 26

ANSWER: 26 ✓
```

**How to verify (important!):** Convert back: 26 ÷ 2 = 13 r 0; 13 ÷ 2 = 6 r 1; 6 ÷ 2 = 3 r 0; 3 ÷ 2 = 1 r 1; 1 ÷ 2 = 0 r 1 Read bottom-up: 11010 ✓ Matches!

**Time taken:** ~90 seconds

---

### Problem A2: Convert 11111111 to decimal

**What the question is asking:** "What is this 8-bit number in decimal?"

**My approach:**

```
Step 1: Recognize the pattern
Binary: 1 1 1 1 1 1 1 1
All ones! This is a special case.

Step 2: Write powers
Powers: 128 64 32 16 8 4 2 1

Step 3: Since all digits are 1
Sum: 128 + 64 + 32 + 16 + 8 + 4 + 2 + 1

Step 4: Calculate
= 255

SMART OBSERVATION: With all 1s, just add all powers of 2!
Formula: 2ⁿ - 1 (for n-bit number with all 1s)
So: 2⁸ - 1 = 256 - 1 = 255 ✓

ANSWER: 255
```

**Time taken:** ~60 seconds (faster due to pattern recognition)

---

## **SECTION B: DECIMAL → BINARY**

### Problem B1: Convert 45 to binary

**What the question is asking:** "Break down 45 in terms of powers of 2"

**My approach (division method):**

```
Step 1: Divide by 2, note remainder
45 ÷ 2 = 22 remainder 1
         ↑ quotient  ↑ remainder

Step 2: Divide quotient by 2 again
22 ÷ 2 = 11 remainder 0

Step 3: Continue...
11 ÷ 2 = 5 remainder 1
5 ÷ 2 = 2 remainder 1
2 ÷ 2 = 1 remainder 0
1 ÷ 2 = 0 remainder 1
       ↑ STOP when quotient = 0

Step 4: Read remainders from BOTTOM to TOP
         ↑ Start here (last remainder)
45 ÷ 2 = 22 r 1
22 ÷ 2 = 11 r 0
11 ÷ 2 = 5  r 1
5  ÷ 2 = 2  r 1
2  ÷ 2 = 1  r 0
1  ÷ 2 = 0  r 1 ← Read from here
         ↓ Read this way (BOTTOM→TOP)

ANSWER: 101101 ✓

Verification: 32 + 8 + 4 + 1 = 45 ✓
              2⁵ + 2³ + 2² + 2⁰ ✓
```

**Common mistake to avoid:** Reading remainders TOP→BOTTOM would give: 101101 (reversed - WRONG!)

**Time taken:** ~2 minutes

---

### Problem B2: Convert 128 to binary

**What the question is asking:** "How do you write 128 in binary?"

**My approach:**

```
Step 1: Recognize that 128 = 2⁷
So binary should be 10000000

Step 2: Verify using division method:
128 ÷ 2 = 64 r 0
64  ÷ 2 = 32 r 0
32  ÷ 2 = 16 r 0
16  ÷ 2 = 8  r 0
8   ÷ 2 = 4  r 0
4   ÷ 2 = 2  r 0
2   ÷ 2 = 1  r 0
1   ÷ 2 = 0  r 1

Read bottom→top: 10000000 ✓

OBSERVATION: Powers of 2 in binary are 1 followed by zeros!
2¹ = 10, 2² = 100, 2³ = 1000, ... 2⁷ = 10000000 ✓

ANSWER: 10000000
```

**Time taken:** ~90 seconds

---

## **SECTION C: HEXADECIMAL → DECIMAL**

### Problem C1: Convert 1F to decimal

**What the question is asking:** "What does 1F in hex equal in decimal?"

**My approach:**

```
Step 1: Remember hex digit values
1 is just 1
F = 15 (memorize: A=10, B=11, C=12, D=13, E=14, F=15)

Step 2: Write positions and powers
Hex:      1    F
Position: 1    0
Power:    16¹  16⁰
Value:    16   1

Step 3: Multiply and add
1×16¹ + 15×16⁰ = 1×16 + 15×1 = 16 + 15 = 31

ANSWER: 31 ✓

Verification: 31 ÷ 16 = 1 remainder 15→F; 1 ÷ 16 = 0 remainder 1
Read: 1F ✓
```

**Time taken:** ~90 seconds

---

### Problem C2: Convert 3E8 to decimal

**What the question is asking:** "Convert this 3-digit hex number to decimal"

**My approach:**

```
Step 1: Identify hex digits
3 = 3
E = 14
8 = 8

Step 2: Set up powers of 16
Position: 2    1   0
Power:    16²  16¹ 16⁰
Value:    256  16  1

Hex digits: 3    E   8

Step 3: Multiply
3×256 + 14×16 + 8×1

Step 4: Calculate
768 + 224 + 8 = 1000

ANSWER: 1000 ✓

Cool fact: 1000 decimal = 3E8 hex (common in programming!)

Verification: 
1000 ÷ 16 = 62 r 8 (8)
62  ÷ 16 = 3  r 14→E (E)
3   ÷ 16 = 0  r 3 (3)
Read bottom→top: 3E8 ✓
```

**Time taken:** ~2 minutes

---

## **SECTION D: DECIMAL → HEXADECIMAL**

### Problem D1: Convert 255 to hexadecimal

**What the question is asking:** "Break down 255 in terms of powers of 16"

**My approach:**

```
Step 1: Divide by 16, note remainder (convert if ≥ 10)
255 ÷ 16 = 15 remainder 15
                     ↑ This is F in hex!

Step 2: Continue with quotient
15 ÷ 16 = 0 remainder 15
                  ↑ This is F in hex!
         ↑ STOP (quotient = 0)

Step 3: Read remainders from BOTTOM to TOP
255 ÷ 16 = 15 r 15→F
15  ÷ 16 = 0  r 15→F ← Read from here

Read bottom→top: FF

ANSWER: FF ✓

Verification: 15×16 + 15 = 240 + 15 = 255 ✓

OBSERVATION: 255 is 2⁸-1, the maximum 8-bit value
In binary: 11111111 = FF in hex ✓
```

**Time taken:** ~90 seconds

---

### Problem D2: Convert 1000 to hexadecimal

**What the question is asking:** "Convert this decimal number to hex (used in programming)"

**My approach:**

```
Step 1: Divide by 16
1000 ÷ 16 = 62 remainder 8
                       ↑ Keep this (8)

Step 2: Divide quotient by 16
62 ÷ 16 = 3 remainder 14
                   ↑ Convert to E

Step 3: Divide quotient by 16
3 ÷ 16 = 0 remainder 3
                 ↑ Keep this (3)
        ↑ STOP (quotient = 0)

Step 4: Read BOTTOM to TOP
1000 ÷ 16 = 62 r 8
62   ÷ 16 = 3  r 14→E
3    ÷ 16 = 0  r 3

Read bottom→top: 3E8

ANSWER: 3E8 ✓

Verification: 3×256 + 14×16 + 8 = 768 + 224 + 8 = 1000 ✓
```

**Important conversion note:** If remainder ≥ 10, convert it:

- 10 → A
- 11 → B
- 12 → C
- 13 → D
- 14 → E
- 15 → F

**Time taken:** ~2 minutes

---

## **SECTION E: HEXADECIMAL → BINARY (FAST!)**

### Problem E1: Convert 2A to binary

**What the question is asking:** "Convert this hex to binary (WITHOUT using decimal!)"

**My approach:**

```
Step 1: Use the hex→binary table (memorize this!)
0=0000, 1=0001, 2=0010, 3=0011, 4=0100, 5=0101, 6=0110, 7=0111
8=1000, 9=1001, A=1010, B=1011, C=1100, D=1101, E=1110, F=1111

Step 2: Convert each hex digit independently
Hex: 2      A
     ↓      ↓
Bin: 0010   1010

Step 3: Combine
00101010

Step 4: Clean up leading zeros (optional)
101010

ANSWER: 101010 ✓

Verification: 32+8+2 = 42 in decimal (if needed)
Or check hex: 2×16 + 10 = 42 ✓

WHY THIS IS FAST:
- No decimal conversion needed
- Just memorize the table
- 4 hex digits = 16 binary digits max
- Takes ~60 seconds for any hex number!
```

**Time taken:** ~60 seconds (FASTEST METHOD!)

---

### Problem E2: Convert F0F0 to binary

**What the question is asking:** "Convert this larger hex number to binary"

**My approach:**

```
Step 1: Each hex digit separately
F     0     F     0
↓     ↓     ↓     ↓
1111  0000  1111  0000

Step 2: Combine
11110000111100000

Step 3: That's already in binary form
(No leading zeros to remove)

ANSWER: 11110000111100000

Or if you want cleaner: 1111000011110000 (16 bits, 4 hex digits)

OBSERVATION: Hex is DESIGNED to map to binary in 4-bit chunks!
That's why it's used in computing - conversion is trivial!

Time taken: ~30 seconds (even faster - pattern recognition!)
```

**Time taken:** ~45 seconds

---

## **SECTION F: BINARY → HEXADECIMAL (FAST!)**

### Problem F1: Convert 10101010 to hexadecimal

**What the question is asking:** "Convert this binary to hex (WITHOUT using decimal!)"

**My approach:**

```
Step 1: Start from the RIGHT, group into 4s
10101010
  ↓   ↓
1010 1010

Step 2: Convert each 4-bit group to hex
Binary: 1010   1010
        ↓      ↓
Hex:    A      A

Step 3: Combine
AA

ANSWER: AA ✓

Verification: 10×16 + 10 = 170 in decimal
Or in binary: 128+32+8+2 = 170 ✓

WHY THIS IS FAST:
- No need for intermediate decimal
- Just group and look up in table
- Takes ~45 seconds for any binary!
```

**Time taken:** ~45 seconds (FASTEST!)

---

### Problem F2: Convert 11011001 to hexadecimal

**What the question is asking:** "Convert this 8-bit number to 2-digit hex"

**My approach:**

```
Step 1: Group from RIGHT into 4s
11011001
  ↓   ↓
1101 1001

Step 2: Convert each group
1101 = 1×8 + 1×4 + 0×2 + 1×1 = 8+4+1 = 13 → D
1001 = 1×8 + 0×4 + 0×2 + 1×1 = 8+1 = 9 → 9

Step 3: Combine
D9

ANSWER: D9 ✓

Verification: 13×16 + 9 = 208 + 9 = 217
Or in binary: 128+64+16+8+1 = 217 ✓

Note: For group 1101
- Remember: 8,4,2,1 are the powers of 2 in a 4-bit group
- 1101 means: yes, yes, no, yes = 8+4+1 = 13 = D
```

**Time taken:** ~60 seconds

---

### Problem F3: Convert 1001001 to hexadecimal

**What the question is asking:** "Convert 7-bit binary to hex"

**My approach:**

```
Step 1: Group from RIGHT, padding with zeros on LEFT
 1001001
← Pad with 0 to make groups of 4
0001001001

Group:
0001 1001

Step 2: Convert
0001 = 1
1001 = 9

Step 3: Combine
19

ANSWER: 19 ✓

Verification: 1×16 + 9 = 25
Or binary: 16+8+1 = 25 ✓

KEY RULE: Always group from RIGHT, add zeros on LEFT if needed!
This prevents mistakes from uneven grouping.
```

**Time taken:** ~60 seconds

---

## **EXAM SPEED COMPARISON**

|Conversion|Fastest Time|Method|
|---|---|---|
|Binary → Decimal|90 sec|Powers of 2|
|Decimal → Binary|2 min|Division by 2|
|Hex → Decimal|90 sec|Powers of 16|
|Decimal → Hex|2 min|Division by 16|
|**Hex → Binary**|**45 sec**|**Direct mapping**|
|**Binary → Hex**|**45 sec**|**Direct grouping**|

**Total time for all 6 types:** ~10-12 minutes **Time saved by using direct methods for last 2:** ~3-4 minutes!

---

## **FINAL PROFESSOR ADVICE**

### When you're stuck on a problem in exam:

1. **"I don't know what to do"** → Use division method (works for everything)
2. **"I'm running out of time"** → Skip to Hex↔Binary conversions (fastest)
3. **"I made an arithmetic error"** → Verify by converting back
4. **"The number is huge"** → Break into smaller groups (for binary/hex) or groups of digits
5. **"I forgot a power"** → Derive it: 2⁵ = 2⁴ × 2 = 16 × 2 = 32

### Success criteria:

- ✅ Can you do each conversion in < 3 minutes?
- ✅ Do you always verify your answers?
- ✅ Can you explain WHY each method works?
- ✅ Do you know when to use which method?
- ✅ Have you practiced at least 20 problems of each type?

---

**You've got this! The confusion disappears with practice. 🎓**