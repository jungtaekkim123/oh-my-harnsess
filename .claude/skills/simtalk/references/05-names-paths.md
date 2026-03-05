> **Read this when:** Object paths, relative/absolute references, namespaces, qualified names, `basis` keyword  
> **Skip this when:** Identifier naming rules (see 04) or variable types (see 07-10)


## Contents

  - [Anonymous Identifiers](#anonymous-identifiers)
  - [@ - anonymous identifier](#--anonymous-identifier)
  - [? - anonymous identifier](#--anonymous-identifier)
  - [basis - anonymous identifier](#basis---anonymous-identifier)
  - [current - anonymous identifier](#current---anonymous-identifier)
  - [root - anonymous identifier](#root---anonymous-identifier)
  - [rootfolder - anonymous identifier](#rootfolder---anonymous-identifier)
  - [self - anonymous identifier](#self---anonymous-identifier)
  - [Object Paths in SimTalk](#object-paths-in-simtalk)
  - [The Absolute Path](#the-absolute-path)
  - [The Relative Path](#the-relative-path)
  - [Object Reference](#object-reference)
- [Namespace](#namespace)

### Anonymous Identifiers
 Anonymous identifiers make using a Method more flexible and
  independent of its context. Anonymous identifiers are, for example @, basis, current, ?, root, RootFolder, and self
   
   You can insert an anonymous identifier into different models without having to
    modify the source code of the Method that contains it.Normally, the name of a control you programmed in a Method does not change in your model. The path to the Method changes from model to model, though. If a control requires the current path, you can query it by using anonymous identifiers. 
  See also
   
   Location [SimTalk] - material flow objects [SimTalk]

---

### @ - anonymous identifier
    The anonymous identifier @ (at sign) designates
        the MU that triggered the respective control. Remarks
            If you specify an entrance control or an
                    exit control in a material flow object,
                the anonymous identifier @ enables you to
                access the MU that entered the object or is ready to exit
                the object.The assignment is unique even if several control methods are triggered at the same simulation time, as Plant Simulation always processes the triggering MU completely before proceeding to the next MU. 
        Example
            
```
@.move(ParallelStation.succ(3))
```

---

### ? - anonymous identifier
                The anonymous identifier ?
                                (question mark) designates the material flow object or the control
                                                (Method) that called the Method. Remarks
                                                The anonymous identifier ? enables a control
                                                  to be used without modifications by several
                                                  objects.
                                Example
                                                
```
?.Cont.move(E2) // moves the contents of the object that 
                // called the method to the object E2
```

---

### basis - anonymous identifier
The anonymous identifier basis designates the
class library. Remarks
You can only use basis in comparisons, i.e.,
with = or /=.
Example

```
if location = basis 
// in the class library
else
// inserted into a Frame 
end
```

See also

Class Library
Relational Operators

---

### current - anonymous identifier
   The anonymous identifier current returns the Frame within which the Method object is
      located. Remarks
         This way you can easily enter the location of a Frame into lists and tables or enter it as a parameter to methods in other Frames. You can also use current to distinguish between a local and a global variable with the same name. The parameter name identifies a local
            variable, while current.name designates the
            global variable.
      Example
         
```
print "Current pause ", current.pause
MyStation.pause := current.pause
var shift := root.ShiftCalendar.GetCurrShift
print "Current shift: ", shift
   
if not current.unplanned 
       
if current.pause
   current.currIcon := "pause"
else
   current.currIcon := "working"
end
```

---

### root - anonymous identifier
The anonymous identifier root designates the
topmost Frame in the hierarchy of Frames. Remarks
From the topmost Frame on you can then navigate downward through the
hierarchy of Frames in your model. 
The identifier root is especially helpful if
you do not know the name of the root Frame, i.e., the Frame that is located at the top of the hierarchy. 
Example

```
Method1                  // same namespace
root.Frame2.Method1      // path and name
&Method1.executeIn(8.5)  // pass to EventController
Variable.execute         // call the referenced Method, note that the
                         // object Variable has the data type object
```

---

### rootfolder - anonymous identifier
  The anonymous identifier rootfolder designates
    the folder in the Class Library in which you store Methods which a number of objects use. 
    Remarks
      
      Using the root folder prevents wasting main memory and prevents long paths
        as Plant Simulation then calls this method once only from the Class Library instead of a large number of instances of this method
        located in different folders. 
      If you use the anonymous identifier 
`rootfolder`
 in a Method, the rootfolder designates a folder in the Class Library
        for which you have set the attribute RootFolder
        . In this case Plant
          Simulation searches for such a folder, starting with the class of the Method, upward in the hierarchy of objects. 
      You can also use the anonymous identifier rootfolder within
          control methods. Here Plant Simulation looks for the folder for which
        you set the attribute RootFolder to 
`true`
, starting with the class
        of the Frame into which you inserted the object in which you programmed the
        control.
    
    Example
      
```
.UserObjects.rootfolder := true
```

    
    See also
      
      RootFolder [SimTalk] - attribute
      Set the Root Folder for Your Simulation Model

---

### self - anonymous identifier
The anonymous identifier self designates the
currently executed Method. Remarks
Use self if it is likely that methods are renamed later on. Otherwise you may have to change each instance of the previous name to the new name.
```
self.executeIn(60)
self      // returns the path to and the name of the Method
self.Name // returns the name of the Method only
```
In a user-defined attribute of data type method the identifier self is the user-defined method attribute itself. Use self.~ to access the object for which you created the user-defined attribute.
Return Value

The return value has the data type object. 

Example

```
self.~.pause := true  // pauses the object for which you defined 
                      // the user-defined attribute
```

---

### Object Paths in SimTalk
If different objects are not located within the same Frame, i.e.,
within the same namespace, you have to add their path to the objects to uniquely identify them. Only
then you can access them in a Method. 
An object path consists of a sequence of names separated by a period:
```
[.]name[.name.name[...]]
```

Note 
Brackets designate optional components or parameters, meaning that you can, but
do not have to specify them.

The syntax diagram of a path looks like this:

The Syntax of the individual methods might look like this:
```
<Path>.openDialog([CallOpenControl:boolean:=false]) → boolean
```

The expression <Path> designates the path of the object to which the
method applies. 

The signature of the method, consisting of the identifier and the data type of the parameter, is
listed in parentheses. The expression (Parameter:string), for example, designates a
parameter of data type string. Instead of a constant value, you can also use a variable of
the required type or a method that returns the required data type. 
Note 
Make sure to enter the parentheses for expressions within parentheses (…). Not
entering them may lead to unexpected results and open the Debugger.

Optional parameters are listed within brackets. The expression [, Parameter:boolean], for example, means that you can, but do not have to enter
the boolean parameter. 
If a parameter has a default value, the signature shows the default value after the parameter
If the method has a return value, the signature shows its data type after the arrow
→.

Plant Simulation distinguishes between two kinds of paths. 

The absolute path starts with a period—standing for the Class
Library—followed by the name of the folder and top-level Frame. Then a period
and a name alternate until you reach the desired object, which again is preceded by a period. 
An absolute path might look like this:

`.Models.MyPlant.Engine_Assembly_Anytown.MyStation`

The relative path starts in the current namespace and identifies an object
by a combination of built-in methods and names. 
In most cases the relative path starts with a Frame. 
A relative path might look like this:

`MyPlant.Engine_Assembly_Anytown.MyStation`

In addition, you can access a variable of data type Object using an object
reference.

See also

The Absolute Path
The Relative Path
Object Reference
Change Values by Assigning a Value in SimTalk
Class Library
Object [SimTalk]

---

### The Absolute Path
    The absolute path starts with a period—standing for the
            Class Library—followed by the name of the folder
        and top-level Frame. Then a period and a name alternate until you
        reach the desired object, which again is preceded by a period.Remarks
            
            In the example below the absolute path of the Station named
                    MyStation looks like this:
`.Models.MyPlant.EngineAssemblyMyTown.MyStation`

            The structure of the model looks like this:
            
            
            You might, for example, use the absolute
                    path for a control method. This method might
                always execute certain actions before starting a simulation run, which never change.
                Then it makes sense to add this method to the Class Library
                and reference it using its absolute path that never changes.
            You have to use the absolute path for MUs when you model a complex station, for example a
                receiving station of a plant with one or more Sources.
            If, on the other hand, you want to use the same method, but with different source
                code, in instantiated Frames, you will use the relative
                    path, to make sure that each Frame finds the method where
                you programmed actions specific to this Frame. 
            To insert the absolute path of the object
                into a text box with drag-and-drop, hold down the Shift and Ctrl keys.
        
        See also
            
            Class Library
            The Relative Path
            Object Reference
            Change Values by Assigning a Value in SimTalk

---

### The Relative Path
The relative path starts in the current namespace—formed by all
objects located within a single Frame—or the Frame
in which the Method object is located. Remarks

The relative path starts with an anonymous identifier, a name in the current namespace,
or a built-in method. Then a period follows and the name of a Frame or a period and a
built-in method. The last entry is a period and the name of the object or a period and a built-in
method or a period and an attribute. 
In the example below the relative path of the Station which we inserted into a
Frame named MyPlant looks like this:
`MyPlant.EngineAssemblyMyTown.MyStation`

The structure of the model looks like this:

This table lists where the relative path starts for the different objects:
| Object | Relative path starts in || Built-in or user-defined attribute of data type object in a material flow
object | the Frame which contains the material flow object. || Built-in or user-defined attribute of data type object in a MU | the parent Frame of the material flow object which contains the MU. || Built-in or user-defined attribute of data type object in a Frame | the Frame itself. || Source code of a Method or of a user-defined attribute of data type
method | the Frame which contains the Method or the object which has the attribute. || DataTable or user-defined attribute of data type table, with columns
of data type object | the Frame which contains the DataTable or in the parent object which has the
attribute. || User-defined attribute of data type table of a MU, with columns of data type object | the Frame in which the MU is located. || WorkerPool | the Frame in which the Worker is located. |
Suppose that you want to access the object named Station1 in a Method, which
you inserted into a Frame. Station1 is located in a sub-Frame named
Frame1. The relative path then looks like this: 
`Frame1.Station1`
. 
Suppose that you are located in a Method, which is located in a sub-Frame of
Frame2. Then you would like to access an object named Station2 that is located in
Frame2. Here the relative path looks like this: 
`Location.Station2`

or 
`~.Station2`
. The tilde ~ in the second case is an abbreviation of the built-in
attribute Location.
You can change the starting position of the relative
path with the keywords root, self, and RootFolder.
When dragging and dropping an object onto a text box, Plant
Simulation inserts the relative path by default.

See also

The Absolute Path
Object Reference
Change Values by Assigning a Value in SimTalk > Paths in SimTalk Instructions
root [SimTalk] - anonymous identifier
self [SimTalk] - anonymous identifier
rootfolder [SimTalk] - anonymous identifier
Location [SimTalk] - material flow objects

---

### Object Reference
A variable of data type object can accept a relative or an absolute path as well as an object reference. This also applies to global variables, local variables, formal
parameters, and values in tables which have the data type object. An
object reference always references a single
object.Remarks

Plant Simulation even points to the object when you rename it. If you
delete the object, Plant Simulation cannot resolve the object reference
anymore and does not find the object, even if you insert an object with the same name as the deleted
object.
In the example below the object reference to a Station in the Variable looks
like this:
`*.Models.Model.Station`

The asterisk * in front of the path denotes the object reference as
such.

Note 
We advise caution when using an object
reference. 
As a rule you can always use an object
reference instead of an absolute path. If you
need a relative addressing, use a relative path instead.
The main advantages of an object reference
as compared to a path are a higher access speed and its tolerance toward renaming objects.

See also

Object [SimTalk]
The Absolute Path
The Relative Path
Change Values by Assigning a Value in SimTalk > Paths in SimTalk Instructions

---

## Namespace
                names of the built-in attributes and methods and the names of the user-defined
                    attributes of the Frame, form a namespace. All objects, which you inserted into a folder, plus the names of the built-in attributes and methods of the folder, also form a namespace.The same applies for objects which provide built-in
                attributes and methods and for which you created user-defined attributes of
                the object.Within this namespace, you cannot use the same name more than once, i.e., each name has to be unique! You can use identical names in different name-spaces though, as then Plant Simulation differentiates them using their paths.
        See also
            
            Name [general description]
            isNameUnique [SimTalk] - identifier
