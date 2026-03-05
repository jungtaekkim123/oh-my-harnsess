> **Read this when:** Primitive/scalar types: boolean, integer, real, string, date, time, acceleration, length, speed, weight, money  
> **Skip this when:** Array methods (see 08), JSON (see 09), or collections like List/Queue/Stack/Table (see 10)


## Contents

- [Data Types](#data-types)
  - [Acceleration](#acceleration)
  - [Any](#any)
  - [Boolean](#boolean)
  - [Date](#date)
  - [DateTime](#datetime)
  - [Integer](#integer)
  - [Length](#length)
  - [Method](#method)
  - [Object](#object)
  - [Real](#real)
  - [Speed](#speed)
  - [String](#string)
  - [Time](#time)
  - [Weight](#weight)
  - [Converting Data Types](#converting-data-types)

## Data Types

### Data Types

Plant Simulation only supports the data type money for global variables, user-defined attributes, and for lists and tables. 
Money is not a SimTalk data
type. For local variables use the data type real instead. 
RandTime [SimTalk]

The global Variable and the user-defined attributes provide the data type randtime. You can use it to generate random numbers of data type time using a random number stream of its own. 
Let's say you want to make the random numbers for the setup time independent of the random numbers for the processing time. To achieve this, create a user-defined
attribute of data type randtime, and set the distribution type of the
Set-up time to Formula, and type
`self.<UserDefinedAttribute>.rollDice`
into the edit box.
RandTime is not a SimTalk
data type. When getting a randtime value, Plant
Simulation returns a time value.
Path [signature]

The window Show Attributes and Methods shows the signature path for some objects in the column Signature. 
Path is not a data type that you can assign. If a
built-in attribute is listed with the data type path, you can assign a
value of data type object or string to it. 

See also

Data Types in Local Variables
Keywords

---

### Acceleration
   A local variable of data type acceleration has a maximum range of values between -8.9*10307 ≤ acceleration ≤ 8.9*10
      307, which is displayed like this -8.9e307 ≤ real ≤ 8.9e307.Remarks
         The data type acceleration applies to the objects Conveyor and Transporter. When assigning it to a variable or an attribute, Plant
               Simulation interprets the value as meters per second squared (m/s2). When outputting it, Plant Simulation converts the value to the unit you selected under File > Model Settings/Preferences > Units >
   Acceleration.Note 
In SimTalk 2.0 you can specify the speed units 
`mps`
, 
`fps`
, 
`kmh`
, and 
`mph`
. 
Type in the unit directly after the values, without a separating blank space, for example 
`10mps2`
 or 
`10.2mps2`
. 
Hold down AltGr and press the key with the number 2 to enter the square sign. If your keyboard does not have the Alt Gr key, hold down Ctrl-right+Alt-right instead.

      Example
         
```
var a : acceleration := 10mps²  // 10 meters per second squared 
var b : acceleration := 2.5fps² // 2.5 feet per second squared
```

         The data types time, length, weight, speed, and
               acceleration are not compatible! You can, for example, only assign a value
            of data type length, real or integer to a variable of data
            type length.
      
      See also
         
         isAcceleration [SimTalk]

---

### Any
A local variable of data type any can
take any value. Remarks
The data type of the variable assumes the data type of the first assigned value. If you then assign a value that is incompatible with this data type, Plant Simulation shows an error.To reset the assumed data type, use the forget [SimTalk] statement.
Return Value

The return value has the data type boolean.
Query the data type of a variable of data type any with
the following functions. The function expects a parameter whose data type Plant
Simulation compares.
| getSimTalkTypename [SimTalk] | isLength [SimTalk] | typeStatisticsCumulated [SimTalk] || isAcceleration [SimTalk] | isList [SimTalk] | isString [SimTalk] || isBoolean [SimTalk] | isListRange [SimTalk] | isTable [SimTalk] || isDate [SimTalk] | isObject [SimTalk] | isTime [SimTalk] || isDatetime [SimTalk] | isQueue [SimTalk] | isWeight [SimTalk] || isInteger [SimTalk] | isReal [SimTalk] |  || isJson [SimTalk] | isSpeed [SimTalk] |  |

Examples

```
a := 3.14   -- data type real is assumed
forget a    -- now we can assign a new data type
a := "Test" -- data type string is assumed
```

```
param arg: any // declaring the method named myPrint
if isLength(arg) 
   print "length = ", arg 
end
    
// calling the method myPrint 
myPrint(1)
myPrint("any text")
myPrint(MyConveyor.length)
```

```
var a : any
a := MyConveyor.acceleration
print a," ",getUnit(a)
print isAcceleration(a)
```

Note 
The following applies to isObject, isTable, and isList: The value VOID
does not have a data type as local variables of data types object, table, and
list can all take the value void. For this reason a local variable of data type
any does not take a data type when you assign void to it. If the function isObject
is called with such a variable, the function returns the result false.

Example

```
var a: any := void
print isObject(a)   // prints false
print a = void      // prints true

var b : any := 123
print b = void      // prints false
```

You can also use the function getSimTalkTypename to get
the data type of a variable of data type any. 

Return Value

The return value has the data type string.

Example

```
param a : any
switch getSimTalkTypename(a)
case "integer" 
   print "integer argument"
case "string" 
   print "string argument"
end
```

See also

Query the Data Type of a Variable of Data Type Any

---

### Boolean
        A local variable of data type boolean can be 
`true`
 or 
`false`
.
        See also
            
            Boolean [SimTalk] - value
            isBoolean [SimTalk]

---

### Date
    A local variable of data type date
        designates a date between 01.01.1900 and 31.12.9999. Remarks
            
            When assigning a value to a variable or an attribute of the data type
                    time, you have to convert the date with the function
                    str_to_date.
            Before you assign a value to the local variable, it has an initial value. It is 0 for all numerical data types, false for the data type boolean, an empty string (
`""`
) for the
                data type string, and void for the data types object and list or table. 
            The initial value for the data types date and DateTime depends on the Plant Simulation
                version in which you initially created your simulation model. For models, which you
                created in Plant Simulation 14.0 or higher, the start value
                is 01.01.1900.
        
        See also
            
            isDate [SimTalk]

---

### DateTime
    A local variable of data type dateTime designates a date and a time between 01.01.1900 00:00:00 and 31.12.9999
        23:59:59. Remarks
            
            When assigning a value to a variable or an attribute, you have to
                convert the date with the function str_to_dateTime. 
            Before you assign a value to the local variable, it has an initial value. It is 0 for all numerical data types, false for the data type boolean, an empty string (
`""`
) for the
                data type string, and void for the data types object and list or table. 
            The initial value for the data types Date and dateTime depends on the Plant Simulation version
                in which you initially created your simulation model. For models, which you created
                in Plant Simulation 14.0 or higher, the start value is
                01.01.1900.
        
        See also
            
            isDatetime [SimTalk]

---

### Integer
    A local variable of data type integer
        can only contain integer numbers. Remarks
            
            The range of values is between -9.223.372.036.854.775.808 ≤ integer ≤
                9.223.372.036.854.775.807. Plant Simulation does not check
                for values outside of this range. 
        
        See also
            
            Integer [SimTalk] - value
            isInteger [SimTalk]

---

### Length
   A local variable of data type length
      has a maximum range of values between -8.9*10307 ≤ length ≤
         8.9*10307, which is displayed like this -8.9e307 ≤ real ≤
      8.9e307.
      Remarks
         
         When assigning it to a variable or an attribute, Plant
               Simulation interprets the value as meters (m). 
         When outputting the value to the Debugger or
            the Console, Plant Simulation converts
            the value to the unit you selected under File > Model
               Settings/Preferences > Units > Length.
         Note 
            In SimTalk 2.0 you can specify the length
               units 
`m`
, 
`mm`
,
                  
`km`
, 
`cm`
, 
`yd`
, 
`ft`
, and 
`in`
.
            Type in the unit directly after the values, without a separating
               blank space, for example 
`10m`
 or 
`10.2yd`
. 
            You can type in the unit for floating point
                  values and for integer values.
         
         The data types time, length, weight, speed and acceleration are not compatible! You can, for example, only
            assign a value of data type length, real or integer to a variable of data type length.
      
      Example
         
```
var len := 1.0ft
var s : speed := 10.5m / 1:30
var x : length := 3m
```

      
      See also
         
         isLength [SimTalk]

---

### Method
A local variable of data type method is a
user-defined attribute of data type method, also
called an attribute method in most cases. Remarks

This user-defined attribute is a part of the object, i.e.,
it moves with the object, when you insert it into another Frame or model or
when you move it. Compare the topics Entrance
control and self for details about
using it. 
The object Method and user-defined attributes of data type method have their
own random number stream which you can assign with the attribute RandomSeed. 
As you are used to from the material flow objects, Plant
Simulation automatically assigns the random number stream when you insert an object, so that
each object has its own random number stream.
Method execution for user-defined attributes of data
type method, which are deleted while they are being executed, is terminated
immediately, it will not be continued. Compare the following examples: 

Suppose that a MU has a user-defined
attribute of data type method which was suspended via a waituntil-instruction. Then, the MU is deleted
in the Drain, which naturally also deletes its user-defined attributes. Thereupon the Method is deleted from the
list of suspended methods and method execution is terminated, i.e., the instructions after the
waituntil-instruction will not be executed.
If the attribute method was called from another Method, execution of this Method will be continued. 
If the attribute method had a return value, the value,
which the implicitly existing local variable result had at this point in
time, will be returned to the calling Method.

Suppose that a MU has a user-defined
attribute of data type method which is called by the entrance control of a Station. The attribute method in turn calls a Method that is
inserted in the Frame. This Method deletes the MU with the statement Station.Cont.delete. 
The execution of the attribute method and of the Method called by it are terminated immediately. The return value of the attribute method (or VOID if no return value was declared) will be returned to
the entrance control whose execution will be continued.

User-defined attributes of data type method and objects of type Method behave the same when you extend the
path. For the instruction 
```
Station.MyMethAttr.executeIn(60)
```

Plant Simulation calls the user-defined attribute
named MyMethAttr and not the method executeIn(60). 
If you want to prevent the user-defined attribute from
being executed, you have to use the reference
operator &, 
```
Station.&MyMethAttr.executeIn(60)
```
 for
our example above.

See also

RandomSeed [SimTalk] - Method
User-defined Attributes [general description]

---

### Object
A local variable of data type object
points to an object in your simulation model or is void. Remarks

You can save any graphically represented
object with the data type object. This variable can be a local variable, a
formal parameter, a global variable and values in tables.
You can assign both objects and strings to the variables
of data type object mentioned above. 
If you assign an object, Plant Simulation creates an
Object Reference, regardless if you specify
the object with a relative or an absolute path.
Specify the object with a relative path to immediately resolve the relative path
within the context of the current Method and create an object reference to
the computed object.
Let’s suppose that the method .Models.Model.Method
contains the following method call: 
```
SubFrame.methodU(Station)
```

Plant Simulation resolves the relative path Station to an object reference to .Models.Model.Station and passes this object reference to the method within the SubFrame. If the path cannot be resolved to an object, Plant Simulation opens the Debugger.
If a string is passed to a variable, the string is assigned as a path to the variable. Regardless if this path is
relative or absolute, Plant Simulation does not resolve it at this point in
time. Instead, the path is resolved each and every time when the variable is read.
Let’s suppose that the method .Models.Model.Method
contains the following method call: 
```
SubFrame.methodU("Station")
```

Plant Simulation passes the relative path Station to the method within the SubFrame. At this
point in time such an object neither has to exist within the context of the calling method, nor
within the context of the called method as the path is not resolved yet. 
Let’s suppose that we inserted an object of type Station
into the SubFrame and that this object has the name Station1. 
Let’s also suppose that the source code of methodU in
the SubFrame looks like this:
```
param o: object
Station1.Name := "Station"
o.name := "Station1"
o.name := "Test"  // ERROR!
`Each time the local variable named`
o
```
 is accessed, the relative path will be resolved, in fact it will be
resolved within the context of this method, meaning that path resolution starts in the SubFrame. This way it points to .Models.Model.SubFrame.Station, which now exists. This Station is
then renamed to Station1 so that the path Station
cannot be resolved in the next line of code and Plant Simulation thus opens
the Debugger.
You can assign values of data type object to variables
of data type string or to attributes of data type string. If the value contains an object reference, the
absolute path will be assigned with a leading asterisk (*).
If the value contains a relative or an absolute path, this path is assigned.
```
var o1: object := "Station"
var o2: object := ".Models.Model.Station"
var o3: object := .Models.Model.Station
var s1: string := o1  -- "Station"
var s2: string := o2  -- ".Models.Model.Station"
var s3: string := o3  -- "*.Models.Model.Station"
```

See also

isObject [SimTalk]
The Absolute Path
The Relative Path
Object Reference

---

### Real
A local variable of data type real
contains floating point numbers. The value range is between -1.7976931348623158e+308 and
1.7976931348623158e+308.
Remarks

Real numbers have a precision of 16 places (meaning digits, i.e., digits before
and after the decimal point). When displaying the numbers, the computer rounds to 15 places.
As floating point numbers can only save a fixed number of places, rounding errors
can, in principle, always occur when computing with floating point numbers. For this reason you
should, as a rule, not use the equal operator 
`=`
 when comparing
floating point numbers as it checks for exact equivalence. Use the about-equal-operator 
`~=`
 instead.
You can also type in floating point numbers with mantissa and exponent in this
notation: 
`1.0e-3`
 this corresponds to 
`0.001`
.
Internally Plant Simulation always saves the numbers
with mantissa and exponent. The accuracy of the mantissa is limited to 16 decimal digits. This is
determined by the representation of floating point numbers in the CPU, which is defined by the IEEE
Standard for Floating-Point Arithmetic (IEEE 754).
The CPU can only process binary data, i.e., zeros and ones. For this reason
floating point numbers are represented according to the IEEE-754 standard in the binary numeral
system. Consequently, the mantissa actually does not contain 16 decimal digits but 53 binary
numbers. Many numbers, which can be represented within the decimal system with a finite number of
digits, cannot be represented with a finite number of digits in the binary numeral system. 

Examples

The decimal number 1.125 can be represented precise as 1 + 0/2 +
0/4 + 1/8. This corresponds to the binary number 1.001.

The decimal number 1.1 cannot be represented precise with a finite number
of places. Within the binary numeral system this would be 1 + 0/2 + 0/4 + 0/8 + 1/16 + 1/32
+ 0/64 + 0/128 + 1/256 + 1/512 + 0/1024 + 0/2048 + 1/4096 + 1/8192 + …
This corresponds to the binary number 1.0001100110011…

If you type a number with decimal point and digits after the decimal point into
the Method Editor, the computer converts this number to a floating point
number according to the IEEE-754 standard when interpreting the source code so that the CPU can
process it. The number is thus converted into a binary number with a fixed number of places. If
binary places are cut off during this process, this number minimally differs from the decimal number
that you specified.
You can view this effect when you run the following SimTalk instruction:

```
var x: real := 1.1 - 1
```

You can then see in the Method-Debugger that x has the value
0.1000000000000001.

See also

isReal [SimTalk]
Real [SimTalk] - value

---

### Speed
A local variable of data type speed has a
maximum range of values between -8.9*10307 ≤ speed ≤ 8.9*10307 which is
displayed like this -8.9e307 ≤ real ≤ 8.9e307. Remarks

When assigning it to a variable or an attribute, Plant
Simulation interprets the value as meters per second (m/s). When outputting it, Plant Simulation converts the value to the unit you selected under File > Model Settings/Preferences > Units > Speed.
Note 
In SimTalk 2.0 you can specify the speed units 
`mps`
, 
`fps`
, 
`kmh`
, and 
`mph`
. 
Type in the unit directly after the number, without a separating blank space, for
example 
`100kmh`
 or 
`100.5kmh`
.
```
var len := 1.0ft
var s : speed := 10.5m / 1:30
var x : length := 3m
```

Note 
In SimTalk 2.0 you can type in the unit 
`s`
 for seconds. Type in the unit

`s`
 directly after the number, without a separating blank space.
Specifying the unit sometimes is necessary to make sure that the computed expression has the correct
data type.
```
var x : length := 10m
var s : speed := x / 2s   // Beware: x/2 would have the wrong unit, m instead of m/s
```

The data types time, length,
weight, speed and acceleration are not compatible! You can, for example, only assign a value of data type length, real, or integer to a
variable of data type length.

See also

isSpeed [SimTalk]

---

### String
        A local variable of data type string can consist of any number of characters, meaning upper or lower
                case letters, numbers, special characters, etc. enclosed in quotation marks 
`""`
.Remarks
                        
            Plant Simulation shows a value of data type
                    string in the source code in this color .
            
```
var st: string := "Hello World! Good day to everybody."
```

        
        See also
            
                        Functions for Editing Variables of Data Type String
                        Compare strings with relational operators
                        Colors for Syntax Highlighting
            isString [SimTalk]
            String [SimTalk] - value

---

### Time
    A local variable of data type time
        has a maximum range of values between -8.9*10307 ≤ time ≤
            8.9*10307 which is displayed like this -8.9e307 ≤ real ≤
        8.9e307. Remarks
            
            When assigning it to a variable or an attribute, the value is always
                interpreted in seconds (sec). Plant Simulation converts the
                output to a compound format with hours (hh) minutes (mm) and seconds (ss.ss)
                separated by colons: hh:mm:ss.ss
            The data types time, length, weight, speed,
                and acceleration are not compatible! You can, for example,
                only assign a value of data type length, real, or integer to a variable of
                data type length.
        
        See also
            
            isTime [SimTalk]

---

### Weight
   A local variable of data type weight
      has a maximum range of values between -8.9*10307 ≤ weight ≤
         8.9*10307 which is displayed like this -8.9e307 ≤ real ≤ 8.9e307. Remarks
         
         When assigning it to a variable or an attribute, Plant
               Simulation interprets the value as kilograms (kg). When outputting it, Plant Simulation converts the value to the unit you selected
            under File > Model Settings/Preferences > Units >
               Mass.
         The data types time, length, weight, speed, and
               acceleration are not compatible! You can, for example, only
            assign a value of data type length, real, or integer to a variable of data type length.
      
      See also
         
         isWeight [SimTalk]

---

### Converting Data Types

Plant Simulation automatically converts numeric values. You have to explicitly start all other type conversions. 
Plant Simulation automatically converts the data type integer to real and vice versa. When you assign a real value to an integer variable, the digits after the decimal point will be lost. When parameters are passed, Plant Simulation automatically converts the data type real to integer and vice versa. The same is true for the data types dateTime and date. Here, Plant Simulation deletes the time part. 
During calculations Plant Simulation treats the units of the physical data types length, weight, speed, acceleration and time as real numbers. If a calculation results in another physical data type, Plant Simulation assigns the result the corresponding data type. The quotient of length and time is assigned the data type speed. If the result cannot be assigned a physical data type, Plant Simulation uses real instead.
You can only assign a value with the correct unit or a value without a unit (real or integer) to a local variable of physical data types (length, weight, speed, acceleration, time). In all other cases the assignment throws an error to point out a potential problem.
Manually Converting Data Types

The remaining data types you have to convert explicitly by calling the conversion function listed below:
| Conversion method | Data type of the return value || bool_to_num [SimTalk](boolean) | real [SimTalk] || num_to_bool [SimTalk](integer) | boolean [SimTalk] || str_to_bool [SimTalk](string) | boolean [SimTalk] || str_to_date [SimTalk](string) | time [SimTalk] || str_to_dateTime [SimTalk](string) | dateTime [SimTalk] || str_to_length [SimTalk](string) | length [SimTalk] || str_to_num [SimTalk](string) | real [SimTalk] || str_to_obj [SimTalk](string) | object [SimTalk] || str_to_speed [SimTalk](string) | speed [SimTalk] || str_to_time [SimTalk](string) | time [SimTalk] || str_to_weight [SimTalk](string) | weight [SimTalk] || to_str [SimTalk](any, … ) | string [SimTalk] |
