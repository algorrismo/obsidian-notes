tags : #COA 
date : 2026-07-02

---
# NUMBER SYSTEM CONVERSIONS - QUICK REFERENCE CARD

## Keep this beside you while studying!

---

## **MEMORIZE THESE FIRST**

### Powers of 2 (for binary)

```
2⁰=1    2¹=2    2²=4    2³=8    2⁴=16   2⁵=32   2⁶=64   2⁷=128   2⁸=256
```

### Powers of 16 (for hex)

```
16⁰=1    16¹=16    16²=256    16³=4096
```

### Hex Digits

```
0-9 stay same
A=10  B=11  C=12  D=13  E=14  F=15
```

### Hex-Binary Mapping (MOST IMPORTANT!)

```
0=0000  1=0001  2=0010  3=0011  4=0100  5=0101  6=0110  7=0111
8=1000  9=1001  A=1010  B=1011  C=1100  D=1101  E=1110  F=1111
```

---

## **THE 6 CONVERSIONS - QUICK METHODS**

### **1️⃣ BINARY → DECIMAL**

**Method:** Add up powers of 2

**Steps:**

1. Write powers of 2 above each digit (from right)
2. Add only the ones with "1" below them

**Example:** 10110

```
Powers: 16  8  4  2  1
Digits:  1  0  1  1  0
                 ↓  ↓  ↓
Sum: 16 + 4 + 2 = 22 ✓
```

---

### **2️⃣ DECIMAL → BINARY**

**Method:** Divide by 2, keep remainders, read bottom-up

**Steps:**

1. Divide number by 2
2. Write remainder (0 or 1)
3. Take quotient, divide by 2 again
4. Repeat until quotient = 0
5. Read remainders BOTTOM→TOP

**Example:** 22

```
22 ÷ 2 = 11 r 0  ←── Read from here!
11 ÷ 2 = 5  r 1     ↑
5  ÷ 2 = 2  r 1     ↑
2  ÷ 2 = 1  r 0     ↑
1  ÷ 2 = 0  r 1  ←── Start from here!

Answer: 10110 ✓
```

---

### **3️⃣ HEX → DECIMAL**

**Method:** Add up powers of 16 (same as binary but use 16!)

**Steps:**

1. Write powers of 16 above each digit (from right)
2. Convert each hex digit to decimal (A=10, B=11, etc.)
3. Multiply digit × its power
4. Add all results

**Example:** 2A5

```
Powers: 256  16   1
Digits:  2    A   5
Hex→Dec: 2   10   5

Calc: 2×256 + 10×16 + 5×1
    = 512 + 160 + 5
    = 677 ✓
```

---

### **4️⃣ DECIMAL → HEX**

**Method:** Divide by 16, keep remainders, read bottom-up (convert ≥10 to letters!)

**Steps:**

1. Divide number by 16
2. Write remainder (if ≥10, convert to A-F)
3. Take quotient, divide by 16 again
4. Repeat until quotient = 0
5. Read remainders BOTTOM→TOP

**Example:** 677

```
677 ÷ 16 = 42 r 5    ←── Read from here!
42  ÷ 16 = 2  r 10→A    ↑
2   ÷ 16 = 0  r 2   ←── Start here!

Answer: 2A5 ✓
```

---

### **5️⃣ HEX → BINARY**

**Method:** Each hex digit = 4 binary digits (NO DECIMAL NEEDED!) ⭐

**Steps:**

1. Convert each hex digit to its 4-bit binary equivalent
2. Combine all groups
3. Remove leading zeros (optional)

**Example:** 2A5

```
Hex: 2    A    5
     ↓    ↓    ↓
Bin: 0010 1010 0101
     └────────────┘
Combined: 001010100101
Cleaned:  1010100101 ✓
```

**Another Example:** 1F

```
Hex: 1    F
     ↓    ↓
Bin: 0001 1111
     └─────────┘
Combined: 00011111
Cleaned:  11111 ✓
```

---

### **6️⃣ BINARY → HEX**

**Method:** Group into 4s from RIGHT, convert each group (NO DECIMAL NEEDED!) ⭐

**Steps:**

1. **GROUP from RIGHT into groups of 4**
2. Add leading zeros if needed
3. Convert each 4-bit group to hex digit

**Example:** 1010100101

