tags : #COA 
created : 2026-07-02

# Number System Conversions - Complete Guide for COA

## A Senior Professor's Approach to Understanding Bases

---

## **PART 0: THE FOUNDATION - Understand Positional Notation FIRST**

Before we do ANY conversion, understand this universal principle:

```
Any number = Sum of (digit × base^position)

Positions count from RIGHT to LEFT, starting at 0
```

### Example in Decimal (Base 10):

```
Number: 325 (in decimal)
= 3×10² + 2×10¹ + 5×10⁰
= 3×100 + 2×10 + 5×1
= 300 + 20 + 5
= 325
```

### Example in Binary (Base 2):

```
Number: 1011 (in binary)
= 1×2³ + 0×2² + 1×2¹ + 1×2⁰
= 1×8 + 0×4 + 1×2 + 1×1
= 8 + 0 + 2 + 1
= 11 (in decimal)
```

### Example in Hexadecimal (Base 16):

```
Number: 2A5 (in hexadecimal)
A = 10, so:
= 2×16² + 10×16¹ + 5×16⁰
= 2×256 + 10×16 + 5×1
= 512 + 160 + 5
= 677 (in decimal)
```

**KEY INSIGHT:** All conversions ultimately use this principle!

---

## **PART 1: BINARY TO DECIMAL** ✓

### **Method: Use the positional notation principle**

**Steps:**

1. Write down powers of 2 from right to left (2⁰, 2¹, 2², 2³, 2⁴, 2⁵...)
2. Multiply each binary digit by its corresponding power
3. Add all results

**Memorize these powers of 2 (saves time in exam):**

```
2⁰ = 1
2¹ = 2
2² = 4
2³ = 8
2⁴ = 16
2⁵ = 32
2⁶ = 64
2⁷ = 128
2⁸ = 256
2⁹ = 512
2¹⁰ = 1024
```

### **Example 1: Convert 10110 to Decimal**

```
Binary: 1 0 1 1 0
         │ │ │ │ └─ Position 0: 0 × 2⁰ = 0 × 1  = 0
         │ │ │ └─── Position 1: 1 × 2¹ = 1 × 2  = 2
         │ │ └───── Position 2: 1 × 2² = 1 × 4  = 4
         │ └─────── Position 3: 0 × 2³ = 0 × 8  = 0
         └───────── Position 4: 1 × 2⁴ = 1 × 16 = 16

Sum: 16 + 0 + 4 + 2 + 0 = 22
```

### **Example 2: Convert 11001101 to Decimal**

```
Binary: 1 1 0 0 1 1 0 1
Powers: 2⁷ 2⁶ 2⁵ 2⁴ 2³ 2² 2¹ 2⁰
        128 64 32 16 8  4  2  1

Calculation:
1×128 + 1×64 + 0×32 + 0×16 + 1×8 + 1×4 + 0×2 + 1×1
= 128 + 64 + 8 + 4 + 1
= 205
```

### **Quick Tip for Exam:**

Just write the powers of 2 above each position, then only add the columns with 1:

```
Binary: 1 0 1 1 0
        16 8 4 2 1
              ↑ ↑ ↑
          Sum: 16 + 4 + 2 = 22 ✓
```

---

## **PART 2: DECIMAL TO BINARY** 🔄

### **Method: DIVISION METHOD (Most reliable)**

**Steps:**

1. Divide the decimal number by 2
2. Write down the remainder (0 or 1)
3. Divide the quotient by 2 again
4. **Repeat until quotient becomes 0**
5. **Read remainders BOTTOM TO TOP**

### **Example 1: Convert 22 to Binary**

```
22 ÷ 2 = 11 remainder 0  ←─┐
11 ÷ 2 = 5  remainder 1    │
5  ÷ 2 = 2  remainder 1    │
2  ÷ 2 = 1  remainder 0    │
1  ÷ 2 = 0  remainder 1    │
                           │
Read this way (BOTTOM→TOP)─┘

Answer: 10110 ✓

Verify: 1×16 + 0×8 + 1×4 + 1×2 + 0×1 = 16+4+2 = 22 ✓
```

### **Example 2: Convert 205 to Binary**

```
205 ÷ 2 = 102 remainder 1  ↑ Read from here
102 ÷ 2 = 51  remainder 0  │
51  ÷ 2 = 25  remainder 1  │
25  ÷ 2 = 12  remainder 1  │
12  ÷ 2 = 6   remainder 0  │
6   ÷ 2 = 3   remainder 0  │
3   ÷ 2 = 1   remainder 1  │
1   ÷ 2 = 0   remainder 1  ↑

Answer: 11001101 ✓

Verify: 128+64+8+4+1 = 205 ✓
```

### **Why This Method?**

Binary inherently asks "Is there a 2ⁿ in this number?" Division by 2 answers exactly that!

---

