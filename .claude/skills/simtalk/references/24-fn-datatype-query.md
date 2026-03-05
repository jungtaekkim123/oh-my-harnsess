> **Read this when:** Type introspection: type checking functions, `is_*` predicates, querying data types at runtime  
> **Skip this when:** Type conversion (see 26) or primitive type details (see 07)


## Contents

- [Query the Data Type of a Variable of Data Type any](#query-the-data-type-of-a-variable-of-data-type-any)
  - [Query the Data Type of a Variable of Data Type Any](#query-the-data-type-of-a-variable-of-data-type-any)
  - [getSimTalkTypename](#getsimtalktypename)
  - [isAcceleration](#isacceleration)
  - [isArray](#isarray)
  - [isBoolean](#isboolean)
  - [isDate](#isdate)
  - [isDatetime](#isdatetime)
  - [isInteger](#isinteger)
  - [isJson](#isjson)
  - [isLength](#islength)
  - [isList](#islist)
  - [isListRange](#islistrange)
  - [isObject](#isobject)
  - [isQueue](#isqueue)
  - [isReal](#isreal)
  - [isSpeed](#isspeed)
  - [isStack](#isstack)
  - [isString](#isstring)
  - [isTable](#istable)
  - [isTime](#istime)
  - [isWeight](#isweight)

## Query the Data Type of a Variable of Data Type any

### Query the Data Type of a Variable of Data Type Any
                contents to the left for querying the data type of a variable of data type
                    Any. 
            The function expects a parameter whose data type Plant Simulation compares. 
        See also
            
            Any [SimTalk]
        
        Return Value
            
            The return value has the data type boolean.

---

### getSimTalkTypename
   Returns the name of the data type of an arbitrary value. 
      
      Syntax
         
```
getSimTalkTypename(Value:any) → string
```

      
      Return Value
         
         The return value for the data types table/stack/queue returns these
            strings:
         | Data Type [SimTalk] | Return Value [SimTalk] || table [SimTalk] | table [SimTalk] || stack [SimTalk] | stack [SimTalk] || queue [SimTalk] | queue [SimTalk] |
         For local variables of data type any, which were assigned a special object, for
            example a sensor, getSimTalkTypename returns sensor,
               lane,, storage place, 3D
               object, or 3D animation depending on the type of
            the special object. 
         If the passed value has an  data type Array, getSimTalkTypename returns an array.
      
      Examples
         
```
print getSimTalkTypename(Conveyor.sensorID(1))  // sensor
print getSimTalkTypename(Conveyor._3D)          // 3D object
print getSimTalkTypename(TwoLaneTrack.A)        // lane
print getSimTalkTypename(Store[1,1])            // storage place
```

```
// compute the character count
param value: any -> integer

switch getSimTalkTypename(value)
case "integer"
   if value > 0
      return log10(value) + 1
   elseif value < 0
      return log10(-value) + 2
   else
      return 1;
   end
case "string"
   return strlen(value)
case "object"
   return strlen(obj_to_str(value))
case "boolean"
   return when value then /*true*/4 else /*false*/5
else
   return -1  // error
end
```

      
      See also
         
         Any [SimTalk]
         Array [SimTalk]

---

### isAcceleration
   Returns if the designated argument is of data type Acceleration or not.
      
      Syntax
         
```
isAcceleration(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isAcceleration(arg)
   print "acceleration = , arg
end 
```

      
      See also
         
         Any [SimTalk]
         Acceleration [SimTalk]

---

### isArray
Returns if the designated argument has an Array data type or
not

Syntax

```
isArray(Argument:Value) → boolean
```

Parameter

The parameter Argument of data type any designates the argument to be
checked.

Return Value

The return value has the data type boolean.

Example

```
var a:any[] := [[1,2,3], 42]
print "a = ", a
print "a[1] = ", a[1]
print "a[2] = ", a[2]

print isArray(a)    // true
print isArray(a[1]) // true
print isArray(a[2]) // false
```

See also

Array [SimTalk]

---

### isBoolean
   Returns if the designated argument is of data type Boolean or
      not.
      
      Syntax
         
```
isBoolean(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isBoolean(arg) 
   print "Boolean = ", arg
end
```

      
      See also
         
         Any [SimTalk]
         Boolean [SimTalk]

---

### isDate
   Returns if the designated argument is of data type Date or
      not.
      
      Syntax
         
```
isDate(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isDate(arg) 
   print "Date = ", arg
end 
```

      
      See also
         
         Any [SimTalk]
         Date [SimTalk]

---

### isDatetime
   Returns if the argument designated is of data type DateTime
      or not.
      
      Syntax
         
```
isDatetime(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isDatetime(arg) 
   print "Datetime = ", arg
end 
```

      
      See also
         
         Any [SimTalk]
         DateTime [SimTalk]

---

### isInteger
   Returns if the designated argument is of data type Integer or
      not
      
      Syntax
         
```
isInteger(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isInteger(arg) 
   print "Integer = ", arg
end 
```

      
      See also
         
         Any [SimTalk]
         Integer [SimTalk]

---

### isJson
   Returns if the designated argument is of data type JSON or
      not.
      
      Syntax
         
```
isJson(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isJson(arg) 
   print "json = ", arg
end 
```

      
      See also
         
         Any [SimTalk]
         JSON [SimTalk]

---

### isLength
   Returns if the designated argument is of data type Length or
      not.
      
      Syntax
         
```
isLength(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isLength(arg) 
   print "Length = ", arg
end
```

      
      See also
         
         Any [SimTalk]
         Length [SimTalk]

---

### isList
Returns if the designated argument is of data type List or
not.
Syntax

```
isList(Argument:any) → boolean
```

Parameter

The parameter Argument of data type any designates the argument to be
checked.

Return Value

The return value has the data type boolean.
Note 
The value VOID does not have a data type as local variables of data types object,
table, and list can all take the value void. For this reason a local variable of
data type any does not take a data type when you assign void to it. 

Example

```
var a: any := void
print isObject(a)  // prints false
print a = void     // prints true

var b : any := 123
print b = void     // prints false 
```

See also

Any [SimTalk]
List [SimTalk]

---

### isListRange
   The function isListRange returns if the designated argument
      is a list range (true) or not (false).
      Syntax
         
```
isListRange(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isListRange(arg)           // something like {1,1}..{2,*}
   print "listRange = ", arg  // prints listRange = {1,1}..{2,*}
end 
```

      
      See also
         
         Any [SimTalk]

---

### isObject
Returns if the designated argument is of data type Object or
not.

Syntax

```
isObject(Argument:any) → boolean
```

Parameter

The parameter Argument of data type any designates the argument to be
checked.

Return Value

The return value has the data type boolean.
Note 
For isObject, isTable, and isList this applies: The value VOID does
not have a data type as local variables of data types object, table, and
list can all take the value void. For this reason a local variable of data type
any does not take a data type when you assign void to it. If the function isObject
is called with such a variable, the function returns the result false.

Example

```
var a: any := void
print isObject(a)  // prints false
print a = void     // prints true

var b : any := 123
print b = void     // prints false 
```

See also

Any [SimTalk]
Object [SimTalk]

---

### isQueue
   Returns if the designated argument is of data type Queue or
      not.
      
      Syntax
         
```
isQueue(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isQueue(arg) 
   print "Queue = ", arg
end 
```

      
      See also
         
         Any [SimTalk]
         Queue [SimTalk]

---

### isReal
   Returns if the designated argument is of data type Real or
      not.
      
      Syntax
         
```
isReal(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isReal(arg) 
   print "Real = ", arg
end
```

      
      See also
         
         Any [SimTalk]
         Real [SimTalk]

---

### isSpeed
   Returns if the designated argument is of data type Speed or
      not.
      
      Syntax
         
```
isSpeed(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isSpeed(arg) 
   print "Speed = ", arg
end
```

      
      See also
         
         Any [SimTalk]
         Speed [SimTalk]

---

### isStack
   Returns if the designated argument is of data type Stack or
      not.
      
      Syntax
         
```
isStack(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isStack(arg) 
   print "Stack = ", arg
end
```

      
      See also
         
         Any [SimTalk]
         Stack [SimTalk]

---

### isString
   Returns if the designated argument is of data type String or
      not.
      
      Syntax
         
```
isString(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isString(arg) 
   print "String = ", arg
end
```

      
      See also
         
         Any [SimTalk]
         String [SimTalk]

---

### isTable
   Returns if the designated argument is of data type Table or
      not.
      
      Syntax
         
```
isTable(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be checked.
      
      Return Value
         
         The return value has the data type boolean.
         Note 
            The value VOID does not have a data type as local variables of data types
                  object, table, and list can all take the value void.
               For this reason a local variable of data type any does not take a data type
               when you assign void to it. 
         
      
      Example
         
```
param arg: any
if isTable(arg) 
   print "Table = ", arg
end
```

      
      See also
         
         Any [SimTalk]
         Table [SimTalk]

---

### isTime
   Returns if the designated argument is of data type Time or
      not.
      
      Syntax
         
```
isTime(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isTime(arg) 
   print "Time = ", arg
end
```

      
      See also
         
         Any [SimTalk]
         Time [SimTalk]

---

### isWeight
   Returns if the designated argument is of data type Weight or
      not.
      
      Syntax
         
```
isWeight(Argument:any) → boolean
```

      
      Parameter
         
         The parameter Argument of data type any designates the argument to be
            checked.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
param arg: any
if isWeight(arg) 
   print "Weight = ", arg
end
```

      
      See also
         
         Any [SimTalk]
         Weight [SimTalk]

---
