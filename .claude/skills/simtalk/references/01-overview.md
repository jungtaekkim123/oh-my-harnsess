> **Read this when:** First contact with SimTalk, 'what is SimTalk', quick syntax overview, basic value types  
> **Skip this when:** You already know SimTalk basics and need specific function signatures or advanced features

## SimTalk Reference

### SimTalk Reference
integrated in Plant Simulation. It enables you to implement custom behavior
and logic in your simulation model which is not covered by the built-in functionality of the
simulation objects. SimTalk contains an Interpreter,
which directly executes the instructions you wrote in objects of type Method
, when Plant Simulation
runs the simulation.SimTalk is tightly integrated with the simulation objects. With SimTalk you can access all attributes, read-only attributes, and methods of the built-in objects.You can also create your own reusable objects with behavior for your specific needs and implemented in SimTalk. Together with the integrated Method Debugger
  SimTalk is an easy-to-use programming environment.Instead of programming code in SimTalk, you can also program code in Python. Note 
Python code is not intended to replace SimTalk code. As SimTalk code also accesses compiled built-in functions, it generally is quite a bit faster in execution than Python code.
As many university graduates are exposed to Python,
writing Python code during their studies, the Python
Module makes programming in Plant Simulation easier. 
In Plant Simulation 12.1 we introduced SimTalk 2.0. We simplified the syntax and added a number of features to make it easier to write your code.The Plant Simulation Help only describes SimTalk 2.0. Click this to show a short comparison of the major differences.SimTalk 1.0 stills works in the current and previous versions of Plant Simulation and you can continue using SimTalk 1.0 in old and new models.The command Find Outdated
Functions on the Debugger ribbon tab finds methods, attributes, read-only
attributes, and functions in the source code of all Methods in your simulation model.The description of SimTalk is divided in:

General SimTalk Access

SimTalk Access in 3D

Note 
SimTalk supports English and German for programming the source code of your methods.
For this reason the German Help shows the English name of the attribute, read-only attribute, and method next to the German name, separated by a forward slash, for example EnergieAktiv [SimTalk] / EnergyActive. This facilitates programming methods if you are working with the German version of Plant Simulation and are creating an English language model that your colleagues in other countries can use as well.

Compare Creating a German Model with English Identifiers.
Also consultWhat's NewIntroducing Plant SimulationUpdate Arbitrary Old ModelsThe Components of the Program Window
The Step-by-Step HelpOutdated SimTalk NamesThe 3D Help
SimTalk Access to 3DThe Quick Reference CardsThe Add-Ins Reference HelpThe Libraries Reference

---



---

## A Quick Tour Through SimTalk 2.0

#### A Quick Tour Through SimTalk 2.0
```
print "Hello, World!"
```
This is a complete source code which you can run. You don’t need to type in semicolons at the end of each statement as is required in C, in C++, or in JavaScript.This tour provides you with enough information to start writing code in SimTalk by showing you how to approach a variety of programming tasks. Do not worry if you don’t understand something. Everything that we are going to introduce in this tour is explained in detail in the rest of the Plant Simulation Help.Below we describe:

Simple Values

Control Flow

Declare Default Arguments

---

#### Simple Values
Use var to create a local
variable:
```
var myVariable := 42
```

A local variable must have the same data type as the value
you want to assign to it.
If the initial value does not provide enough information, or if there is no
initial value, specify the data type by typing it in after the variable, separated by a colon:
```
var myVariable: real := 3.1415
```

You can create arrays using brackets 
```
[]
```
 and access their elements by entering the index within the brackets.
```
var myIntegerArray: integer[]
myIntegerArray.append(3)
print myIntegerArray[1]
```

See also

Declare Local Variables in the Source Code
Constant Values
Colors for Syntax Highlighting

---

#### Control Flow
         Use if and switch to create conditionals. 
         Use for, while, and repeat to create
               loops. 
         Parentheses around the condition or the loop variable are optional, meaning that you can type them, but
            you do not have to do so.
```
var ages := [34,42,18,44,53,12,63]
var countBelow30: integer
var countAbove29: integer
for var i := 1 to ages.dim
   if ages[i]  30
       countBelow30 := countBelow30 + 1
   else
       countAbove29 := countAbove29 + 1
   end
next

print "Below 30: ", countBelow30
print "Above 29: ", countAbove29
```

         Use switch if you have to check for a large amount of different
            values:
```
var currentDay := 3
switch currentDay
case 1
   print "Monday"
case 2
   print "Tuesday"
case 3
   print "Wednesday"
case 4
   print "Thursday"
case 5
   print "Friday"
case 6
   print "Saturday"
case 7
   print "Sunday"
end
```

         Use while to repeat a block of code until a condition
            changes.
```
var n := 2
while n  10
   n := n * 2
end
```

         The condition of a loop can also be located at the end instead, ensuring that
            the loop is executed at least once using the repeat loop.
```
var n := 2
repeat
   n := n * 2
until n  10
```

      
      See also
         
         Colors for Syntax Highlighting

---

#### Declare Default Arguments
You can assign default arguments, also called
optional arguments, or optional
parameters in SimTalk 2.0. If the Method is then called without the argument, the associated parameter will be set to the default value, which is defined in the Method.
```
param x: integer := 123
```
The Method can be called with or without argument. If the Method is called without argument, the parameter 
`x`
 has the value 
`123`
 in the example above.You can also assign default arguments to some of the parameters only. If a parameter has a default argument, all following parameters also have to have a default argument.
```
param a: string,
      b, c: string := "",
      d: boolean := true
```
The Method in the following example can be called with
one to four arguments, but not without any argument at all, as no default argument was defined for
the parameter 
`A`
.Possible calls are:
```
Method("A")
Method("A", "B")
Method("A", "B", "C")
Method("A", "B", "C", false)
```
Allowed Values for Default Arguments

Default arguments only accept constant values, i.e., numbers, string constants,
the boolean constants 
`true`
 and 
`false`
, 
`void`
, and

`pi`
.

Parameters of data type object,
table, list, stack, queue, and any can only have 
`void`
 as default argument. 

Parameters of data type date and
dateTime cannot have a default argument at all. 

Parameters of data type array can
have an empty array 
```
[]
```
 or an empty JSON object 
```
{}
```
 as default argument. 

Reference parameters, i.e., parameters declared by the
keyword byref, cannot have a default
argument.

See also

Declare Parameters
Colors for Syntax Highlighting

---