## **PART 3: HEXADECIMAL TO DECIMAL** ↓

### **Method: Use positional notation (same as binary)**

**First, memorize hex digits:**

```
0-9 = 0-9
A = 10
B = 11
C = 12
D = 13
E = 14
F = 15
```

**Memorize these powers of 16:**

```
16⁰ = 1
16¹ = 16
16² = 256
16³ = 4,096
16⁴ = 65,536
```

### **Example 1: Convert 2A5 to Decimal**

```
Hex:  2   A   5
      │   │   └─ Position 0: 5 × 16⁰ = 5 × 1   = 5
      │   └───── Position 1: A × 16¹ = 10 × 16 = 160
      └───────── Position 2: 2 × 16² = 2 × 256 = 512

Sum: 512 + 160 + 5 = 677
```

### **Example 2: Convert 1F3 to Decimal**

```
Hex:  1   F   3
      │   │   └─ Position 0: 3 × 16⁰ = 3 × 1   = 3
      │   └───── Position 1: F × 16¹ = 15 × 16 = 240
      └───────── Position 2: 1 × 16² = 1 × 256 = 256

Sum: 256 + 240 + 3 = 499
```

### **Example 3: Convert ABC to Decimal**

```
Hex:  A   B   C
      │   │   └─ Position 0: C × 16⁰ = 12 × 1   = 12
      │   └───── Position 1: B × 16¹ = 11 × 16  = 176
      └───────── Position 2: A × 16² = 10 × 256 = 2,560

Sum: 2,560 + 176 + 12 = 2,748
```

---

## **PART 4: DECIMAL TO HEXADECIMAL** 🔄

### **Method: DIVISION METHOD (same concept as binary)**

**Steps:**

1. Divide decimal by 16
2. Write down the **remainder** (convert to hex digit if ≥10)
3. Repeat until quotient = 0
4. **Read remainders BOTTOM TO TOP**

### **Example 1: Convert 677 to Hexadecimal**

```
677 ÷ 16 = 42 remainder 5    ↑
42  ÷ 16 = 2  remainder 10→A │ Read from here
2   ÷ 16 = 0  remainder 2    ↑

Answer: 2A5 ✓

Verify: 2×256 + 10×16 + 5 = 512+160+5 = 677 ✓
```

### **Example 2: Convert 255 to Hexadecimal**

```
255 ÷ 16 = 15 remainder 15→F ↑
15  ÷ 16 = 0  remainder 15→F ↑

Answer: FF ✓

Verify: 15×16 + 15 = 240+15 = 255 ✓
```

### **Example 3: Convert 2748 to Hexadecimal**

```
2748 ÷ 16 = 171 remainder 12→C  ↑
171  ÷ 16 = 10  remainder 11→B  │
10   ÷ 16 = 0   remainder 10→A  ↑

Answer: ABC ✓

Verify: 10×256 + 11×16 + 12 = 2560+176+12 = 2748 ✓
```

---

## **PART 5: HEXADECIMAL TO BINARY** 🎯 (The Easy Shortcut!)

### **Method: DIRECT CONVERSION (No decimal needed)**

**Key Insight:** Each hex digit = exactly 4 binary digits!

**Memorize this table:**

```
HEX → BINARY
0   → 0000
1   → 0001
2   → 0010
3   → 0011
4   → 0100
5   → 0101
6   → 0110
7   → 0111
8   → 1000
9   → 1001
A   → 1010
B   → 1011
C   → 1100
D   → 1101
E   → 1110
F   → 1111
```

### **Example 1: Convert 2A5 to Binary**

```
Hex:     2    A    5
Binary: 0010 1010 0101

Combine: 001010100101

Clean up (remove leading zero): 1010100101
```

### **Example 2: Convert ABC to Binary**

```
Hex:     A    B    C
Binary: 1010 1011 1100

Combine: 101010111100
```

### **Example 3: Convert 1F to Binary**

```
Hex:     1    F
Binary: 0001 1111

Combine: 00011111

Clean up: 11111
```

---

## **PART 6: BINARY TO HEXADECIMAL** 🎯 (Also Easy!)

### **Method: GROUP INTO 4s FROM RIGHT**

**Steps:**

1. Group binary digits into groups of 4 **from RIGHT to LEFT**
2. Add leading zeros if needed
3. Convert each group to hex digit

### **Example 1: Convert 1010100101 to Hexadecimal**

```
Binary: 1010100101

Group from right (pad with zeros):
0010 1010 0101
  ↓    ↓    ↓
  2    A    5

Answer: 2A5 ✓
```

### **Example 2: Convert 11111 to Hexadecimal**

```
Binary: 11111

Group from right (pad with zeros):
0001 1111
  ↓    ↓
  1    F

Answer: 1F ✓
```

### **Example 3: Convert 101010111100 to Hexadecimal**