```
Group from right:
0010 1010 0101
  ↓    ↓    ↓
  2    A    5

Answer: 2A5 ✓
```

**Another Example:** 11111

```
Pad and group from right:
0001 1111
  ↓    ↓
  1    F

Answer: 1F ✓
```

---

## **DECISION TREE: "What do I need to do?"**

```
Read the problem:
├─ Binary input + Decimal output?  → USE METHOD 1
├─ Decimal input + Binary output?  → USE METHOD 2
├─ Hex input + Decimal output?     → USE METHOD 3
├─ Decimal input + Hex output?     → USE METHOD 4
├─ Hex input + Binary output?      → USE METHOD 5 ⭐ FAST!
└─ Binary input + Hex output?      → USE METHOD 6 ⭐ FAST!
```

---

## **IMPORTANT EXAM REMINDERS**

✅ **Always verify your answer** by converting back:

```
22 (decimal) → 10110 (binary) → verify by checking powers
10110 → 16+4+2 = 22 ✓
```

✅ **Division method is foolproof:**

- Always divide by 2 for binary
- Always divide by 16 for hex
- Always read remainders BOTTOM→TOP

✅ **Hex↔Binary is THE FASTEST:**

- Don't convert to decimal as intermediate!
- Just use the 16-digit mapping table
- Saves 2-3 minutes per conversion

✅ **Write clearly during exam:**

```
GOOD:
22 ÷ 2 = 11 r 0
11 ÷ 2 = 5  r 1
5  ÷ 2 = 2  r 1
2  ÷ 2 = 1  r 0
1  ÷ 2 = 0  r 1
Answer: 10110

BAD: (messy, hard to read)
```

✅ **Remainders must be 0 or 1 (for binary), 0-15 (for hex):**

- If remainder > base, you did division wrong!

✅ **Leading zeros don't matter (usually):**

```
00010110 = 10110 = same value
```

---

## **COMMON MISTAKES TO AVOID**

|Mistake|Why Wrong|How to Fix|
|---|---|---|
|Reading division remainders TOP→BOTTOM|They go backwards!|Always read BOTTOM→TOP|
|Forgetting to convert remainders in hex (10→A, etc.)|Incomplete answer|Have the mapping table ready|
|Grouping binary from LEFT instead of RIGHT|Wrong grouping = wrong answer|ALWAYS group from RIGHT|
|Using decimal as intermediate for hex↔binary|Wastes time in exam|Use direct 4-bit conversion|
|Not memorizing powers|Calculating them takes forever|Spend 10 min now, save 20 min in exam|
|Mixing up 2³ and 3²|Basic careless error|Double-check: 2³ = 2×2×2 = 8|

---

## **PRACTICE PROBLEMS WITH ANSWERS**

### Quick Drills (1-2 min each)

|Problem|Answer|Method|
|---|---|---|
|1010 (bin) → dec|10|Powers: 8+2|
|15 (dec) → bin|1111|Divide: 15,7,3,1,0|
|20 (hex) → dec|32|Powers: 2×16|
|64 (dec) → hex|40|Divide: 64÷16=4r0|
|FF (hex) → bin|11111111|Direct: F=1111 twice|
|10101010 (bin) → hex|AA|Group: 1010,1010|
|255 (dec) → bin|11111111|Powers: all 1s below|
|256 (dec) → hex|100|Divide: 256÷16=16r0; 16÷16=1r0; 1÷16=0r1|

---

## **EXAM TIME MANAGEMENT**

If you have 6 conversions to do:

```
Hex↔Binary conversions: 1 min each × 2 = 2 min (FASTEST!)
Decimal↔Binary conversions: 2-3 min each × 2 = 5 min
Decimal↔Hex conversions: 2-3 min each × 2 = 5 min

Total: ~12 min for all 6 types (leaves buffer for verification)
```

---

## **LAST-MINUTE CHEAT: POWERS TABLE**

```
Binary:        Hex:
2⁰ = 1         16⁰ = 1
2¹ = 2         16¹ = 16
2² = 4         16² = 256
2³ = 8         16³ = 4096
2⁴ = 16        16⁴ = 65536
2⁵ = 32
2⁶ = 64
2⁷ = 128
2⁸ = 256
2⁹ = 512
2¹⁰ = 1024
```

---

**Print this card. Keep it. Love it. 🎓**