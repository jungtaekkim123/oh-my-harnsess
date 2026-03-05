> **Read this when:** `if`/`else`, `for`, `while`, `repeat`, `switch`/`case`, `waituntil`, `try`/`catch`, `prio`, exception handling  
> **Skip this when:** Operator precedence (see 11) or function API reference (see 13-27)


## Contents

- [Control Flow Statements](#control-flow-statements)
  - [Branching with if-else-end](#branching-with-if-else-end)
  - [Multiple Branching with if-elseif-end](#multiple-branching-with-if-elseif-end)
  - [Conditional Expressions with when-then-else](#conditional-expressions-with-when-then-else)
  - [Check for a Large Amount of Different Values with switch](#check-for-a-large-amount-of-different-values-with-switch)
  - [Exiting Methods with the Keyword return](#exiting-methods-with-the-keyword-return)
  - [Error Handling](#error-handling)

## Control Flow Statements

### Control Flow Statements
A control is not always executed linearly. Different events influence the course of
execution a control takes and require an appropriate reaction. Plant
Simulation provides language constructs for programming control flow statements.

Branching with if-else-end

Multiple Branching with if-elseif-end

Conditional Expressions with when-then-else

The control flow statement Check for a Large Amount of Different Values with switch [SimTalk]

Loops [SimTalk]

waituntil [SimTalk] and stopuntil [SimTalk] for suspending Methods

---

### Branching with if-else-end
        The 
`if`
-statement uses the given condition to
                decide where to continue: Either with the following statements or with the
                statements in the 
`else`
 branch. 
                        Branching is terminated with the keyword 
`end`
. Plant
                                        Simulation executes the 
`statement_list1`
 if the condition is true, otherwise it executes 
`statement_list2`
 after 
`else`
. If you did not program the
                                        
`else`
 branch because you do
                                not need it, Plant Simulation continues the
                                execution with the first statement after branching. A 
`statement_list`
 consists of assignments, method calls, loops, or additional branches. There is no nesting limit.
        Syntax
            
```
if condition 
   statement_list1 
[else
   statement_list2]
end
```

        Examples with an else branch

Within the 
`condition`

                                Plant Simulation checks if the Transporter has reached its destination
                                        (
`@.destination = current`
).
                                If the condition is true, the control
                                transfers a MU to the workstation. If the
                                condition is false, the Transporter moves on.
```
// Is this delivery destined for us?
if @.destination = current  // yes, then unload
   @.Cont.move(workstation)
else                        // if not, then move on
    @.move(current.succ(1))
end
```

```
var ages := [34,42,18,44,53,12,63]
var countBelow30: integer
var countAbove29: integer
for var i := 1 to ages.dim
   if ages[i] < 30
       countBelow30 := countBelow30 + 1
   else
       countAbove29 := countAbove29 + 1
   end
next

print "Below 30: ", countBelow30
print "Above 29: ", countAbove29
```

Example without an else branch

The 
`condition`
 of the branching returns true when MUs are located on the Transporter. In this case one MU is going to be moved from the Transporter to the workstation. If the Transporter is empty, nothing happens. 
```
if @.NumMU > 0 // parts here? 
   @.Cont.move(workstation)
end
```

        See also
            
                        else [SimTalk]
            Edit ribbon tab of the Method > Select Template > if-else
            Edit ribbon tab of the Method > Select Template > if-else-end

---

### Multiple Branching with if-elseif-end
   At times a simple distinction between true and false will not suffice for handling all modeling situations. Then, you
      can use the 
`elseif`
to select one of several possibilities.SimTalk analyzes the conditions one after the other until
            one condition is true. Then it executes the respective
            statement. If no condition is true, SimTalk executes the optional else branch. If there is no else branch,
               Plant Simulation continues after the final 
`end`
. 
      Syntax
         
```
if condition1 
   statement_list1 
elseif condition2 
   statement_list2
[...]
[else
   statement_list3 ]
end
`Example`
// Is this part destined for us? 
if transporter.destination = current 
// yes, look for available workstation
   if Station_1.empty 
       transporter.Cont.move(Station_1)
    elseif Station_2.empty 
       transporter.Cont.move(Station_2)
    elseif Station_3.empty 
       transporter.Cont.move(Station_3)
    else // no idle Station
       transporter.move(current.succ(1))
    end
else // the shipment is not for us
    transporter.move(current.succ(1))
end // end of multiple branching
```

      
      See also
         
         else [SimTalk]
         elseif [SimTalk]
         Edit ribbon tab of the Method > Select >
               Template > if-elseif-end

---

### Conditional Expressions with when-then-else
The 
`when`
-
`then`
-
`else`
-statement selects
an expression based on the value of a boolean expression.
Syntax

`when condition then expression1 else expression2`

The syntax description reads like this:

The statement 
`condition`
 is a boolean expression.

The statement 
`expression1`
 is the expression that is to be selected if the

`condition`
 is true.

The statement 
`expression2`
 is the expression that is to be selected if the

`condition`
 is false.

Examples

```
@.color := when ?.EntranceLocked then "red" else "green"
```

```
Method(x, y + (when dy > 0 then y+dy else 100))
```

See also

when [SimTalk]-then [SimTalk]-Restore Original Size

---

### Check for a Large Amount of Different Values with switch
   The control structure 
`switch`
 enables Plant
         Simulation to make easier and clearer choices when being confronted with several
      possible choices. This way you do not have to use lengthy if-elseif-end-chains. 
      Syntax
         
```
switch expression
   case constant_list statement_list 
   [case constant_list statement_list ...]
   [else statement_list]
end
`Examples`
param number: integer
switch number
   case 1 
      print "not a prime number"
   case 2,5,7,3 
      print "prime number"
   case 9,4 
      print "square number"
   else
      print "no special number"
      print "or number greater than 9"
end 
```

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
`Values of Data Type String`
var ProductColor : string := "Green"
switch strToLower(ProductColor)
case "green"
    print "Product color is green."
case "blue"
    print "Product color is blue."
end
```

         For values of data type string
            the switch instruction distinguishes between upper and lower
            casing. 
         
      
      Values of Data Type Real
         
         For values of data type real the
               switch instruction does not check for exact equivalence. 
         For if instructions you can decide if you want
            to check for exact equivalence or if you want to permit a tolerance for epsilon by using 
`=`
 (equal to) or 
`~=`
 (about
            equal). 
         switch instructions do not support this. As the
            epsilon value permits comparatively great differences, we decided to not use it for switch instructions. Instead, we ignore the last significant
            digit of the internal floating point display which will be rounded while displaying it
            and which you thus normally cannot see.
```
var x := 1.0000000000000004

print x      // outputs 1
print x - 1  // outputs 4.44089209850063e-16

if x = 1.0
   print "x = 1.0"
elseif x ~= 1.0
   print "x ~= 1.0"  // will be reached
else
   print "x /= 1.0"
end

switch x
case 1.0
   print "case 1.0"  // will be reached
else
   print "x /= 1.0"
end
```

      Range of Definition

The term 
`expression`
 can be as complex as you need it to be. The data type of the result can be integer, real, or string. 
Course of Execution

SimTalk analyzes the expression one time and converts it into the data type of the constant. If this is not possible, Plant Simulation shows an error message. It then executes the case branch, whose list of constants contains the result of the expression. 
If no constant fits and the switch instruction contains
            an else branch, it executes the source code of the else branch. 
The order of the when-statements and the order of the constants in the when-statements does not affect the speed with which the switch instruction is being executed.

      SimTalk
         
         switch [SimTalk]
         case [SimTalk]
         Tolerance for about equal (~=) comparison [model settings]
         setEpsilon [SimTalk]
      
      See also
         
         Edit ribbon tab of the Method > Select
               Template > switch-case-end
         Edit ribbon tab of the Method > Select
               Template > switch-case-else-end
         Relational Operators

---

#### Loops
   Plant Simulation provides the 
`while`
, the
         
`repeat`
, and the 
`for`
 loop.

while loop [SimTalk]
               

repeat loop [SimTalk]
               

for loop [SimTalk]
               

You can Exit a Loop with exitLoop

---

#### while loop
   Plant Simulation executes the instruction within the while-loop several times as long as the condition is fulfilled. Plant Simulation checks the condition before each loop iteration. If
      the condition is not even fulfilled on the first iteration, the instructions within the loop
      will not be executed at all. Remarks
         If the condition never results in the value false, the
            loop will be executed infinitely. Press Ctrl+Alt+Shift to stop the infinite loop and to open the Method-Debugger.
      Examples
         
```
param n: integer -> integer  // computes the factorial of n 
result := 1
while n > 1 
   result := n * result
   n -= 1
end
```

```
var n := 2
while n < 10
   n := n * 2
end
```

      
      See also
         
         Edit ribbon tab of the Method > Select
               Template > while-end
         Exit a Loop with exitLoop
         while [SimTalk]
         repeat loop [SimTalk]

---

#### repeat loop
   Plant Simulation executes the instruction within the repeat-loop one or more times. Plant
         Simulation checks the condition after each loop iteration and only exits the loop when
      the condition is fulfilled. For this reason the loop will always be executed at least once. Remarks
         If the condition never returns true, the loop will be
            executed infinitely. Press Ctrl+Alt+Shift to stop
            the infinite loop and to open the Method-Debugger.
      Example
         
```
var x: length
repeat
   x := methodEnterLength
until x >= 0
```

      
      See also
         
         Edit ribbon tab of the Method > Select
               Template > repeat-until
         Exit a Loop with exitLoop
         repeat [SimTalk]
         while loop [SimTalk]

---

#### for loop
   The for-loop iterates through a range between
      a start value and an end value. Remarks
         
         The loop declares a loop variable of data type integer. The loop variable is initialized
            with a start value. At the end of the loop, Plant Simulation
            automatically increases the loop variable by 1. The loop is
            executed as long as the loop variable is less than or equal to
            the end value. If the end value is less than the start value, Plant
               Simulation does not execute the loop at all. 
         The loop variable is only visible within the
            loop. After the loop is executed, you cannot access the loop
               variable anymore.
         Note 
            For performance reasons Plant Simulation
               evaluates the start value and end value only once!
         
```
for var y := 1 to table.yDim 
   print table[1,y]
next
`Use the keyword`
downto
```
 instead of the
            keyword 
`to`
 to iterate through a range backward. Plant Simulation reduces the loop variable by 1 each time. Plant Simulation executes the loop as long as the loop variable is greater than or equal to the end value. If the
            end value is greater than the start value, Plant Simulation
            does not execute the loop at all.
```
for var y := table.yDim downto 1 
   print table[1,y]
next 
```

         The loop variable is only visible within the
            loop. Outside of the loop the identifier instead points to an object with this name if
            this object exists, for example to a global variable.
```
// the loop variable 'i' is only visible inside of the loop
for var i := 1 to ParallelStation.NumMU 
   print ParallelStation.MU(i)
next

print i // the loop variable is not visible here, consequently 'i' must be the name of an object

// another loop with its own loop variable 'i'
for var i := ParallelStation.NumMU downto 1 
   print ParallelStation.MU(i)
next

// the local variable 'i' is visible from here to the end of the source code
var i := 1.234
print i // prints 1.234

for var i := 1 to 10  // does not compile, because 'i' is already declared
next
```

         You can also use a local variable of data type
               integer as the loop variable. Then
            omit the keyword 
`var`
 or 
`local`
 respectively.
```
var y: integer
for y := Table.yDim downto 1 
   if Table[1,y] > 100
      exitloop
   end
next
print y // outputs the index of the first table value greater than 100
```

      
      See also
         
         Edit ribbon tab of the Method > Select
               Template > for-next
         Exit a Loop with exitLoop
         for [SimTalk]

---

#### Exit a Loop with exitLoop
   The keyword exitLoop exits a loop.
      Optionally, you can set the number of loops to be exited by specifying an integer number, for example 
```
exitloop 2 // two
      loops
```
.
      Examples
         
```
for var y := 1 to DataTable.yDim
   for var x := 1 to DataTable.xDim
       if DataTable[x,y] ~= "looking for this"
         print x, " ", y
         exitloop // exits the inner loop
      end
   next
next
```

```
for var y := 1 to DataTable.yDim
   for var x := 1 to DataTable.xDim
       if DataTable[x,y] ~= "looking for this"
         print x, " ", y
         exitloop 2 // exits the inner and outer loop
      end
   next
next
```

      
      See also
         
         exitloop [SimTalk] - keyword

---

#### Suspending Methods
The execution of a Method can be interrupted for a number of
reasons. A Method might, for example, call another Method, or it may move a MU onto an object for which you
programmed an entrance control. The execution of the Method will then be interrupted until the entrance
control is executed, and will be continued once the entrance
control is finished.Another possibility would be to conditionally suspend the execution of a Method. It stops the execution until a certain condition is fulfilled. Other
Methods can then be executed independent of the suspended Method. As soon as the condition is fulfilled, the execution of all Methods will be interrupted and the execution of the suspended Method will be continued.The waituntil-instruction and the stopuntil-instruction allow you to suspend the execution of a method according to a condition you define. If this condition is not true, the interpreter saves the entire call chain, including parameters and local variables, and either starts to execute other Methods or continues the simulation run. As soon as the condition is true, the interpreter starts executing the suspended Method at the place in the source code at which it was suspended. An observer can watch this and initiate the appropriate action.Let’s illustrate this with an example: The interpreter executes MethodA and comes across a 
`waituntil`
 instruction. The condition is not true, thus the interpreter suspends MethodA. Then, it executes MethodB, which changes the model during its execution, so that the condition for MethodA is true. At this time, the interpreter immediately interrupts MethodB, reactivates MethodA and executes it. Then, the interpreter resumes executing MethodB.The 
`waituntil`
-statement and the 
`stopuntil`
-statement behave differently when several methods are to be activated at the same time. Then, it might happen, that after the Method with the highest priority has been executed, the condition for the other Methods takes the value false again.

For Methods that were suspended with 
`waituntil`
 a new evaluation of the condition and the priorities for each additional Method to be woken up takes place after processing each Method that has been woken up. 

Methods that were suspended with 
`stopuntil`
 will be woken up in any case when the condition has been fulfilled once. This
means that no new evaluation of the condition takes place. 

If a Method is being executed during the reset phase and suspends itself with a wait instruction, Plant Simulation deletes the suspension at the end of the reset phase.A Method that is suspended by a waituntil-statement or by a stopuntil-statement, by a wait-instruction, or by a sleep-instruction, shows a tooltip in the Frame window.The tooltip shows:

The Caller of the method, in our case the ExitContr

The Suspended instruction, in our case 
`waituntil SP.empty prio @.ID wait 5:00 ? = PP`

The number of suspended methods, in our case the ExitContr is suspended three times

Compare the sample models in the Examples Collection.|  |  |
See also

waituntil [SimTalk] and stopuntil [SimTalk]
Interrupting Method Execution with Wait
Time Limitation for Waituntil and Stopuntil
Watchable Values
Create and Delete an Observer
Maximum number of suspended methods [preferences]
Maximum depth of calls [preferences]
Maximum number of call chains [preferences]

---

#### waituntil and stopuntil
The waituntil/stopuntil-statements suspend method execution until
the condition set in the statement evaluates to true.Remarks
 The simulation continues running, and that other Methods
can be executed during this time. As soon as the condition is fulfilled, the suspended Method will be woken up immediately and its execution will be continued. If Methods are being executed at the point in time at which the condition is
fulfilled, their execution will be interrupted and will only then be continued after the Method, that has been woken up, has been executed all the way.The waituntil/stopuntil-statement can also observe expressions for which only the last part of the path is watchable, for example 
`Station.Origin.Name`
.The statements consists of:
```
waituntil condition [prio number] [wait timespan:time]
stopuntil condition [prio number] [wait timespan:time]
```

The keyword waituntil or stopuntil respectively

A condition (a boolean expression)

The optional keyword prio, and an integer expression used to analyze the priority.

The keyword wait if you
want to set a time limit after which the statement will be woken up, although the condition has not
been fulfilled yet. Use the keyword waitExpired to query if the time-span has elapsed or not.
Note 
Do not use these statements within a formula. In a formula the interpreter cancels the execution of the Method with an error message.

If you want to wake up several suspended Methods simultaneously, it might happen, that after the Method with the highest priority has been executed, the condition for the other Methods takes the value false again.

For Methods that were suspended with 
`waituntil`
 a new evaluation of the condition and the priorities of for each
additional Method to be woken up takes place after processing each Method that has been woken up. 

Methods that were suspended with 
`stopuntil`
 will be woken up in any case when the condition has been fulfilled once. This
means that no new evaluation of the condition takes place. 

When you reset your simulation model, Plant Simulation deletes suspensions of Methods, which are located in the same Frame as the EventController or in a sub-Frame of this Frame. It also deletes suspensions of Methods, whose caller (the anonymous identifier ?) is located in the same Frame as the EventController or in a sub-Frame of this Frame. This means that when you reset an EventController, Plant Simulation no longer deletes suspensions of Methods of other simulation models within the model file.The waituntil/stopuntil-statement are not event-based, so no EventController is required, as compared to the wait-statement, which does require an EventController.A Method that is suspended by a waituntil-statement or by a stopuntil-statement shows this in the tooltip in the Frame window.If you add a comment after a waituntil-statement, a stopuntil-statement, a wait-statement, or a sleep-statement to the source code of your Method and if this comment starts with three hyphens 
`---`
 or with three forwards slashes 
```
///
```
, Plant Simulation does not show the entire statement on the Tab Suspended of the Watch Window and of the Method Debugger, but only the comment.The method deleteSuspendedMethods deletes all suspensions of all methods.Plant Simulation shows a suspended Method with a purple LED .3D shows the state as a colored rectangle on the top border of the icon.Compare the sample models in the Examples Collection.|  |  |
See also

Condition [SimTalk]
Priority [method execution]
Waking up Methods
Simultaneously Waking up Several Methods
Create and Delete an Observer
Simultaneously Waking up Several Methods with waituntil
Simultaneously Waking up Several Methods with stopuntil
Maximum number of suspended methods [preferences]

---

#### Condition
The expression that you enter into waituntil/stopuntil-statements
determines under which condition the interpreter continues executing the Method.Remarks
If the condition is true, the interpreter continues the execution with the next statement. If the condition is false, the interpreter suspends the Method and monitors the individual components of the expression. If one component changes, the interpreter restarts the Method, so that the condition can be analyzed again. Let’s illustrate this with a example: A Transporter is to load a MU
and to drive on afterward. However, we do not know if the Transporter or
the MU arrives at the station first. To solve this problem, we can either
enter exit controls into the Transporter and the MU, checking if the other one is at the station
or not, or we can use a single exit control for the Transporter combined with a waituntil-statement:
```
waituntil MU_place.occupied prio 1
MU_place.Cont.move(@)
```
By using the waituntil-statement, the
exit control makes sure that a MU is
available to be loaded. If no MU is available, the interpreter suspends the
Method until a MU arrives, and activates the Method as soon as the MU enters the location 
`MU_place`
.As the interpreter has to automatically break up the expression into components that it can observe:

You can use the basic operators (
`+`
, 
`–`
,

`*`
, 
`/`
), comparison operators (
`=`
,

`<=`
, 
`>=`
, 
`/=`
), logical operators
(
`AND`
, 
`OR`
, 
`NOT`
), and parentheses

```
()
```
. 

You cannot use Method calls, access to tables, and built-in methods with parameters. 

You can, but should not, use built-in methods that produce side effects, such as 
`stack.pop`
 because the condition may have to be analyzed frequently. 

Plant Simulation always evaluates logical operations from left to right. The evaluation terminates as soon as the value of the expression is certain.
Example

```
waituntil Station.Cont /= void AND Station.Cont.Finished
`As long as`
Station.Cont
`has the value`
void
```
, it is already clear
that the entire condition will be false, and therefore

`Station.Cont.Finished`
 will not be evaluated and thus does not lead to a runtime
error.
Note 
If you are watching a user-defined attribute of data type object, its value can
become 
`void`
 for two reasons:

A Method assigns the value 
`void`
 to the user-defined
attribute. Then the condition will be re-evaluated and the waituntil/stopuntil
statement might wake up. 
The object to which the user-defined attribute points is deleted. Then the condition
will not be re-evaluated and the waituntil/stopuntil statement will not wake up. 

See also

waituntil [SimTalk] and stopuntil [SimTalk]
Priority [method execution]
Waking up Methods
Simultaneously Waking up Several Methods
Create and Delete an Observer
Simultaneously Waking up Several Methods with waituntil
Simultaneously Waking up Several Methods with stopuntil
Maximum number of suspended methods [preferences]

---

#### Priority [method execution]
Plant Simulation may suspend several Methods based on identical or similar conditions. Consequently, a set of several Methods may be woken up at the same time. In this case the interpreter wakes up
the Method with the highest priority and continues executing it.After Plant Simulation finished executing this Method or if it comes across another waituntil statement with an unfulfilled condition during its
execution, the interpreter re-analyzes the conditions of the remaining Methods in the set. This yields a new subset of Methods to be woken
up. If any of the conditions are still true, the interpreter re-analyzes
the priorities and again selects the Method with the highest priority. For evaluating the priority you can use Methods, DataTables, or parameters. Avoid side effects, such as deleting MUs or changing a global variable, as the frequency and time of evaluation of the priority expression depend on
both the interpreter and the state of the model.Note 
One (1) is the lowest priority. The higher the values you specify, the higher the
priority, i.e., the sooner the Method will be reactivated. 

See also

waituntil [SimTalk] and stopuntil [SimTalk]
Condition [SimTalk]
Waking up Methods
Simultaneously Waking up Several Methods
Create and Delete an Observer
Simultaneously Waking up Several Methods with waituntil
Simultaneously Waking up Several Methods with stopuntil
Maximum number of suspended methods [preferences]

---

#### Interrupting Method Execution with Wait
   You can interrupt method execution with the keyword 
`wait`
 for the
      specified number of seconds.Syntax
`wait timespan:real`
The keyword wait interrupts
            the execution of a call chain for the number of seconds passed as the parameter of data
            type real. The simulation continues as if the call chain had
            been finished. Plant Simulation enters a MethWakeup event into the List of scheduled events in the EventController to continue executing the call chain after the time you
            specified has elapsed. Note 
This only works if your simulation model contains an EventController.
If a control is being executed during the reset phase and suspends itself with a wait instruction, Plant Simulation deletes the suspension at the end of the reset phase.You can also suspend a Method class, meaning a Method that is located in a folder in the Class Library, with a wait instruction if the Method class was called by a Method that is located in a model containing an EventController.Plant Simulation shows a Method that was interrupted with 
`wait`
 with a blue LED .3D shows the state as a colored rectangle at the top border of the icon.A Method that is suspended by a wait instruction shows this in the tooltip in the Frame window.
      Example
         
```
var MU: object
repeat
    if not Station.occupied 
       MU := .MUs.Container.create(Station)
    end
    wait 120
    if MU /= void
       mu.delete
    end
    wait 30
until false
```

---

#### Time Limitation for Waituntil and Stopuntil
    In SimTalk 2.0 you can specify a time limitation for
        waituntil and stopuntil statements. If the waituntil/stopuntil statement is
                suspended for this time duration it will be reactivated, although the condition has
                not yet been met. The keyword waitExpired is set to true once the instruction is reactivated caused by the time limitation. If the suspension terminates because of the condition on the other hand, waitExpired is set to false.
```
waituntil Station.Empty wait 60
   if waitExpired
       [Station]
   else
       @.delete
   end
```

        See also
            
            waituntil [SimTalk] and stopuntil [SimTalk]

---

#### Waking up Methods
    The value of a condition causing a Method to be suspended can
        change because of a simulation event (for example a MU exiting the
        station) or method processing (for example, assignment of a value). 
            If a Method is active, the interpreter
                interrupts the execution of the active Method and saves the
                entire call chain of the Method. 
            After that, the interpreter re-analyzes the conditions of the
                suspended Methods. The interpreter does not analyze
                conditions that do not depend on the change again. 
            If the condition is not true, it suspends
                the Methods immediately. 
            If the condition is true, the interpreter
                analyzes its priority and builds a priority list. It then selects the Method with the highest priority and resumes executing that
                    Method, meaning it reactivates it. Method execution
                continues until Plant Simulation executed the entire active
                call chain, if an error occurs during execution or if a Method encounters a waituntil-statement again,
                whose condition is not met and the Method is thus suspended
                again. 
        
        See also
            
            Simultaneously Waking up Several Methods
            Simultaneously Waking up Several Methods with waituntil
            Simultaneously Waking up Several Methods with stopuntil
            Priority [method execution]

---

#### Simultaneously Waking up Several Methods
    Plant Simulation reactivates the Method with the highest priority first if several Methods
        can be reactivated at the same time. 
            Waking up a Method  may affect the conditions of the
                remaining Methods. Thus, some of the initially true conditions may become false
                after the first Method is executed.
            For Methods that were suspended with waituntil, the interpreter analyzes the conditions again after the first
                reactivated Method is finished. Consequently, some Methods may
                remain suspended even though their condition was initially true. 
            For Methods that were suspended with stopuntil, the interpreter does
                not analyze the conditions a second time. The fact that a condition became true initially suffices for all remaining Methods to be reactivated. The interpreter reactivates the
                    Methods according to the priority you specified.
        
        See also
            
            Simultaneously Waking up Several Methods with waituntil
            Simultaneously Waking up Several Methods with stopuntil
            Priority [method execution]

---

#### Simultaneously Waking up Several Methods with waituntil
Use 
`waituntil`
 to simultaneously reactivate several Methods. 
Compare this example: 
Transporters are to drive from several objects to the
same Station. Remember that a Station can only
accept a MU, if it is Empty. 
The source code of the exit controls of the
predecessor objects looks like this:
```
waituntil Station.Empty prio @.Capacity
@.move(Station)
```

Suppose we have three suspended exit
controls. Once the Station is empty, the Transporter with the highest capacity drives to the Station, as it has the highest priority. After the Transporter drives to the Station, the condition 
`Station.Empty`
 is false. Thus, the remaining two
Transporters stay where they are at and wait until the Station is empty again.

See also

waituntil [SimTalk] and stopuntil [SimTalk]
Simultaneously Waking up Several Methods with stopuntil
Priority [method execution]

---

#### Simultaneously Waking up Several Methods with stopuntil
Use 
`stopuntil`
 to simultaneously reactivate several Methods. 
Compare this example: 
We model a Store using the Variable named GateOpen. MUs can only enter
the Store if 
`GateOpen`
 is true. After the MUs move through the gate at the
entrance of the Store, the condition 
`GateOpen`
 is false again. 
The source code of the exit control of the
predecessor objects like this:
```
stopuntil GateOpen prio 1
@.move(Store)
GateOpen := false
`If`
GateOpen
```
 is true,
the interpreter wakes up all suspended Methods, although 
`GateOpen`
 (and the suspension condition) is set to false after the first Method is called. 

See also

waituntil [SimTalk] and stopuntil [SimTalk]
Simultaneously Waking up Several Methods with waituntil
Priority [method execution] during method execution

---

#### Watchable Values
    Plant Simulation must be able to watch the conditions used in a waituntil-instruction or a stopuntil-instruction with an observer. A condition is
            watchable if all components of the boolean expression are watchable. 
            SimTalk only evaluates the condition anew if
                one of its watchable components changed during the simulation. Some examples of
                conditions that cannot be watched are the return values of user-defined methods and values that change continuously, such as the
                utilization of stations. 
            If the condition contains a component that Plant Simulation cannot watch,
                the Method Debugger will open and display the error message
                    Expression cannot be watched. 
            The column Watchable in the window Show Attributes and Methods shows all
                    attributes, methods, and read-only attributes that
                    Plant Simulation can watch.
            
        
        See also
            
            waituntil [SimTalk] and stopuntil [SimTalk]
            Edit Observers [general description]
            Create and Delete an Observer

---

### Exiting Methods with the Keyword return
   Terminates the currently executed Method and returns to the
      calling Method.
      Syntax
         
`return`

      The keyword return terminates the currently executed Method and returns to the calling Method.
```
if ParallelStation.failed   // cannot process?
   return                   // return immediately
else
   ...
end
```
You can terminate a Method that returns a result with
               
`return <expression>`
. This has the same effect
            as 
```
result := expression return
```
.
```
param n: integer -> integer // computes the factorial of n 
if n = 0 
   return 1
end
return n * self.execute(n-1)
```

      See also
         
         return [SimTalk]
         result [SimTalk]

---

### Error Handling
Error handling, also known as exception handling in software development, enables you to react to
runtime errors which occur within Methods while the source code is being
executed. 
Error handling makes, for example, sense, if
the simulation has to continue under all circumstances and To record the errors, which occur, or if
you want to take appropriate measures, if errors, which you expect to occur, do in fact occur.To implement error handling, proceed as follows: 

For an object of type Method: 
Create a user-defined attribute of data type method or object and name it 
`ErrorHandler`
. You have to create this attribute either in the Method itself or in the Frame into which you inserted the Method.

For a user-defined attribute of data type method: 
Create another user-defined attribute in the object which has the user-defined attribute(s). Assign the data type method or object this attribute and name it 
`ErrorHandler`
.

The source code of the ErrorHandler could, for example, look like this:
```
param byref error: string,
      method_path: string,
      line_number: integer -> any 
if error = "Division by zero." 
   error := ""  // catch this error
   return 1e300 // return a value to the calling method
end
// route error message to the calling method 
error := "error in " + method_path + ": " + error
```
When a runtime error occurs in a Method, Plant Simulation cancels executing that Method and calls the error handling method, the ErrorHandler, of the Method. If the Method does not have an ErrorHandler, Plant Simulation searches for an ErrorHandler within the call chain. If none of the Methods within the call chain have an ErrorHandler, Plant Simulation uses the standard error handling procedure, meaning that it opens the Method Debugger.
Parameters

Pass three parameters to the ErrorHandler: 

The error message.

The path of the faulty Method. 

The number of the line of code in which the error occurred. 

If you assign an empty string 
`""`
 to the error message variable, Plant
Simulation assumes that you successfully took care of the error. Plant Simulation will
not continue executing the faulty Method. Instead, Plant Simulation jumps back to
that Method, that called the Method, which has the ErrorHandler. 
If the Method, which has the ErrorHandler, returns a value, the
ErrorHandler should also do so.
If you cannot react appropriately to the error because, for example, an error
occurred, which you did not expect, you should not delete the error message. You can change it at
will though. If you do not delete the error message, Plant Simulation
assumes that you did not take care of the error, and passes the error message to the calling Method. If the call chain contains another Method with
an ErrorHandler, Plant Simulation calls this ErrorHandler with the changed error message. Otherwise, Plant Simulation uses the standard error handling procedure with the changed error message,
meaning that it opens the Method Debugger.
Note 
If another runtime error occurs during error handling, Plant Simulation does not
re-execute the error handling Method.

Compare the example model in the Examples Collection.

See also

setErrorHandler [SimTalk]
getCallStack [SimTalk]
throwRuntimeError [SimTalk]
Calculate Values with a Formula

---