```
Binary: 101010111100

Group from right (already 12 digits = 3 groups):
1010 1011 1100
  ↓    ↓    ↓
  A    B    C

Answer: ABC ✓
```

---

## **DECISION FLOWCHART: When to Use What?**

```
┌─────────────────────────────────────────────────┐
│  What conversion do I need?                     │
└──────────────────┬──────────────────────────────┘
                   │
        ┌──────────┼──────────┬──────────┐
        │          │          │          │
        ▼          ▼          ▼          ▼
    BINARY→     BINARY→    HEX→       HEX→
    DECIMAL    BINARY     DECIMAL    BINARY
        │          │          │          │
        ▼          ▼          ▼          ▼
    Use powers  Already   Use powers  Group
    of 2 and    binary!   of 16 and   into 4s
    add them    Group     multiply    Convert
                into 4s   and add     each
                          them        group
```

---

## **SUMMARY TABLE: All Methods at a Glance**

|From → To|Method|Key Trick|Time|
|---|---|---|---|
|**Binary → Decimal**|Powers of 2, multiply & add|Memorize: 1,2,4,8,16,32,64,128,256|2 min|
|**Decimal → Binary**|Divide by 2, read remainders bottom-up|Stop when quotient = 0|3 min|
|**Hex → Decimal**|Powers of 16, multiply & add|Memorize: 1,16,256,4096|2 min|
|**Decimal → Hex**|Divide by 16, read remainders bottom-up|Convert remainders ≥10 to letters|3 min|
|**Hex → Binary**|1 hex = 4 binary, memorize table|**NO decimal needed!**|1 min ⭐|
|**Binary → Hex**|Group into 4s from right, use table|Pad with leading zeros|1 min ⭐|

---

## **EXAM STRATEGY: What to Memorize**

### **Minimum Memorization:**

```
Powers of 2 (for binary):
1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024

Powers of 16 (for hex):
1, 16, 256, 4096

Hex-Binary table:
0-7 → 0000-0111 (straightforward)
8-F → 1000-1111 (just add 8 to 0-7 and flip leading bit)
```

### **Division Method (Universal):**

Just divide by base, keep remainders, read bottom-up!

---

## **PRACTICE PROBLEMS**

### Set 1: Binary ↔ Decimal

1. 11010 (binary) → decimal? **[Answer: 26]**
2. 45 (decimal) → binary? **[Answer: 101101]**
3. 10111 (binary) → decimal? **[Answer: 23]**
4. 100 (decimal) → binary? **[Answer: 1100100]**

### Set 2: Hex ↔ Decimal

5. 1C (hex) → decimal? **[Answer: 28]**
6. 256 (decimal) → hex? **[Answer: 100]**
7. 3F (hex) → decimal? **[Answer: 63]**
8. 1000 (decimal) → hex? **[Answer: 3E8]**

### Set 3: Hex ↔ Binary

9. FF (hex) → binary? **[Answer: 11111111]**
10. 10101010 (binary) → hex? **[Answer: AA]**
11. 7B (hex) → binary? **[Answer: 01111011]**
12. 11001100 (binary) → hex? **[Answer: CC]**

---

## **COMMON CONFUSION - SOLVED!**

### **Question: "When do I know which conversion to use?"**

**Answer:** Just read the problem!

- Binary input + Decimal output = **Part 1**
- Decimal input + Binary output = **Part 2**
- Hex input + Decimal output = **Part 3**
- Decimal input + Hex output = **Part 4**
- Hex input + Binary output = **Part 5** ⭐ (Fast!)
- Binary input + Hex output = **Part 6** ⭐ (Fast!)

### **Question: "Why is hex-to-binary easier than decimal?"**

**Answer:** Because 16 = 2⁴. Each hex digit is EXACTLY 4 binary digits. No division needed!

### **Question: "Can I convert hex↔binary directly without decimal?"**

**Answer:** YES! That's the whole point of Parts 5 & 6. This is the **FASTEST method in exams**.

### **Question: "Do I always need to memorize powers?"**

**Answer:** For speed, yes. But if you forget, you can derive them:

- 2⁵ = 2⁴ × 2 = 16 × 2 = 32
- 16³ = 16² × 16 = 256 × 16 = 4,096

---

## **FINAL EXAM CHECKLIST**

- [ ] Can I convert any binary to decimal in < 2 min?
- [ ] Can I convert any decimal to binary in < 3 min?
- [ ] Do I know the powers of 2 and 16 by heart?
- [ ] Can I use the hex-binary shortcut without thinking?
- [ ] Can I explain WHY division method works?
- [ ] Can I verify my answers by converting back?
- [ ] Do I know when remainder = 1 vs 0 in division?
- [ ] Can I distinguish between digits and remainders?

**If yes to all → You're ready! 🎓**

---

Good luck! Remember: **Understand the principle, not just the steps, and no conversion will confuse you again.**