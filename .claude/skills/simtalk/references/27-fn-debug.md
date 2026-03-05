> **Read this when:** Debugging: breakpoints, tracing, debug output, method debugging, `debugAssert`, `debugBreak`  
> **Skip this when:** Profiling functions (see 23) or console output (see 25)


## Contents

- [Functions for Debugging the Model](#functions-for-debugging-the-model)
  - [clearAllBreakpoints](#clearallbreakpoints)
  - [debug](#debug)
  - [deleteSuspendedMethods](#deletesuspendedmethods)
  - [getErrorStop](#geterrorstop)
  - [ignoreBreakpoints](#ignorebreakpoints)
  - [setErrorHandler](#seterrorhandler)
  - [setErrorStop](#seterrorstop)
  - [setMaxDepthOfCalls](#setmaxdepthofcalls)
  - [setMaxNumberOfCallChains](#setmaxnumberofcallchains)
  - [setMaxNumberOfSamples](#setmaxnumberofsamples)
  - [setMaxSuspendedMethods](#setmaxsuspendedmethods)

## Functions for Debugging the Model

### clearAllBreakpoints
    Deletes all class breakpoints and all instance breakpoints you have set in all Methods in your simulation model.
        
        Syntax
            
`clearAllBreakpoints`

        
        See also
            
            Delete Breakpoints in All Methods

---

### debug
   Stops the simulation run and opens the Debugger window. If
      your model contains errors you can interrupt the simulation run and debug your
      model.
      
      Syntax
         
`debug`

      
      Example
         
```
if determinante  0 
   debug
end
```

      
      See also
         
         Debug Method [button]

---

### deleteSuspendedMethods
Terminates all kinds of suspended Methods, meaning Methods that were suspended by a waituntil-statement or a
stopuntil-statement or by a sleep-instruction.
Remarks

Note 
The function does not delete the Method object itself,
but only terminates the suspended state of this Method. 

Note 
The EventController automatically terminates all suspended Methods during the reset phase of the simulation. 

```
deleteSuspendedMethods([WaitingToo:boolean:=false)]
```

Parameter

The optional parameter WaitingToo of data type boolean sets if
Methods, which are suspended via a wait instruction, will be deleted as well
(
`true`
) or not (
`false`
).
Default Value of the Parameter
The default value is false.

Example

```
deleteSuspendedMethods(true)
```

See also

Terminate Suspended Methods
Suspending Methods
Reset Simulation [EventController]

waituntil [SimTalk] and stopuntil [SimTalk]
sleep [SimTalk]

---

### getErrorStop
Gets the settings Stop on Formulas and Stop on Error Handlers and sets the passed variables to the respective
values.

Syntax

```
getErrorStop(byRef StopOnErrors:boolean, byRef StopOnErrorsInFormulas:boolean) → boolean
```

Parameters

The local variable StopOnErrors of data type boolean is the variable into which Plant Simulation
writes if Stop on Error Handlers is activated or deactivated.

The local variable StopOnErrorsInFormulas of data type
boolean is the variable into which Plant
Simulation writes if Stop on Formulas is activated or deactivated.

Return Value

The return value has the data type boolean.

Example

```
var StopOnErrors, StopOnErrorsInFormulas: boolean
getErrorStop(StopOnErrors, StopOnErrorsInFormulas)
print StopOnErrors, " ", StopOnErrorsInFormulas
```

See also

setErrorStop [SimTalk]
Stop on Error Handlers
Stop on Formulas

---

### ignoreBreakpoints
    Ignores (
`true`
) or does not ignore (
`false`
) user-defined breakpoints during your simulation run. 
        
        Syntax
            
```
ignoreBreakpoints(Ignore:boolean)
```

        
        Parameter
            
            The parameter Ignore of data type boolean designates the action to
                be taken.
        
        Example
            
```
ignoreBreakpoints(true)
```

        
        See also
            
            Ignore Breakpoints

---

### setErrorHandler
Sets the Method, whose name you enter as the parameter of data
type object, as the global error handling method. 
Remarks

The function prevents that Plant Simulation opens the Debugger when runtime errors in SimTalk methods occur.
This global error handling method will only be executed, when Plant
Simulation did not find an individual error handling for methods.
When you set a global error handling method, Plant
Simulation calls this method when runtime errors in SimTalk methods
occur. Three parameters are passed to this method: 
setErrorHandler returns the last registered error
handling method. 
When you set 
`void`
 as error handling method, Plant Simulation deactivates global error handling and the Debugger opens when runtime errors occur. 

A string with the error message. You have to declare the
string parameter as a by reference parameter.

A string with the path to the faulty Method.

An integer value that tells, which line contains the
error. 

Note 
Methods of the FlowControl and execute functions also count as formulas.

Syntax

```
setErrorHandler(Method:object) → object
```

Parameter

The parameter Method of data type object designates the Method.

Return Value

The return value has the data type object.

Examples

```
// source code of myMethod
param byref ErrorMessage:string, MethodPath:string, LineNumber:integer

print "Error in ", MethodPath, " Line ", LineNumber, ": ", ErrorMessage
ErrorMessage := ""  // catch this error
```

```
setErrorHandler(&myMethod)
```

See also

Select Template in the Method
Error Handling
Calculate Values with a Formula
getCallStack [SimTalk]
throwRuntimeError [SimTalk]

---

### setErrorStop
Activates (
`true`
) or deactivates (
`false`
) the features Stop on Formulas and Stop on Error Handlers. 

Syntax

```
setErrorStop(StopAfterError:boolean[, StopAfterErrorInFormula:boolean]) → boolean
```

Parameters

When you specify 
`true`
 for the parameter StopAfterError, Plant Simulation stops the simulation
after an error occurred in the current method and opens the Debugger with
the method containing the error and highlights the line containing the error in red. When you close
the Debugger, Plant Simulation terminates the
entire call chain. If the events list in the EventController contains any
more events, the simulation continues. 
When you specify 
`false`
, Plant Simulation terminates the entire call chain and the simulation continues.

The optional parameter StopAfterErrorInFormula of data type boolean determines
if Plant Simulation stops the simulation, when it encounters errors in formulas
(
`true`
) or if it does not stop it (
`false`
).

Return Value

The return value has the data type boolean.

Example

```
setErrorStop(false,true)
```

See also

getErrorStop [SimTalk]
Stop on Error Handlers
Stop on Formulas

---

### setMaxDepthOfCalls
    Sets the number of methods that Plant Simulation may call. 
        Remarks
            
            Each Method consumes main memory while being
                executed. Plant Simulation only releases the memory after
                the execution of a method is finished. This means that memory consumption increases
                with each method that calls another method before it finishes. The number of methods
                is the depth of calls. For example, when method A calls
                method B, and method B in turn calls method C, the depth of calls is three. If, by
                accident, method C called itself again and again, the depth of calls would be
                infinite. To avoid Plant Simulation running out of memory,
                limit the depth of calls. We found the default value 500 to be sufficient for most
                applications. 
        
        
        Syntax
            
```
setMaxDepthOfCalls(NumberOfMethods:integer) → integer
```

        
        Parameter
            
            The parameter NumberOfMethods of data type integer designates the
                number of methods that Plant Simulation may call.
        
        Return Value
            
            The return value has the data type integer.
            Is the previous value of the maximum number of suspended methods and
                does not set the new value if 
`0`
 is passed. 
        
        Example
            
```
setMaxDepthOfCalls(1500)
```

        
        See also
            
            Maximum depth of calls [preferences]

---

### setMaxNumberOfCallChains
    Limits the maximum number of call chains which Plant
            Simulation calls. 
        Remarks
            
            When Plant Simulation reaches the number you
                set, it stops the simulation and shows an error message. 
            You can then increase the Maximum number of call
                    chains and continue the simulation.
        
        
        Syntax
            
```
setMaxNumberOfCallChains(NumberOfCallChains:integer) → integer
```

        
        Parameter
            
            The parameter NumberOfCallChains of data type integer designates
                the maximum number of call chains.
        
        Return Value
            
            The return value has the data type integer.
            Is the previous value of the maximum number of call chains and does
                not set the new value if 
`0`
 is passed. 
        
        Example
            
```
setMaxNumberOfCallChains(1500)
```

        
        See also
            
            Maximum number of call chains [preferences]

---

### setMaxNumberOfSamples
    Sets the maximum number of samples to prevent Plant
            Simulation from spending an excessive amount of time for die rolls, which are
        caused by an unfortunate selection of the interval bounds.
        Remarks
            
            You can specify a number between 
`1`
 and
                    
`32000`
. Plant Simulation
                ignores values outside of this range without issuing a warning message and keeps the
                previous value. The greater the value you enter, the later you recognize if the
                bounds are too close together. For a normal distribution it may, for instance,
                happen that Plant Simulation draws extremely large values.
                When the bounds are too close together, this may result almost exclusively in
                outliers. Then Plant Simulation has to create a large
                number of random numbers consecutively before a valid value is available. This can
                take up a lot of time. 
        
        
        Syntax
            
```
setMaxNumberOfSamples(NumberOfSamples:integer) → integer
```

        
        Parameter
            
            The parameter NumberOfSamples of data type integer designates the
                maximum number of die rolls.
        
        Return Value
            
            The return value has the data type integer.
            Is the previous value of the maximum number of samples and does not
                set the new value if 
`0`
 is passed. 
        
        Example
            
```
setMaxNumberOfSamples(12)
```

        
        See also
            
            Maximum number of samples [preferences]

---

### setMaxSuspendedMethods
    Sets the maximum number of methods that may be suspended at any one time. The number
        of suspended methods by waituntil-statements is limited. 
        Remarks
            
            When Plant Simulation reaches the number you
                set, any additional methods will not suspended and Plant
                    Simulation will display an error message. 
            You can then either increase the Maximum number of
                    suspended methods and continue your simulation run or stop the
                simulation and fix the modeling error. 
        
        
        Syntax
            
```
setMaxSuspendedMethods(NumberOfSuspendedMethods:integer) → integer
```

        
        Parameter
            
            The parameter NumberOfSamples of data type integer designates the
                maximum number of samples.
        
        Return Value
            
            The return value has the data type integer.
            Is the previous value of the maximum number of suspended methods and
                does not set the new value if 
`0`
 is passed.
        
        Example
            
```
setMaxSuspendedMethods(40)
```

        
        See also
            
            Maximum number of suspended methods [preferences]

---
