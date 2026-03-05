> **Read this when:** Array type, array creation, indexing, `append`, `contains`, `dim`, `sort`, `copy*`, array methods  
> **Skip this when:** Primitive types (see 07), JSON (see 09), or collections (see 10)


## Contents

- [Array](#array)
- [Add and Subtract Arrays of Numerical Data Types](#add-and-subtract-arrays-of-numerical-data-types)
- [Compare Arrays of Different Data Types](#compare-arrays-of-different-data-types)
- [Methods and Attributes of Arrays](#methods-and-attributes-of-arrays)
- [append - array](#append---array)
- [appendArray](#appendarray)
- [appendValueOfType](#appendvalueoftype)
- [asAny](#asany)
- [contains - array](#contains---array)
- [copyFromTable](#copyfromtable)
- [copyFromTableColumn](#copyfromtablecolumn)
- [copyToTable](#copytotable)
- [copyToTableColumn - array](#copytotablecolumn---array)
- [delete - array](#delete---array)
- [deleteValue](#deletevalue)
- [Dim - array](#dim---array)
- [Empty - array](#empty---array)
- [find - array](#find---array)
- [getValueOfType](#getvalueoftype)
- [insert - array](#insert---array)
- [join](#join)
- [Magnitude](#magnitude)
- [max - array](#max---array)
- [min - array](#min---array)
- [normalize](#normalize)
- [pop - array](#pop---array)
- [sort - array](#sort---array)
- [sum - array](#sum---array)
- [X - array](#x---array)
- [xDim - array](#xdim---array)
- [Y - array](#y---array)
- [yDim - array](#ydim---array)
- [Z - array](#z---array)

## Array
A local variable of data type array designates a
one-dimensional or a two-dimensional value field of one of the base data types listed under
Data Types.Remarks

Base data types for the array data
types are: 

Base data types can be all data types except for table,
list, stack, and queue.
If you type in any as the base data type, each item of the value field can
have a different data type. Then, even lists and tables can be placed in the array.
Array indexes are one-based, i.e., they start with 1, not with 0.
You can declare array variables as follows:
```
a : integer[10]
b : boolean[10,20]
a : string[]
```

Type a single number within the brackets to specify one-dimensional array of fixed size, for example 
```
a :
integer[10]
```
.

Type in two numbers within the brackets to specify a two-dimensional array of fixed size, for example 
```
b :
boolean[10,20]
```
.

Do not type any number at all within the brackets to specify a one-dimensional array, whose size is not fixed, and which is empty initially,
for example 
```
a : string[]
```
.

Compare this example: 
```
var vector3  : real[3]               // one-dimensional array with 3 real values 
var matrix3x3 : real[3,3]            // two-dimensional array with 9 real values 
var objList : object[]               // one-dimensional array with n objects (the size can change) 
var a        : any[]                 // one dimensional array with n values of any data type 
print vector3[2]                     // prints 0 to the console 
vector3 := [1.0, 2.0, 3.0]           // fills a one-dimensional array 
print vector3[2]                     // prints 2 to the console 

// For filling a two-dimensional array you might type:
for var x := 1 to matrix3x3.xDim
   for var y := 1 to matrix3x3.yDim
      matrix3x3[x,y] := x + y
next
next
print matrix3x3         // prints [2, 3, 4][3, 4, 5][4, 5, 6]

print objList.dim       // prints 0 to the console 
objList.append(Station) // adds Station to the array 
print objList.dim       // prints 1 to the console 
print objList[1]        // prints the path to the Station on the console 
a := vector3
a.append("Hello World")
print a.dim             // prints 4 in the console 
print a                 // prints [1, 2, 3, Hello World] to the console 
```

Plant Simulation displays empty arrays with a space
between the brackets like this 
```
"[ ]"
```
, compare the following
example:
```
var a : real[]
var s : string := to_str(a)  // s := "[ ]" 
`This example creates a nested array:`
-- array of two arrays
-- detect the datatype by the method isArray
var a:any[] := [[current, pi, exp(1)], [Eventcontroller, 42]]
print "a = ",a
print  "a[1] = ",a[1]
print  "a[2] = ",a[2]

-- datatype array
print isArray(a[1])
print isArray(a)
```

The Functions for Accessing 3D
Objects make extended use of the array data types.
The window Show Attributes and
Methods shows the value of an array in brackets, compare Show Methods.

Compare the sample models: Click the Window ribbon tab, click Start Page > Getting Started
> Example Models > Small Examples. Then, select the respective Category, the Topic, and the
Example in the dialog Examples
Collection, and click Open Model.

See also

Data Types [SimTalk]
Methods and Attributes of Arrays

isArray [SimTalk]

Print the Contents List to the Console as an Array

Use a Drag-and-Drop Control for Several Objects

---

## Add and Subtract Arrays of Numerical Data Types
            You can add and subtract arrays of numerical
                data types (integer, real, length, weight, speed, acceleration,
                    time) whose dimensions match. 
            In addition, you can multiply arrays of a
                floating point data type (real, length, weight, speed,
                    acceleration, time) with a numerical value (integer,
                    real) or divide them by a numerical value. We also support matrix multiplication for arrays of a floating point data type.
        
        See also
            
            Relational Operators

---

## Compare Arrays of Different Data Types
When comparing arrays of different data types, Plant Simulation throws a runtime error and opens the Method
Debugger in the following cases:

Arrays of data type real, length, time, speed, and weight based on their content.

Arrays of data type any are
compared to other arrays based on their content as well.

Note 
Arrays of data type integer
cannot be compared with arrays of data type real,
length, time, speed, or
weight.

Examples

```
-- arrays with different data types
var a:any[4]
-- array with different data types
a := [current, pi, -42, [1, 2, 3]]

print "a = ",a
print "a[1]: ", getSimTalkTypename(a[1])

a[1] := "Hello" -- change the data type
print "a[1]: ", getSimTalkTypename(a[1])
```

```
-- create, assign, compare arrays
var a:integer[3]

a[1] := 5
a[2] := 2
a[3] := 7
print "a = ",a

var b:integer[3]
print "b = ",b
b := a
print "b = ",b
print"a = b ", a=b
b.sort
print "b = ",b
print "a = b ", a=b
```

See also

Relational Operators

---

## Methods and Attributes of Arrays
Array data types provide these methods and attributes: 
| append [SimTalk] - array | deleteValue [SimTalk] | normalize [SimTalk] || appendArray [SimTalk] | Dim [SimTalk] - array | pop [SimTalk] - array || appendValueOfType [SimTalk] | Empty [SimTalk] - array | sort [SimTalk] - array || asAny [SimTalk] | find [SimTalk] - array | sum [SimTalk] - array || contains [SimTalk] - array | getValueOfType [SimTalk] | X [SimTalk] - array || copyFromTable [SimTalk] | insert [SimTalk] - array | xDim [SimTalk] - array || copyFromTableColumn [SimTalk] | join [SimTalk] | Y [SimTalk] - array || copyToTable [SimTalk] | Magnitude [SimTalk] | yDim [SimTalk] - array || copyToTableColumn [SimTalk] - array | max [SimTalk] - array | makeRGBValue [SimTalk] || delete [SimTalk] - array | min [SimTalk] - array |  |

See also

isArray [SimTalk]

---

## append - array
Appends the value designated by the parameter to the end of a one-dimensional array designated by <array> that does not have a fixed size.

Syntax

```
<array>.append(Value:any)
```

Parameter

The parameter Value of data type any designates the value that you want to
append. 

Example

```
var a: string[]
a.append("string")
a.append("string")
print a[2]
```

See also

appendArray [SimTalk]
join [SimTalk]

---

## appendArray
Appends all elements of the array passed as the parameter to the array designated by <array>. Remarks
The data types of the passed array and the existing array have to match. 
The method appendArray only applies to one-dimensional
arrays which do not have a fixed size.

Syntax

```
<array>.appendArray(ArrayToBeAppended:array)
```

Parameter

The parameter ArrayToBeAppended of data type array designates the array that is
to be appended to the existing array.

Example

```
var a : integer[]  := [1, 2, 3]
var b : integer[2] := [4, 5]
a.appendArray(b)
print a  // outputs [1, 2, 3, 4, 5]
```

See also

append [SimTalk] - array

---

## appendValueOfType
Converts the passed value to a byte sequence and appends these bytes at the end of an array of data type integer designated by <array>
whose size is not defined. Remarks

The method appendValueOfType is useful if you want to send binary data
with the object Socket.

Syntax

```
<array>.appendValueOfType(Value:any, Type:string)
```

Parameters

The parameter Value of data type any designates the value that you want to
append. 

The parameter Type of data type string designates the data type of the value
that you want to append. 
The passed value can be of data type integer, boolean, real,
length, time, speed, weight, or acceleration. The value
is converted to a byte sequence of a defined length where each byte has a value between 0 and
255.
The length depends on the value of the parameter Type. Allowed values for Type
are:
"int8", "int16", "int32", "int64", "uint8", "uint16", "uint32", "uint64", "real32", "real64",
"Int8", "Int16", "Int32", "Int64", "Uint8", "Uint16", "Uint32", "Uint64", "Real32", and
"Real64".
The number in the Type designates the number of bits, where 8 bits result in 1 byte.
"int16" for example converts the value to 2 bytes and appends these as 2 integer values to
the array.
The byte order of the byte sequence is determined by the first letter of the parameter
Type. 

If Type starts with a lower case letter, the byte sequence is created in little-endian
format.

If Type starts with an upper case letter, the byte sequence is created in big-endian
format.

Example

```
var a : integer[]
a.appendValueOfType(123456, "int32")  // append 4 bytes
a.appendValueOfType(-3000, "int16")   // append 2 bytes

var x := a.getValueOfType(1, "int32") // read 4 bytes
var y := a.getValueOfType(5, "int16") // read 2 bytes
```

See also

getValueOfType [SimTalk]
Socket

---

## asAny
Can be called for arrays of data type string and object designated by <array> and returns a reference
to the addressed array-element. Remarks
The method asAny returns a reference to the addressed array-element if its value is a relative or an absolute path to an existing
object or to an existing lane, storage place or to a user-defined attribute of data type table, list, stack or queue.

Syntax

```
<array>.asAny(Index:integer[, YIndex:integer]) → any
```

Parameters

The parameter Index of data type integer designates the index position of the
element in a one-dimensional array. 
If the array is two-dimensional, the parameter Index designates the
X-index-position (i.e., the column number) of the element.

Return Value

The parameter YIndex of data type integer designates the Y-index-position
(i.e., the row number) of the element in a two-dimensional array.

The return value has the data type object if the array element contains a
reference or a path to an existing object of type Frame.

The return value has the data type any if the array element contains the path
to a lane on a TwoLaneTrack or to a storage
place.

The return value has the data type table, list, stack or
queue respectively if the array element contains the path to a user-defined
attribute of data type table, list, stack or queue.

The return value is VOID if the value of the array element does not contain a path to a
valid object, or something similar.

Example

```
var a : object[2];
a[1] := "TwoLaneTrack.A"
a[2] := "Station.MyTableAttr"
var obj0 := a[1]        // obj0 is VOID, as not of type 'object'
var obj1 := a.asAny(1)  // obj1 is .Models.Model.TwoLaneTrack.A of type 'any'
var obj2 := a.asAny(2)  // obj2 is .Models.Model.Station.MeinTabellenAttr of type 'table'
```

See also

Lane A
Lane B
getRoute [SimTalk] - Transporter

---

## contains - array
  Returns if the specified value is contained in the array
    designated by <array> (true) or not (false). Remarks
      The method contains only applies to one-dimensional arrays.
    
    Syntax
      
```
<array>.contains(Value:any) → boolean
```

    
    Parameters
      
      The parameter Value of data type any designates the value which you would
        like to know if it is contained in the array.
    
    Return Value
      
      The return value has the data type boolean.
    
    Examples
      
```
var a : string[] := ["hello", "world"]
if a.contains("world")
   print "this code is always reached"
end
if a.contains("hell")
   print "this code is never reached"
end
```

```
param color : string := "yellow"
if ["red","green","blue"].contains(color)
  print "color is red or green or blue"
end
```

---

## copyFromTable
Copies the table designated by the parameter of data type table
into the array designated by <array>. Remarks
If the array has a fixed size, the dimension of the table, or of the range of the table, have to match the size of the array. If you copy the table into a one-dimensional array, the values have to be contained in a row of the table.

Syntax

```
<array>.copyFromTable([SourceRange:listrange,] SourceTable:table)
```

Parameters

The parameter SourceTable of data type table designates the table from which
you would like to copy the data.

The optional parameter SourceRange of data type listrange designates the range
which you want to copy from the table.

Example

```
targetArray.copyFromTable(MyDataTable)
```

---

## copyFromTableColumn
Copies the contents of the column of the table into the one-dimensional array designated by <array>. 

Syntax

```
<array>.copyFromTableColumn(SourceTable:table, Column:integer)
```

Parameters

The parameter SourceTable of data type table designates the table from which
you would like to copy data.

The parameter Column of data type integer designates the column whose data you
want to copy.

Example

```
var array: string[]
array.copyFromTableColumn(DataTable, 3)
```

---

## copyToTable
Copies the array designated by <array> into a
table.

Syntax

```
<array>.copyToTable(TargetTable:table[, Column:integer, Row:integer])
```

Parameters

The parameter TargetTable of data type table designates the target table.

The optional parameter Column of data type integer designates the column of the
table.

The optional parameter Row of data type integer designates the row of the
table.

Example

```
arrayVar.copyToTable(MyDataTable,2,9)
```

See also

Write the Contents List into a Table for Further Processing

---

## copyToTableColumn - array
Copies the contents of the one-dimensional array designated by
<array> to the specified column of a table. 

Syntax

```
<array>.copyToTableColumn(TargetTable:table, Column:integer)
```

Parameters

The parameter TargetTable of data type table designates the table to which you
would like to copy data.

The parameter Column of data type integer designates the column into which you
would like to paste data.

Example

```
var array: string[2] := ["hello", "world"]
array.copyToTableColumn(DataTable, 3)
```

---

## delete - array
Deletes the contents of the array designated by
<array>.

Syntax

```
<array>.delete([Index:integer])
```

Parameter

The optional parameter Index of data type integer deletes the item located at
this index position. The size of the array is smaller by 1 after this.

Example

```
a := [current,pi,e]
a.delete(2)
print a.dim
```

---

## deleteValue
Deletes the first occurrence of specified value from the one-dimensional array designated by <array>.

Syntax

```
<array>.deleteValue(Value:any) → boolean
```

Parameter

The parameter Value of data type any designates the value that is going to be
deleted. 

Return Value

The return value has the data type boolean. 
The return value is true if the value is part of the array.
The return value is false if the value is not part of the array.

Example

```
a: string[] := ["Alice", "Bob", "Charlie"]
a.deleteValue("Bob")
print a 
// prints ["Alice", "Charlie"]
```

---

## Dim - array
Returns the dimension of the one-dimensional array designated by
<array>.

Syntax

`<array>.Dim`

Return Value

The return value has the data type integer.

Example

```
var a:real[3]
print a.Dim // prints 3
```

---

## Empty - array
Returns if the array designated by <array> is empty (true) or if it contains items
(false). Remarks
The read-only attribute Empty only applies to one-dimensional arrays.

Syntax

```
<array>.Empty → boolean
```

Return Value

The return value has the data type boolean.

Example

```
var a : integer[]
if a.empty
a.append(42)
end
if not a.empty
print a[1]
end
```

---

## find - array
Searches for a value in the one-dimensional array designated by
<array>.

Syntax

```
<array>.find(Value:any[, StartIndex:integer])
```

Parameters

The parameter Value of data type any designates the value that you want to
find.

The optional parameter StartIndex of data type integer sets the start index, i.e., the position, from which on Plant Simulation starts a search toward the end of the array. 

Return Value

The return value is the position of the item which was found.
Is 0 if the value is not contained in the array.

Example

```
var a:real[5] := [1.1, 2.2, 3.3, 4.4, 5.5]
print a.find(3.3)     // prints 3
print a.find(3.3, 4)  // prints 0, that is, not found
```

---

## getValueOfType
Reads a byte sequence from the array of data type integer designated by <array> and converts it to a value and returns it. Remarks

The method getValueOfType is useful if you want to receive
binary data with the object Socket.

Syntax

```
<array>.getValueOfType(Index:integer, Type:string) -> any
```

Parameters

The parameter Index of data type integer designates the value that you want to
append. 
The parameter Index sets at which position in the array the byte sequence
starts. The length of the byte sequence depends on the value of the parameter Type. Allowed
values for Type are:
"int8", "int16", "int32", "int64", "uint8", "uint16", "uint32", "uint64", "real32", "real64",
"bool",
"Int8", "Int16", "Int32", "Int64", "Uint8", "Uint16", "Uint32", "Uint64", "Real32", "Real64", and
"Bool".

The parameter Type of data type string designates the data type of the value
that you want to append. 
The number in the Type designates the number of bits, where 8 bits result in 1 byte.
"int16" for example reads 2 bytes from the array and creates an integer value
between -32768 and 32767. 
The byte order of the byte sequence is determined by the first letter of the parameter
Type. 

If Type starts with a lower case letter, the byte sequence is interpreted in
little-endian format.

If Type starts with an upper case letter, the byte sequence is interpreted in big-endian
format.

Return Value

The return value has the data type any.

Example

```
var a : integer[]
a.appendValueOfType(123456, "int32")  // append 4 bytes
a.appendValueOfType(-3000, "int16")   // append 2 bytes

var x := a.getValueOfType(1, "int32") // read 4 bytes
var y := a.getValueOfType(5, "int16") // read 2 bytes
```

See also

appendValueOfType [SimTalk]
Socket

---

## insert - array
Inserts a value into the one-dimensional array designated by
<array> which does not have a fixed size.

Syntax

```
<array>.insert(Index:integer, Value:any)
```

Parameters

The parameter Index of data type integer designates the index position at which
Plant Simulation inserts the value.

The parameter Value of data type any designates the value which you want to
insert.

Example

```
var a: real[] := [1.1, 2.2, 3.3, 4.4, 5.5]
a.insert(3,-11)
print a // returns [1.1, 2.2, -11, 3.3, 4.4, 5.5]
```

---

## join
Converts the elements within the array designated by
<array> into a string and unites all elements to a single string. Within the resulting string
the elements are separated by the separator string.

Syntax

```
<array>.join(separator:string) → string
```

Parameter

The parameter separator of data type string sets the separator string. The
separator string can contain any character.

Return Value

The return value has the data type string.

Example

```
var a:integer[]

a.append(1)
a.append(2)
a.append(3)

print a.join(" * ") // 1 * 2 * 3
```

See also

append [SimTalk] - array

---

## Magnitude
    Returns the magnitude/the length of the designated vector of the numerical one-dimensional array designated by <array>. 
        
        Syntax
            
```
<array>.Magnitude → real
```

        
        Return Value
            
            The return value has the data type real.
        
        Example
            
```
var direction: real[3] := [2.0, 3.5, 2.8]
print direction.Magnitude
```

---

## max - array
Returns the greatest value contained in the array
designated by <array>. If the array is empty, the method returns 0 for
an array of numbers and an empty string "" for an array of strings.
Remarks

The method max only applies to one-dimensional arrays with a numerical data type or with the data type string.

Syntax

`<array>.max`

Return Value

If the method is called with two values having the same physical unit, the
returned value also has this unit. Compare these examples:
```
max(time, time)        -> time
max(length, length)    -> length
max(length, speed)     -> real
max(length, real)      -> real
max(integer, integer)  -> integer
max(integer, real)     -> integer
max(real, integer)     -> integer
max(integer, weight)   -> real
`Example`
var a:real[5] := [1.1, 2.2, 3.3, 4.4, 5.5]
print a.max // prints 5.5
```

```
var arrPartPos: length[]
arrPartPos := [6300mm, 5600mm]
var maxPartPos: length := arrPartPos.max
print arrPartPos.max
```

See also

min [SimTalk] - array

---

## min - array
Returns the smallest value contained in the array
designated by <array>. If the array is empty, the method returns 0 for an array
of numbers and an empty string "" for an array of strings.Remarks
The method min only applies to one-dimensional arrays with a numerical data type or with the data type string.

Syntax

`<array>.min`

Return Value

If the method is called with two values having the same physical unit, the
returned value also has this unit. Compare these examples:
```
min(time, time)        -> time
min(length, length)    -> length
min(length, speed)     -> real
min(length, real)      -> real
min(integer, integer)  -> integer
min(integer, real)     -> integer
min(real, integer)     -> integer
min(integer, weight)   -> real
`Example`
var a:real[5] := [1.1, 2.2, 3.3, 4.4, 5.5]
print a.min // prints 1.1
```

```
var arrPartPos:length[]
arrPartPos := [6300mm, 5600mm]
print arrPartPos.min
```

See also

max [SimTalk] - array

---

## normalize
Normalizes the array designated by <array>
of a numerical data type.Remarks
The method normalize only applies to numerical one-dimensional arrays.A normalized vector retains its direction, its length (its Magnitude)
becomes 1 though. The resulting vector is often called unit vector. A vector is normalized by
dividing it by its own length.

Syntax

```
<array>.normalize → real
```

Return Value

The return value has the data type real. 
The return value is the magnitude of the designated old vector.

Example

```
var v:real[3]
v := [2,3,4]
print v.normalize
print v 
// prints 5.3851648071345
[0.371390676354104, 0.557086014531156, 0.742781352708207]
```

See also

Magnitude [SimTalk]

---

## pop - array
Removes the last element from the array designated by
<array> and returns this value.

Syntax

```
<array>.pop → any
```

Return Value

The return value has the data type any.

Example

```
var a:integer[]

a.append(1)
a.append(2)
a.append(3)

print a.pop // 3
```

---

## sort - array
Sorts the array designated by <array>. Remarks
When sorting a two-dimensional array, Plant Simulation sorts the rows according to the first column.Note 
Sorting is case-sensitive.

Syntax

```
<array>.sort(Descending:boolean:=false)
```

Parameter

The optional parameter Descending of data type boolean sets how the array is
going to be sorted:

Specify 
`true`
 to sort the array in descending order.

Specify 
`false`
 or do not specify the parameter to sort the array in
ascending order.
Default Value of the Parameter
The default value is false.

Examples

```
var a:integer[] := [4, 2, 1, 3]
a.sort(false) // ascending
print a       // returns [1, 2, 3, 4]
```

```
var a:integer[] := [4, 2, 1, 3]
a.sort(true) // descending
print a      // returns [4, 3, 2, 1]
```

---

## sum - array
Returns the sum of all values contained in the array designated
by <array>. Remarks
The method sum only applies to one-dimensional arrays.

Syntax

`<array>.sum`

Example

```
var a:real[5] := [1.1, 2.2, 3.3, 4.4, 5.5]
print a.sum // returns 16.5
```

---

## X - array
Returns the element of the array designated by <array> with
the index 1.Remarks
The attribute X applies to one-dimensional arrays, which are of data type integer, real, or length, and have a fixed dimension of three elements. The attribute X points to the element of the array with the index 1.The attribute X applies to one-dimensional arrays, which are of data type integer, real, or length, and have a fixed dimension of two elements. 

Syntax

```
<array>.X -> integer
```

Return Value

The return value has the data type integer.

Example

```
var c: real[3] := Station.Coordinate3D
print c.X  // prints c[1]
c.X := 42  // c[1] := 42
```

See also

Y [SimTalk] - array
Z [SimTalk] - array

---

## xDim - array
Returns the x-dimension of the two-dimensional array designated
by <array>.

Syntax

```
<array>.xDim -> integer
```

Return Value

The return value has the data type integer.

Example

```
var matrix:real[2,3]
print matrix.xDim // prints 2
```

---

## Y - array
Returns the element of the array designated by <array> with
the index 2.Remarks
The attribute Y applies to one-dimensional arrays, which are of data type integer, real, or length, and have a fixed dimension of three elements. The attribute Y points to the element of the array with the index 2.The attribute Y applies to one-dimensional arrays, which are of data type integer, real, or length, and have a fixed dimension of two elements. 

Syntax

```
<array>.Y -> integer
```

Return Value

The return value has the data type integer.

Example

```
var c: real[3] := Station.Coordinate3D
print c.Y  // prints c[2]
c.Y := 42  // c[2] := 42
```

See also

X [SimTalk] - array
Z [SimTalk] - array

---

## yDim - array
Returns the y-dimension of a two-dimensional array designated by
<array>.
Remarks

The method yDim returns 0 for a one-dimensional
array. This way you can find out if a local variable of data type any
contains a one-dimensional array or a two-dimensional
array and if it was assigned to this station, not if it actually was there yet.

Syntax

```
<array>.yDim -> integer
```

Return Value

The return value has the data type integer.

Example

```
var matrix:real[2, 3]
print matrix.yDim // prints 3
```

---

## Z - array
Returns the element of the array designated by <array> with
the index 3.Remarks
The attribute Z applies to one-dimensional arrays, which are of data type integer, real, or length and have a fixed dimension of three elements. 

Syntax

```
<array>.Z -> integer
```

Return Value

The return value has the data type integer.

Example

```
var c: real[3] := Station.Coordinate3D
print c.Z  // prints c[3]
c.Z := 42  // c[3] := 42
```

See also

X [SimTalk] - array
Y [SimTalk] - array
