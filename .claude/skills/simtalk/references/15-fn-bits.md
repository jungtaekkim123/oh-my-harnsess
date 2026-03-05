> **Read this when:** Bit manipulation: `BitAND`, `BitOR`, `BitXOR`, `BitSet`, `BitTest`, `BitShift`, `BitClear`  
> **Skip this when:** Any non-bitwise operation

## Functions for Manipulating Individual Bits

### Functions for Manipulating Individual Bits
                manipulating individual bits of an integer value.

---

### BitAND
Executes a bitwise AND of value 1 and value 2 and returns the result.

Syntax

```
BitAND(Value1:integer, Value2:integer) → integer
```

Parameters

The parameter Value1 of data type integer designates value 1.

The parameter Value2 of data type integer designates value 2.

Return Value

The return value has the data type integer.

---

### BitClear
Changes the value of the parameter OriginalValue by setting the
bit with the number designated by the parameter BitPosition to the bit value
0. The function returns the result of this computation. 

Syntax

```
BitClear(OriginalValue:integer, BitPosition:integer) → integer
```

Parameters

The parameter OriginalValue of data type integer designates the original value
of the computation.

The parameter BitPosition of data type integer designates the bit position. The
value range for the bit position is 0 to 63. The least significant bit has the number 0, the most
significant bit has the number 63.

Return Value

The return value has the data type integer. 

See also

BitSet [SimTalk]

---

### BitOR
Executes a bitwise OR of value 1 and value 2 and returns the result.

Syntax

```
BitOR(Value1:integer, Value2:integer) → integer
```

Parameters

The parameter Value1 of data type integer designates value 1.

The parameter Value2 of data type integer designates value 2.

Return Value

The return value has the data type integer.

---

### BitSet
Changes the value of the parameter OriginalValue by setting the
bit with the number designated by the parameter BitPosition to the bit value
1. The function returns the result of this computation. 

Syntax

```
BitSet(OriginalValue:integer, BitPosition:integer) → integer
```

Parameters

The parameter OriginalValue of data type integer designates the original value
of the computation.

The parameter BitPosition of data type integer designates the bit position. The
value range for the bit position is 0 to 63. The least significant bit has the number 0, the most
significant bit has the number 63.

Return Value

The return value has the data type integer. 

See also

BitClear [SimTalk]

---

### BitShift
Shifts the bits of the value designated by the parameter integer
using the number of digits designated by integer and returns the result. 

Syntax

```
BitShift(Value:integer, NumberOfDigits:integer) → integer
```

Parameters

The parameter Value of data type integer designates the value.

The parameter NumberOfDigits of data type integer designates number of digits.
It moves them to the left, if you specified digits greater than 0. It moves them to the right, if
you specified digits smaller than 0.

Return Value

The return value has the data type integer.

---

### BitTest
Returns if in the Value the bit at the position designated by BitPosition is set (
`true`
) or not (
`false`
). 

Syntax

```
BitTest(Value:integer, BitPosition:integer) → boolean
```

Parameters

The parameter Value of data type integer designates the value.

The parameter BitPosition of data type integer designates the bit position. The
value range for the bit position is 0 to 63. The least significant bit has the number 0, the most
significant bit has the number 63.

Return Value

The return value has the data type boolean.

Example

```
var i : integer := 40 // binary representation: 00101000
print bitTest(i, 3)   // returns true because the bit 3 is set
```

---

### BitXOR
Executes a bitwise XOR of value 1 and value 2 and returns the result.

Syntax

```
BitXOR(Value1:integer, Value2:integer) → integer
```

Parameters

The parameter Value1 of data type integer designates value 1.

The parameter Value2 of data type integer designates value 2.

Return Value

The return value has the data type integer.

---
