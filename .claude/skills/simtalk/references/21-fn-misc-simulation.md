> **Read this when:** Simulation control: `callEvery`, event scheduling, random seeds, animation refresh, `processTime`  
> **Skip this when:** Model file operations (see 20) or UI/dialog functions (see 22)


## Contents

- [callEvery](#callevery)
- [currentEventCtl](#currenteventctl)
- [getSeedTable](#getseedtable)
- [processTime](#processtime)
- [resetRandomNumberStream](#resetrandomnumberstream)
- [setAnimationRefreshRate](#setanimationrefreshrate)
- [setAntitheticRandomNumbers](#setantitheticrandomnumbers)
- [setInfiniteLoopDetectionTimeout](#setinfiniteloopdetectiontimeout)
- [setMUTraceRouteMethod](#setmutraceroutemethod)
- [setRandomSeedCounter](#setrandomseedcounter)
- [setSeedTable](#setseedtable)
- [showStatisticsReport](#showstatisticsreport)

## callEvery
Calls all Methods with the designated name in the designated Frame and all of its sub-frames. 
Remarks

Plant Simulation stops executing the Method that contains the callEvery call, until all methods called are
executed. 
Plant Simulation searches the Frames for Methods using the depth-first strategy. It always
immediately executes Methods it encounters.

Syntax

```
callEvery(Frame:path, Method:string[, Parameters:parameters])
```

Parameters

The parameter Frame of data type path designates the Frame within
which you want to call all Methods.

The parameter Method of data type string designates the name of the
Method you want to call.

The optional parameters are passed as parameters to the calling Methods.

In our example we placed several Frames within Frames in the model. The
numbering M x indicates the sequence the Frames were inserted, i.e., Frame M 11
was placed before Frame M 12, M 111 before M 112, etc. The numbers 1 to 9 indicate the
sequence Plant Simulation searches for methods with the name specified in
callEvery. Plant Simulation always calls the more recent object first. In our
example it calls the Frames in this order: 1, 9, 2, 7, 8, 3, 6, 5, 4. 

The depth-first strategy starts with the Frame entered in Path, and then searches
through the hierarchy, using the sequence in which we inserted the Frames as a
guideline.
The function searches all hierarchy levels for methods with the name of this Method. As
soon as it finds such a method, it will be called with the designated parameters.

Example

```
callEvery(.frame2,"outputMessage",999,"here")
```

---

## currentEventCtl
   Returns the EventController that controls the current
      simulation run.
      
      Syntax
         
```
currentEventCtl → object
```

      
      Return Value
         
         The return value has the data type object. 
      
      Example
         
```
if currentEventCtl /= VOID
   print "simulation running in frame", currentEventCtl.location
   print "simulation running in frame", root
end
```

      
      See also
         
         EventController [object]

---

## getSeedTable
Returns the active Random Number Seed Values
table. 
Remarks

The first column contains the random number seed values (integer). 
The second column contains the comments to the random number seed values (string ). The number of the row matches the number of the random number
stream.
Note 
The seed values only apply to the distribution functions, such as z_uniform, z_normal, etc. 

Syntax

```
getSeedTable → table
```

Return Value

The return value has the data type table. 

Example

```
localseedtable := getSeedTable
```

See also

setSeedTable [SimTalk]
resetRandomNumberStream [SimTalk]
Random Number Seed Values
Distribution Functions, z_ functions

---

## processTime
    Returns the CPU time, which Plant Simulation used, in
        seconds.
        
        Syntax
            
```
processTime -> real
```

        
        Return Value
            
            The return value has the data type real. 
            The return value has a resolution of several milliseconds.
        
        Example
            
```
print processTime
```

        
        See also
            
            getHighResolutionClock [SimTalk]
            sysDate [SimTalk]

---

## resetRandomNumberStream
Resets a random number stream for the distribution function,
such as z_uniform, z_normal, etc.
Remarks

Each of the material flow objects automatically uses a random number stream of its
own. You can set that random number stream with the attribute RandomSeed .
You cannot access the random number streams of the objects with resetRandomNumberStream though. The random number stream, that the function passes, refers to
the distribution function, such as z_uniform, z_normal, etc.

Syntax

```
resetRandomNumberStream(Stream:integer)
```

Parameter

The parameter Stream of data type integer designates the random number stream.

Example

```
resetRandomNumberStream(5)
```

See also

Distribution Functions, z_ functions
RandomSeed [SimTalk] - material flow objects
Random Number Seed Values
setRandomSeedCounter [SimTalk]
setSeedTable [SimTalk]
getSeedTable [SimTalk]

---

## setAnimationRefreshRate
    Sets how often Plant Simulation refreshes the graphics in
        your simulation model per second. 
        Remarks
            
            You can specify a number between 
`1`
 and
                    
`100`
. 
            Depending on your model a lower number may lead to a higher simulation
                speed. A higher number results in a smooth animation which may decrease the
                simulation speed.
        
        
        Syntax
            
```
setAnimationRefreshRate(RefreshRate:integer) → integer
```

        
        Parameter
            
            The parameter RefreshRate of data type integer designates the
                refresh rate. 
        
        Return Value
            
            The return value has the data type integer.
        
        Example
            
```
setAnimationRefreshRate(50)
```

        
        See also
            
            Frame rate [preferences]

---

## setAntitheticRandomNumbers
    Sets if Plant Simulation uses antithetic random numbers (
`true`
) or
            normal random numbers (
`false`
).
        
        Syntax
            
```
setAntitheticRandomNumbers(AntitheticRandomNumbers:boolean) → boolean
```

        
        Parameter
            
            The parameter AntitheticRandomNumbers of data type boolean sets if
                    Plant Simulation uses antithetic random numbers
                    (
`true`
) or normal random numbers
                    (
`false`
). 
        
        Return Value
            
            The return value has the data type boolean.
            The return value shows the previous setting.
        
        Example
            
```
setAntitheticRandomNumbers(true)
```

        
        See also
            
            Antithetic Random Numbers

---

## setInfiniteLoopDetectionTimeout
    Sets the number of seconds which method execution might take before Plant Simulation opens the dialog telling you that you can stop
        method execution by pressing Shift+Alt+Ctrl.
        
        Syntax
            
```
setInfiniteLoopDetectionTimeout(Timeout:integer) → integer
```

        
        Parameter
            
            The parameter Timeout of data type integer designates the number of
                seconds for the timeout. Specifying 
`0`
, or a negative value, will
                deactivate infinite loop detection entirely. Otherwise the allowed minimum value is
                    
`3`
 seconds.
        
        Return Value
            
            The return value has the data type integer. 
            The return value is the previous value.
        
        Example
            
```
setInfiniteLoopDetectionTimeout(60)
```

---

## setMUTraceRouteMethod
Designates a Method or an array_of_Methods, which is called each and every time, when a MU is
moved to another object.
Remarks

Methods which are registered with setMUTraceRouteMethod
are removed from the Registry when you reset the EventController. Each model has to register its Methods anew when
initializing the model. This prevents that Methods are executed for a
model, which does not use setMUTraceRouteMethod, and which were registered
by another model.

Syntax

```
setMUTraceRouteMethod(&Method:object) → object
setMUTraceRouteMethod([array_of_Methods:any]) → object
setMUTraceRouteMethod → object
```

Parameters for a Single Method Object

The method has four parameters.

In the example below the parameter fromObject of data type object designates
the object on which the MU was located before it was moved.

The parameter fromLength of data type length designates the position of the
MU on a length-oriented object at which the MU was located before it was
moved.

The parameter fromLane of data type integer designates the lane on which the
MU was located on a TwoLaneTrack. 

The parameter time of data type time designates the point in time at which the
MU is to be moved.

Return Value

The return value has the data type object.

Example

```
param fromObject: object, fromLength: length, fromLane: integer, t: time 
var numSankeys: integer
var sankeylist: object
var toLength: length
sankeylist := rootfolder.internal.ActiveSankeyObjects
numSankeys := sankeylist.dim
for var i := 1 to numSankeys 
   sankeylist.read(i).printTrace(@,fromObject,fromLength,fromLane,?,t)
next 
```

Parameters for An Array of Methods

The parameter array_of_Methods of data type any designates an array of Method objects. 
You can also call the function setMUTraceRouteMethod without a parameter. If you specify an array of Method objects, Plant Simulation enters all Methods as callback methods and removes all previously existing callback methods from the list of callback methods.
If you call the function setMUTraceRouteMethod without parameter, it does not change the previously existing callback methods but returns an array of the previously existing callback methods.

Return Value

The return value is an array of data type object which contains all previously
existing callback methods.

Example

```
// add 'MyMethod' to the callback methods
var callbacks: object[] := setMUTraceRouteMethod() // get the already installed callback methods
callbacks.append(&MyMethod)      // add MyMethod
setMUTraceRouteMethod(callbacks) // set the previously installed methods plus MyMethod as callback methods

// remove 'MyMethod' from the callback methods
callbacks := setMUTraceRouteMethod() // get the installed callback methods
callbacks.deleteValue(&MyMethod)     // remove MyMethod from the array
setMUTraceRouteMethod(callbacks)     // set the previously installed methods minus MyMethod as callback methods

// clear all callback methods
var empty: object[]
setMUTraceRouteMethod(empty) // setting an empty array will uninstall all callback methods 
```

---

## setRandomSeedCounter
Is only required if you want to influence the automatic allocation of the random number
seed value, which normally is not required.
Remarks

When you insert an object into your model, Plant
Simulation automatically assigns a random number seed value to this object. You can query the
next assigned random seed value with the function 
```
setRandomSeedCounter(0)
```
. After the object is created, Plant
Simulation increases this counter by 1, so that the next object gets a different random seed
value. 
This guarantees that the newly inserted object uses different random numbers, for
example for processing times, for failures, etc. To facilitate this, each model has a counter that Plant Simulation increases when automatically assigning the random number seed value. Calling
the function setRandomSeedCounter with 
`0`

only returns the current counter. If you call the function setRandomSeedCounter with a value other than 0, Plant Simulation sets
the counter to this value. 
Besides, the function setRandomSeedCounter returns the
previous value of the counter. If you only want to get the current value of the counter, call the
function with 
`CounterValue=0`
.
If you set the counter to a value smaller than the previous value, it is not
guaranteed that each newly inserted object has a unique random number seed value.
This function can be useful if you want to automatically create simulation
models. You could, for example, use the Teamcenter Interface to detect the
objects within your installation to then create these objects using a Method. When you then delete the created objects and get the up-to-date information from Teamcenter and create the model anew, the created object will get different
random number seed values, even if the Teamcenter database did not change.
To use the same random number seed values, call the function setRandomSeedCounter once before creating the objects to always initialize the counter with
the same value.

Syntax

```
setRandomSeedCounter(CounterValue:integer) → integer
```

Parameter

The parameter CounterValue of data type integer designates the value of the
counter. 

Return Value

The return value has the data type integer. 
The return value is the current random seed counter.

Example

```
setRandomSeedCounter(4)
print setRandomSeedCounter(0)
```

See also

resetRandomNumberStream [SimTalk]
Random Numbers Variant
RandomSeed [SimTalk] - material flow objects

---

## setSeedTable
Sets the random number seed values for creating
the random number streams. 
Remarks

Note 
The seed values only apply to the distribution functions, such as z_uniform, z_normal, etc. 

Each of the material flow objects automatically uses a random number stream of
its own. You can set that random number stream with the attribute RandomSeed.
Note 
Plant Simulation applies the new random numbers
immediately and resets all random number streams with the new seed values.

Syntax

```
setSeedTable(SeedTable:table)
```

Parameter

The parameter SeedTable of data type table designates a table with one or two
columns or a list. 

The first column contains the random number seed values (integer). 

The optional second column contains the comments to the random number seed values
(string). The number of the row matches the number of the random number stream.

Examples

```
var t: table[integer]
t.create
t[1,6] := 1
setSeedTable(t)
```

```
var t: table[integer]
t.create
t[1,6] := 1
t[2,6] := "Explain usage"
setSeedTable(t)
```

See also

Random Number Seed Values
RandomSeed [SimTalk] - material flow objects
getSeedTable [SimTalk]
resetRandomNumberStream [SimTalk]
Distribution Functions, z_ functions

---

## showStatisticsReport
Shows the statistics report of the objects which
you type into the list.

Syntax

```
showStatisticsReport(List:list[, FileName:string])
```

Parameters

The parameter List of data type list designates the list into which you entered
the names of the objects.

The optional parameter FileName of data type string designates the name of the
file into which Plant Simulation writes the statistics values.

Example

```
showStatisticsReport(myStatisticsObjects)
showStatisticsReport(myStatisticsObjects,"My Statistics Report")
```

See also

Statistics Report [described]
