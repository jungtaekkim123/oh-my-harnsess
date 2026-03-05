> **Read this when:** Utility: `checkID`, `computeSHA*`, `createCombinations`, `createPermutations`, geometry, profiling, `execute`  
> **Skip this when:** Application environment (see 19) or model operations (see 20)


## Contents

- [Miscellaneous Global Functions](#miscellaneous-global-functions)
  - [animation](#animation)
  - [calcBrakingDistance](#calcbrakingdistance)
  - [calcDroppedPerpendicularFootPoint](#calcdroppedperpendicularfootpoint)
  - [checkID](#checkid)
  - [computeSHA1Hash](#computesha1hash)
  - [computeSHA3Hash](#computesha3hash)
  - [createCombinations](#createcombinations)
  - [createPermutations](#createpermutations)
  - [deg2rad](#deg2rad)
  - [deleteAllDebugExpressions](#deletealldebugexpressions)
  - [execute](#execute)
  - [executePythonFile](#executepythonfile)
  - [executeSilent](#executesilent)
  - [getCallStack](#getcallstack)
  - [getProfileCallCycles](#getprofilecallcycles)
  - [isSet](#isset)
  - [makeRGBValue](#makergbvalue)
  - [profiler](#profiler)
  - [putValuesIntoTable](#putvaluesintotable)
  - [rad2deg](#rad2deg)
  - [resetProfile](#resetprofile)
  - [saveProfile](#saveprofile)
  - [sendSMTPMail](#sendsmtpmail)
  - [strHash](#strhash)
  - [throwRuntimeError](#throwruntimeerror)

## Miscellaneous Global Functions

### animation
  Activates or deactivates the animation of MUs and
      States during a simulation run. 
    Remarks
      
      Calling the function without parameter returns the current state of the
        animation.
      Calling the function with parameter sets the state of the animation to
        activated (
`true`
) or deactivated (
`false`
).
    
    
    Syntax
      
```
animation → boolean
animation([Activate:boolean]) → boolean
```

    
    Parameter
      
      The optional parameter Activate of data type boolean activates
          (
`true`
) or deactivates (
`false`
) the animation of
          MUs and States.
    
    Return Value
      
      The return value has the data type boolean.
      The return value is true if the animation of MUs and States is
        activated. 
    
    Example
      
```
animation         // returns if animation is on or off
animation(true)   // activates animation
```

    
    See also
      
      MUs and States [Home ribbon]

---

### calcBrakingDistance
Calculates the required braking distance for a given speed and a given deceleration.
Remarks

The braking distance is calculated according to the formula s=1/2 v2/a.
Note 
The function is especially helpful for the Transporter.

Syntax

```
calcBrakingDistance(Speed:speed, Deceleration:acceleration) -> length
```

Parameters

The parameter Speed of data type speed designates the
speed.

The parameter Deceleration of data type acceleration designates the
deceleration.

Example

```
print calcBrakingDistance(100kmh, 10) // returns 138.888888888889m
```

Return Value

The return value has the data type length.

See also

Deceleration [SimTalk] - Transporter
SafetyZones [SimTalk]
calcBrakingDistance [SimTalk] - Transporter

---

### calcDroppedPerpendicularFootPoint
Calculates the foot of the dropped perpendicular of the point P
on the line A1-A2 and returns it.

Syntax

```
calcDroppedPerpendicularFootPoint(A1:length[3], A2:length[3], P:length[3]) -> length[3]
```

Parameters

The parameter A1 is an array of data type length with three values. It
sets the first point of the line.

The parameter A2 is an array of data type length with three values. It
sets the second point of the line.

The parameter P is an array of data type length with three values. It
designates the point for which the foot of the dropped perpendicular is calculated.

Return Value

The return value is an array with three values of data type length.

Example

```
print calcDroppedPerpendicularFootPoint([1,0.1,0.1],[2,0.2,0.4],[5,0.5,1])
// returns [4.91818181818182, 0.491818181818182, 1.27545454545455]
```

---

### checkID
    Checks if you can use an expression as the name of an object (true) or not (false). 
        
        Syntax
            
```
checkID(Expression:string) → boolean
```

        
        Parameter
            
            The parameter Expression of data type string designates the
                expression. The function considers all keywords and function calls. 
        
        Return Value
            
            The return value has the data type boolean.
        
        Example
            
```
print checkID("sin") -- returns false
```

        
        See also
            
            Keywords

---

### computeSHA1Hash
    Returns the 40-digit SHA1 hash code of the passed text.
        
        Syntax
            
```
computeSHA1Hash(Text:string) → string
```

        
        Parameter
            
            The parameter Text of data type string designates the string for
                which you would like to know the hash code. 
        
        Return Value
            
            The return value has the data type string.
        
        Example
            
```
print computeSHA1Hash("MyText") 
// returns 0e9e68d9402c96044f0f93194f7010bc2e056752
```

        
        See also
            
            computeSHA3Hash [SimTalk]
            strHash [SimTalk]

---

### computeSHA3Hash
    Returns the SHA3 hash code of the passed text. 
        Remarks
            
            computeSHA3Hash uses the SHA3-256-algorithm (NIST: FIPS
                202).
        
        
        Syntax
            
```
computeSHA3Hash(Text:string) → string
```

        
        Parameter
            
            The parameter Text of data type string designates the string for
                which you would like to know the hash code. 
        
        Return Value
            
            The return value has the data type string.
        
        Example
            
```
print computeSHA3Hash("MyText") 
// returns 27acf01aa72d499265cc50388f80054e644640586fb04c3165cd4f86d20e02a8
```

        
        See also
            
            computeSHA1Hash [SimTalk]
            strHash [SimTalk]

---

### createCombinations
Creates all combinations of the specified Length of the elements
array. 
Remarks

If a value is contained multiple times in the elements array, the result also
contains multiple combinations.

Syntax

```
createCombinations(Elements:integer[], Length:integer) -> integer[]
```

Parameters

The parameter Elements is an array of data type integer which designates the
elements of the array whose length you would like to create.

The parameter Length of data type integer designates the length of the element
designated by the parameter Elements.

Return Value

The return value is an array of data type integer.
The number of generated combinations is limited to 1,000,000.

Examples

```
// Creates all combinations with two elements
print createCombinations([1,2,3], 2) // returns [1, 2][1, 3][2, 3]
```

```
// Creates all combinations of two colors
var arrString:string[]
var arrInt:integer[]

arrString.append("red")
arrString.append("green")
arrString.append("blue")

arrInt.append(1)
arrInt.append(2)
arrInt.append(3)

var resArr = createCombinations(arrInt, 2)

var colorCombination:string

for var y := 1 to resArr.ydim
    print arrString[resArr[1, y]], ", ", arrString[resArr[2, y]]
next
```

---

### createPermutations
Creates all permutations of the specified Length of the elements
array. 
Remarks

If a value is contained multiple times in the elements array, the result also
contains multiple permutations.

Syntax

```
createPermutations(Elements:integer[], Length:integer) -> integer[]
```

Parameters

The parameter Elements is an array of data type integer which designates the
elements of the array whose length you would like to create.

The parameter Length of data type integer designates the length of the element
designated by the parameter Elements.

Return Value

The return value is an array of data type integer.
The number of generated permutations is limited to 1,000,000.

Example

```
// Creates all permutations with two elements
print createPermutations([1,2,3], 2) // returns [1, 2][1, 3][2, 1][2, 3][3, 1][3, 2]
```

---

### deg2rad
    Converts the specified angle in degrees into the respective angle in radians. 
        
        Syntax
            
```
deg2rad(AngleInDegrees:real) -> real
```

        
        Parameter
            
            The parameter AngleInDegrees of data type real designates the angle
                in degrees which you would like to convert into the angle in radians.
        
        Return Value
            
            The return value has the data type real.
        
        Example
            
```
print deg2rad(45) // returns 0.785398163397448
```

        
        See also
            
            rad2deg [SimTalk]

---

### deleteAllDebugExpressions
    Deletes all debug expressions in all methods.
        
        Syntax
            
`deleteAllDebugExpressions`

        
        Example
            
`deleteAllDebugExpressions`

---

### execute
Receives a string and interprets it as though it were the source
code of a method. 
Remarks

The function execute accepts all statements. The anonymous
identifier ? refers to the Method
object that called the execute function. The anonymous identifier @ is received by the calling method. 
The function execute runs the referenced Method. Use execute to run Methods that you referenced via variables. Let us say you save a Method to a variable obj of data type object, you can then call this Method using obj.execute.
Note 
The syntax, which is used in the argument for the execute function, has to be the same as the Method syntax which calls
the execute function.

The semantics of execute is as follows:

If a runtime error occurs while the string method is being executed, there are
two possibilities:

If the setting Ignore Errors in Formulas is deactivated,
Plant Simulation opens the Debugger.

If the setting Ignore Errors in Formulas
is activated, the function execute acts like the function
executeSilent.

If no runtime error occurs:

If the string method does not have a return value, execute returns VOID.
```
var objPath : string := "Track"
var attrName: string := "Length"
var attrVal : length := 3.5
execute(to_str(objPath, ".", attrName, ":=", attrVal))
```

In all other cases, execute will return the return value
of the string method.
```
execute("-> integer; return 42") // returns 42 
```

You can also pass parameters to the execute
statement.
```
execute("param x, y: integer; print x+y", 1, 2) // outputs 3 
`Syntax`
execute(SourceCode:string[ ,Parameter:parameter, ...])
```

See also

executeSilent [SimTalk]
Ignore

---

### executePythonFile
    Executes the source code of the specified Python file.
        Remarks
            
            You can access the objects in your Plant
                    Simulation model in the same way as you would when executing the Python
                code using a PythonModule.
        
        
        Syntax
            
```
executePythonFile(File:string) -> boolean
```

        
        Parameter
            
            The parameter File of data type string designates the Python file
                that contains the source code that you would like to execute.
        
        Return Value
            
            The return value has the data type boolean. 
            It is true if no error occurred while executing the source code in the Python file.
                It is false if an error occurred.
        
        Example
            
```
print executePythonFile("D:\test.py", "TestArg")
```

        
        See also
            
            Execute External Python Code

---

### executeSilent
Receives a string and interprets it as though it were the source code of a method. 
Remarks

The function executeSilent accepts all statements. The
anonymous identifier ? refers to the Method object that called the executeSilent function. The anonymous
identifier @ is received by the calling method. 
The semantics of executeSilent is as follows:

If the string method does not have a return value, executeSilent returns VOID.
```
var objPath : string := "Track"
var attrName: string := "Length"
var attrVal : length := 3.5
executeSilent(to_str(objPath, ".", attrName, ":=", attrVal))
```

If the string method has a return value, these may look
as follows:

If the string method contains a syntax error, executeSilent returns VOID. 
```
executeSilent("-> integer; 1+") // returns VOID 
```

If a runtime error occurs while the string method is executed, executeSilent returns the default value of the corresponding type, i.e., the
value of a local variable of this type would have at the beginning of the execution of the method.
Plant Simulation does not open the Debugger when a
runtime error occurs, but continues to be executed. 
Use the function execute to make Plant
Simulation open the Debugger, when runtime errors occur. For example,
the executeSilent-statement below returns false because assigning the
keyword "if" to the name of an object causes a runtime error. 
```
executeSilent("->boolean; Station.name := \"if\"; return true")
// returns false because of a runtime error 
```

In all other cases, executeSilent will return the return
value of the string method.
```
executeSilent("->integer; return := 42") // returns 42
```

You can also pass parameters to the executeSilent
instruction.
```
executeSilent("param x, y: integer; print x+y", 1, 2) // returns 3
```

The function executeSilent executes the referenced Method. You can use it to execute Methods that you
referenced via variables. Let us say you save a Method to a variable obj of data type object, you can now call this Method using obj.executeSilent. 
```
param obj: object, new_name: string
if not executeSilent("param o: object -> boolean; o.name := \"" + new_name + "\"; return true" obj) 
   print "invalid name"
end 
`Be aware that the variant`
executeSilent("->boolean; " + obj + ".name := \"" + new_name + "\"; return true") 
`does not work, when`
obj
```
 points to a method.
The syntax which is used in the argument for the executeSilent function has to be the same as the Method syntax which
calls the executeSilent function.

Syntax

```
executeSilent(SourceCode:string[ ,Parameter, ...])
```

See also

execute [SimTalk]

---

### getCallStack
Returns the active call stack, and writes it to a table. 
Remarks

The first column is of data type string and contains the
absolute path of the method. 
The second column is of data type integer and contains the
row number of the executed SimTalk instruction.
Note 
If getCallStack is called in a local ErrorHandler, the function returns the call stack of the faulty method and not the call stack
of the ErrorHandler.

|  |  |

Syntax

```
getCallStack → list
```

Return Value

The return value has the data type list. 

Example

```
var tab: table
tab := getcallStack
```

See also

Tab Call Stack [Watch window]
Error Handling
setErrorHandler [SimTalk]

---

### getProfileCallCycles
    Returns a JSON object containing the call cycles that Profiler collected provided it is activated.
        
        Syntax
            
```
getProfileCallCycles([getProfileCallCycles:integer]) -> json
```

        
        Parameter
            
            The optional parameter MaxNumCycles of data type integer restricts
                the amount of call cycles which getProfileCallCycles returns.
            To return all call cycles, do not specify the parameter. The amount
                of returned data can be very large and that the call can take a long time to
                finish.
        
        Return Value
            
            The return value has the data type json. 
        
        Example
            
```
print getProfileCallCycles(10)
```

        
        See also
            
            Activate Profiler
            profiler [SimTalk]
            Activate Profiler

---

### isSet
Returns if the value of a built-in attribute in Plant Simulation
is set (true ) or not (false). 
Remarks

Examples for such attributes are the values of the drop-down lists in the dialogs
of the objects. You can also access these settings in the window Show
Attributes and Methods by double-clicking the respective attribute and selecting a value
in the drop-down list.
|  |  |
The attribute ResourceType
of the material flow objects can, for example, take the values Production/Produktion, Transport/Transport, or
Storage/Lagerung, depending on the model
language and the setting you selected for Display down-list boxes in the
SimTalk language of the model. 

Syntax

```
<Path>.isSet(ValueOfTheAttribute:string) → boolean
```

Parameter

The parameter ValueOfTheAttribute of data type string designates the value of
the attribute.

Return Value

The return value has the data type boolean.

Example

```
print MyStation.ResourceType 
// the value is Storage, outputs Storage or Lagerung in the Console

print MyStation.ResourceType.isSet("Storage") 
// checks, independent of the model language, if the value is Storage or Lagerung
```

See also

putValuesIntoTable [SimTalk]
Model language [model settings]
Display down-list boxes in the SimTalk language of the model

---

### makeRGBValue
Generates the RGB color values of the specified color.
Remarks

You can use the RGB values in the methods drawEllipse, drawLine,
drawRectangle and drawText, the attribute BackgroundColor and the
attribute Color of the objects Connector, Variable, Comment, and Display designated by
<Path> to efficiently define colors.

Syntax

```
<Path>.makeRGBValue(Red:integer, Green:integer, Blue:integer) → integer
```

Parameters

The parameter Red of data type integer designates its
red component of the color.

The parameter Green of data type integer designates its
green component.

The parameter Blue of data type integer designates its
blue component. 

You can specify an integer number between 
`0`
 and 
`255`
.
Instead of directly typing the values for the color components into the source
code of the Method, you can also press Ctrl and the spacebar to open the dialog Colors.
Then, select the color in the dialog, and click OK. Plant Simulation then inserts the color values into the method.
|  |  |
If you already defined a color by setting its color values, Plant Simulation recognizes it, selects it in the dialog Colors, and transfers its values for red, green, and blue into the source code of your
Method. 
Compare this example:
```
var rgb: integer := makeRGBValue(0,0,255)
```

If you hold down Ctrl and press the
spacebar in the Method Editor, Plant Simulation
recognizes the color values, and selects the color blue in the dialog Colors.
If you then select the color red in the dialog Colors, for example, and
click OK, Plant Simulation automatically enters the color values of
the color red into the source code of your Method, namely:
```
var rgb : integer := makeRGBValue(255,0,0)
```

Return Value

The return value has the data type integer.

Example

```
.Models.Model.BackgroundColor.Color := makeRGBValue(110,0,200)
.Models.Model.Connector.Color := makeRGBValue(100,0,200)
.Models.Model.Comment.Color := makeRGBValue(110,0,200)
.Models.Model.Display.Color := makeRGBValue(110,0,200)
.Models.Model.&Variable.Color := makeRGBValue(110,0,200)
```

See also

drawEllipse [SimTalk]
drawLine [SimTalk]
drawRectangle [SimTalk]
drawText [SimTalk]
BackgroundColor [SimTalk] - Frame
Color [SimTalk] - Connector

---

### profiler
Activates or deactivates the Profiler. 
Remarks

While it is active, it continuously collects information pertaining to the
frequency of calls and the runtime of methods.

Syntax

```
profiler(Activate:boolean)
```

Parameter

The parameter Activate of data type boolean activates (
`true`
)
or deactivates (
`false`
) the Profiler.

Example

```
profiler(true) // activate Profiler 
```

See also

| Activate Profiler | getProfileCallCycles [SimTalk] || Show Profiler Data [button] | resetProfile [SimTalk] || Reset Profiler | saveProfile [SimTalk] |

---

### putValuesIntoTable
Writes the values of an attribute of data type string, which can
only take certain values predefined in Plant Simulation, into a
table.
Remarks

Examples for such attributes are the values of the drop-down lists in the dialogs
of the objects. You can also access these settings in the window Show Attributes and
Methods by double-clicking the respective attribute and selecting a value in the
drop-down list.
|  |  |
The attribute ResourceType of the material flow objects can, for
example, take the values Production/Produktion, Transport/Transport, or Storage/Lagerung, depending on the Model language and the
setting you selected for Display down-list boxes in the SimTalk language of the
model. 
The function returns the values according to the Model
language  you selected and which you can also query with the function
language.

Syntax

```
putValuesIntoTable(TargetTable:table)
```

Parameter

The parameter TargetTable of data type table designates the target table.

Example

```
var lst: list[string]
MyStation.ResourceType.putValuesIntoTable(lst)
MyDialog.setList("My drop-down list box",lst)
```

The result looks like this after the values have been filled into the drop-down list:

Note 
You can query if the value, which you enter, is selected without having to query
the selected model language with the function isSet.

See also

Show Attributes and Methods [described]
ResourceType [SimTalk]
Display down-list boxes in the SimTalk language of the model
Model language [model settings]
language [SimTalk]
isSet [SimTalk]

---

### rad2deg
    Converts the specified angle in radians into the respective angle in degrees. 
        Title
            
            Function
        
        Syntax
            
```
rad2deg(AngleInRadians:real) -> real
```

        
        Parameter
            
            The parameter AngleInRadians of data type real designates the angle
                in radians which you would like to convert into the angle in degrees.
        
        Return Value
            
            The return value has the data type real.
        
        Example
            
```
print rad2deg(0.785398163397448) // returns 45
```

        
        See also
            
            deg2rad [SimTalk]

---

### resetProfile
Deletes all data collected by the Profiler up until the time at
which you reset the model. 
Remarks

Call this function before activating the Profiler to only
record valid data for the active simulation run. 

Syntax

`resetProfile`

Example

`resetProfile`

See also

| Activate Profiler | profiler [SimTalk] || Show Profiler Data [button] | saveProfile [SimTalk] || Reset Profiler |  |

---

### saveProfile
Saves all data collected by the Profiler to the designated file.
Any existing contents of the file will be overwritten. 
Remarks

You can print this file or load it into a Method
object.
If you deactivate the safety setting File > Model
Settings > General > Prohibit access to the computer, the function saveProfile can copy data from another folder and write them to the model
folder or its sub-folders. The function cannot copy files from the model folder or its sub-folders. 

Syntax

```
saveProfile(FileName:string[, IncludeTop50CallCycles:boolean]) → boolean
```

Parameters

The parameter FileName of data type string designates the path to the file. Any
existing content of the file will be overwritten.

The optional parameter IncludeTop50CallCycles of data
type boolean sets if the Top 50 Call Cycles will be
written to the file (
`true`
) or not (
`false`
).

Return Value

The return value has the data type boolean.

Example

```
saveProfile("C:\Users\Jeff\MyRun1.txt")
```

See also

Prohibit access to the computer [model settings]
Top 50 Call Cycles
| Activate Profiler | profiler [SimTalk] || Show Profiler Data [button] | resetProfile [SimTalk] || Reset Profiler |  |

---

### sendSMTPMail
Sends an e-mail via the denoted mail server to the designated address. 
Remarks

If you deactivate the safety setting File > Model
Settings > General > Prohibit access to the computer, Plant
Simulation does not execute the function sendSMTPMail and shows an
error message. 

Syntax

```
sendSMTPMail(Mail-Server:string, Receiver:string, Subject:string, MessageText:string)
```

Parameters

The parameter Mail-Server of data type string designates the mail server. 

The parameter Receiver of data type string designates the receiver of the mail.

The parameter Subject of data type string designates the subject of the mail.

The parameter MessageText of data type string designates the message text of
the mail. 

Example

```
sendSMTPMail("mail.company.com", "John.Smith@abc.org", "Test", "Hello John, the smoke test was successful.")
```

See also

Prohibit access to the computer [model settings]

---

### strHash
Calculates the hash value from the passed string. 
Remarks

The value is located between 0 and 2147483647 (including both thresholds). The
hash function is case-sensitive. If you do not want this, convert the string to lower case with the
function strToLower beforehand.
You might, for example, use the hash value to find a string very fast. Comparing
integer numbers is faster than comparing strings. The hash value generation is not a bijective
function, i.e., it is not unambiguously reversible.
Once you have found the hash value, you should then compare the strings. If you
want to map the hash value to a smaller value range, i.e., if you want to program a hash table, you
should use the modulo value of the hash value.

Syntax

```
strHash(string) → integer
```

Return Value

The return value has the data type integer.

Example

```
var hashTable: any[7]
var emptyStringArray: string[]
for var i := 1 to hashTable.dim
   hashTable[i] := emptyStringArray
next
hashTable[strHash("Source")   mod 7 + 1] := ["Source"]
hashTable[strHash("Drain")    mod 7 + 1] := ["Drain"]
hashTable[strHash("AssemblyStation") mod 7 + 1] := ["AssemblyStation"]

var SourceFound: boolean := hashTable[strHash("Source") mod 7 + 1].find("Source") /= 0
var BufferFound: boolean := hashTable[strHash("Buffer") mod 7 + 1].find("Buffer") /= 0
```

See also

strToLower [SimTalk]
computeSHA1Hash [SimTalk]
computeSHA3Hash [SimTalk]

---

### throwRuntimeError
  Returns an error message to the calling Method in library
    methods. This is, for example, the case if the library method was called with parameter values
    that are not allowed. 
    Remarks
      
      You can also use the function outside of libraries. When the function throwRuntimeError is called, Plant Simulation
        opens the Method Debugger for the calling Method and shows the message that was passed to throwRuntimeError. In case the Method does not run as a
        subroutine, i.e., if no caller exists, Plant Simulation opens the
          Method Debugger at the position which contains the function throwRuntimeError. If the method is encrypted, Plant Simulation opens a message box instead that shows the message.
      If the Method that executes throwRuntimeError is part of a library, Plant Simulation
        returns the call chain up to the point at which the first Method
        was found which does not belong to this library. For this Method
        Plant Simulation then opens the Method
          Debugger. If the Method that executes throwRuntimeError does not belong to a library, Plant
          Simulation opens the Method Debugger for the first direct
        caller of the Method.
      If an error handling method (ErrorHandler) exists,
          Plant Simulation does not open the Method
          Debugger or the message window respectively, but instead executes the error handling
        method. The search for an error handling method starts at the Method for which the Method Debugger would open. If this
          Method does not have an error handling method, Plant Simulation goes back in the call chain until it finds a local
        error handling method. If none of these Methods in the call chain
        has a local error handling method, it instead calls the global error handling method. If no
        global error handling method exists either, then Plant Simulation
        opens the Method Debugger or the message window as described
        above.
    
    
    Syntax
      
```
throwRuntimeError(ErrorMessage:string)
```

    
    Parameter
      
      The parameter ErrorMessage of data type string sets the error message
        that Plant Simulation shows.
    
    Example
      
```
param NewPosition : length
// the method drives the hook of the crane to a new position

if NewPosition < 0 or NewPosition > MyCrane.MyCraneArmLength
   throwRuntimeError("invalid crane position")
end

// set the new position ...
```

    
    See also
      
      Error Handling
      Calculate Values with a Formula
      getCallStack [SimTalk]
      setErrorHandler [SimTalk]
