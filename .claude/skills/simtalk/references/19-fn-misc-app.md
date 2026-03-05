> **Read this when:** Application info: `applicationHome`, `applicationVersion`, licensing, environment, language settings  
> **Skip this when:** Model file operations (see 20) or simulation control (see 21)


## Contents

- [applicationHome](#applicationhome)
- [applicationVersion](#applicationversion)
- [checkForLicense](#checkforlicense)
- [createLicenseFile](#createlicensefile)
- [enableFullScreenMode](#enablefullscreenmode)
- [exitApplication](#exitapplication)
- [getCommandLineArg](#getcommandlinearg)
- [getEpsilon](#getepsilon)
- [getHighResolutionClock](#gethighresolutionclock)
- [hideBBL](#hidebbl)
- [isComputerAccessPermitted](#iscomputeraccesspermitted)
- [keepWindowsAlwaysOnTop](#keepwindowsalwaysontop)
- [language](#language)
- [licenseName](#licensename)
- [numOfLimitedObjects](#numoflimitedobjects)
- [setEpsilon](#setepsilon)
- [setPythonDLLPath](#setpythondllpath)
- [userInterfaceLanguage](#userinterfacelanguage)

## applicationHome
    Returns the folder in which Plant Simulation is
        installed.
        
        Syntax
            
```
applicationHome → string
```

        
        Return Value
            
            The return value has the data type string.
        
        Example
            
```
print applicationHome // might return C:\Program Files\Siemens\Plant Simulation 2404\
```

        
        See also
            
            Installing Plant Simulation

---

## applicationVersion
Returns the coded version number of Plant Simulation. 

Syntax

```
applicationVersion -> integer
```

Return Value

The return value of data type integer is composed as follows: VVMMMPPP

VV is the major version number.

MMM is the minor version number.

PPP is the number of the patch level.

Example

```
print applicationVersion // might return 15002002, i.e. version 15.2.2
print applicationVersion // might return 16001003, i.e. version 16.1.3
print applicationVersion // might return 22001006, i.e. version 2201.0006
print applicationVersion // might return 23002008, i.e. version 2302.0008
print applicationVersion // might return 24004000, i.e. version 2404.0000
```

See also

About Plant Simulation

---

## checkForLicense
Checks if a user-defined license is available or not.

Syntax

```
checkForLicense(Feature:string, Version:string, PasswordHash:string) → integer
```

Parameters

The parameter Feature of data type string designates the name of the license
feature.

The parameter Version of data type string designates the requested version
number of the license.

The parameter PasswordHash of data type string designates the SHA-1-Hash of the
password of the license.

Return Value

The return value has the data type integer.
The individual values have this meaning:

0: The license feature is registered and valid.

1: The license feature is not registered.

2: The file has an invalid registry data format.

3: The SHA-1-Hash is wrong.

4: The Host-ID is wrong.

5: The registered version of the feature is too old.

6: The license has expired.

7: The feature does not permit the use with the license type of Plant Simulation
(Professional / Standard / Runtime /...).

Example

```
if checkForLicense("MyFeature", "1", "686483805ac47ca14e03514f7481a7973b401762") = 0 
// The license is available, you can proceed ...
else
closeModel
messageBox("The license 'MyFeature' is unavailable. The model was closed.\n", 1, 1)
end
```

See also

createLicenseFile [SimTalk]
setRequiredLicense [SimTalk]

---

## createLicenseFile
Generates a user-defined license and writes it to a Windows
Registry file. 
Remarks

You can then send this file to another person to enter the user-defined license
into the Registry on the target computer.
You can use the method setRequiredLicense to make a library folder
request this license. A simulation model/an object containing such a folder can only be loaded if
the license is entered into the Registry and is valid. If you want to always
permit loading the model or the object, but only want to permit certain actions when a license is
available, you can also request the user-defined license in a method by calling the global function
checkForLicense.
If you deactivate the safety setting File > Model
Settings > General > Prohibit access to the computer, the function createLicenseFile can copy data from another folder and write it to the model
folder or its sub-folders. The function cannot copy files from the model folder or its sub-folders. 

Syntax

```
createLicenseFile(Feature:string, Version:string, HostID:string, ExpirationDate:string/date, Password:string, FileName:string[, Restriction:string]) → string
```

Parameters

The parameter Feature of data type string designates the name of the license
feature. The name cannot contain blank spaces.

The parameter Version of data type string designates the version number of the license. The registered version has to be greater
than or equal to the requested license. The version number cannot contain blank spaces.
If, for example, version 10 of the feature is registered, you can request version 9.5.0 but not
vice versa.

The parameter HostID of data type string designates the Host ID of the computer for which the license is valid. If you type in
an empty string 
`""`
 or 
`"any"`
, the
license if valid on all computers. You can query the valid Host IDs of a computer by starting Plant Simulation on the target computer and click Query Host ID under File > Preferences >
License.
Note 
Always use the adapter of the physical LAN port for the Host ID.

Instead of a Host ID you can also type in
a Sold To ID. This way the license is not bound to a certain
computer but to the Plant Simulation license of a customer. This means that
the license is valid on each computer that requests a Plant Simulation
license whose license file has this Sold To ID hat. To query
the Sold To ID by starting Plant
Simulation on the target computer and selecting File > Help >
About Plant Simulation. The Host ID may not
contain any blank spaces.

The parameter ExpirationDate of data type string/date designates the expiration date until which
the license is valid. If you type in an empty string 
`""`
 or 
`"permanent"`
, the license has no expiration date. The date cannot contain
blank spaces.

The parameter Password of data type string designates the secret password.

The parameter FileName of data type string designates the file name or the file
<Path>. The function writes the Registry data
for the generated license to this file. The file should have the file extension .reg so that the
license can be entered into the Registry on the target computer by double-clicking it.

The optional parameter Restriction of data type string designates the restriction you want to apply to the license. You can
only type in
`"Application"`
, 
`"Runtime"`
, 
`"Simulation"`
, or 
`"Viewer"`
. The license will then only be available if the license type of Plant Simulation matches the specified type or a type of lower value. This
means that if you restrict the license to 
`"Application"`
, the
license is also available in a Runtime license and a
Simulations license of Plant
Simulation. User-defined licenses are always available in a Viewer license.

Return Value

The return value has the data type string.
It is the SHA-1-Hash for the password. When you call the function checkForLicense, you have to type in this hash. If the hash does not match the
hash of the password, the license is considered invalid. We recommend to call the function checkForLicense within an encrypted method so that the function call cannot be
removed.
It is practically impossible to extract the password from the hash. If you
inadvertently give the unencrypted Method to somebody else, your password
will still be unknown. This is important in case you also used the password somewhere else. As you
have to type in the password when generating a license with the function checkForLicense no license can be generated using the hash value either.

Example

```
PasswordHash := createLicenseFile("MyLicenseName", "1.0", "COMPOSITE=0ADF1C780F29", "", "abc", "C:\TEMP\license.reg")
```

See also

Prohibit access to the computer [model settings]
Host IDs
About Plant Simulation
checkForLicense [SimTalk]
setRequiredLicense [SimTalk]

---

## enableFullScreenMode
    Activates (
`true`
) or deactivates (
`false`
) full screen
        mode. 
        
        Syntax
            
```
enableFullScreenMode(Activate:boolean)
```

        
        Parameter
            
            The parameter Activate of data type boolean activates
                    (
`true`
) or deactivates (
`false`
) full screen
                mode.
        
        Example
            
```
enableFullScreenMode(true)
```

        
        See also
            
            Full Screen [Window ribbon]

---

## exitApplication
   Terminates the simulation run and exits Plant
      Simulation.
      Remarks
         
         Note 
            Plant Simulation does not save model data before exiting. Changes to the
               model or to the simulation data are lost if you do not save the model before, compare
               the function saveModel. Plant Simulation does
                  not issue a warning or prompt asking you if
               you really want to exit.
         
         Note 
            You can also define a Method with the name
                  onCloseModel in any folder in the Class Library, including the Basis
               folder. This Method is being executed when you close the
               model or when you exit Plant Simulation. You can, for
               example, program clean-up tasks, delete temporary files, etc. 
            The method onCloseModel has to declare the
               boolean parameter 
`onExitApplication`
. Plant Simulation sets this parameter to 
`false`
 when onCloseModel is
               called when you close the model. Plant Simulation sets this
               parameter to 
`true`
 when onCloseModel is called when you exit Plant
                  Simulation. 
            You can also program several onCloseModel
               methods and place them into different folders. Plant
                  Simulation then calls all existing onCloseModel
               method classes in the Class Library when you close the model
               or exit the application.
         
      
      
      Syntax
         
`exitApplication`

      
      Example
         
```
if EventController.time > 36000 
   saveModel("Variation_IIV")
   exitApplication
end
```

      
      See also
         
         Exit Application
         saveModel [SimTalk]

---

## getCommandLineArg
   Queries if a command-line argument has been passed to Plant
         Simulation when starting it. 
      
      Syntax
         
```
getCommandLineArg(CommandLineArgument:string, byref Value:string) → boolean
```

      
      Parameters
         
         
            
               The parameter CommandLineArgument designates the command-line argument
                  that has been passed to Plant Simulation when starting it.
            
            
               If the parameter CommandLineArgument expects a value, you
                  can query this value with the parameter Value. 
               The local variable Value is always
                  assigned the value of the next specified command-line argument, compare this
                  example.
```
/NoMessageBox /TrustModels /TestCode true
getCommandLineArg("NoMessageBox", Value) -> Value = '/TrustModels'
getCommandLineArg("TrustModels", Value)  -> Value = '/ TestCode'
getCommandLineArg("TestCode", Value)     -> Value = 'true'
```

               Note 
                  If the parameter CommandLineArgument does not expect a
                     value, do not specify the parameter Value or ignore it.
               
            
         
      
      Return Value
         
         The return value has the data type boolean. 
         true if Plant Simulation was started with the
            specified command-line argument.
         false if it was not started with the specified command-line argument. 
      
      Example
         
```
// Suppose we started Plant Simulation with these command-line arguments:
// PlantSimulation2404.exe /L Runtime /abc 42 /xyz /myfile "C:\Program Files\a.txt"
var arg: string
if getCommandLineArg("abc", arg) 
   print arg // outputs 42
end
if getCommandLineArg("myfile", arg) 
   print arg // outputs C:\Program Files\a.txt
end
if getCommandLineArg("xyz", arg) 
   print arg // outputs an empty string
end
```

      
      See also
         
         Specifying Start Options

---

## getEpsilon
    Returns the value you set for which Plant Simulation
        considers numerical values to be about equal. 
        
        Syntax
            
```
getEpsilon → real
```

        
        Return Value
            
            The return value has the data type real.
        
        Example
            
```
print getEpsilon // might output 7e-08
```

        
        See also
            
            Tolerance for about equal (~=) comparison [model settings]
            setEpsilon [SimTalk]

---

## getHighResolutionClock
Returns the number of seconds that passed since opening the model.
Remarks

You can use the function to measure extremely short time spans, for example the
time which a SimTalk instruction requires.

Syntax

```
getHighResolutionClock → real
```

Return Value

The return value has the data type real.

Example

```
var t1, t2: real
t1 := getHighResolutionClock
var x := sin(t1)
t2 := getHighResolutionClock
print "elapsed time: ", (t2-t1)*1000, " milliseconds"
```

See also

processTime [SimTalk]
sysDate [SimTalk]

---

## hideBBL
Minimizes Plant Simulation to an icon in the status area of the
taskbar.

Syntax

```
hideBBL(MinimizeWindow:boolean[, HideWindow:boolean]) → boolean
```

Parameters

Setting the parameter MinimizeWindow of data type boolean to

`true`
 minimizes Plant Simulation into the taskbar status area. The
application window can be restored by double-clicking the icon in the status area of the
taskbar.
Setting the parameter to 
`false`
 restores the application window (if it has been
minimized to the status area of the taskbar).
Note 
The parameter HideWindow of data type boolean is optional and only relevant,
when the parameter boolean has the value 
`true`
.

Setting the parameter HideWindow of data type boolean to 
`true`

hides the application window without showing an icon status area of the taskbar, so the user cannot
restore the application window.
Setting the parameter to 
`false`
 shows an icon in the status area of the taskbar,
when Plant Simulation is minimized in the status area of the taskbar. This is the
default.

Return Value

The return value has the data type boolean. 

Example

```
hideBBL(true) // hides the Plant Simulation window
```

See also

Specifying Start Options, 
`-hideBBL`

---

## isComputerAccessPermitted
Returns if access to the computer is permitted for the executed Method (true) or not (false). 
Remarks

Access can be denied for these two reasons:

Access is prohibited under Model Settings > General > Prohibit access
to the computer.

The executed Method belongs to a library and access is
prohibited for this library. You find this setting under Edit Library Information >
Prohibit access to the computer.

Syntax

```
isComputerAccessPermitted → boolean
```

Return Value

The return value has the data type boolean.

Example

```
print isComputerAccessPermitted
```

See also

Model Settings > Prohibit access to the computer [model settings]
Edit Library Information > Prohibit access to the computer

---

## keepWindowsAlwaysOnTop
    Sets if Plant Simulation windows will always appear on top of
        all open windows on the screen or not. 
        
        Syntax
            
```
keepWindowsAlwaysOnTop(WindowInForeground:boolean)
```

        
        Parameter
            
            The parameter WindowInForeground of data type boolean sets if
                    Plant Simulation windows will always appear on top of all open windows
                on the screen (
`true`
) or not (
`false`
).
        
        Example
            
```
keepWindowsAlwaysOnTop(true)
```

---

## language
  Returns the model language which you selected under File >
      Model Settings/Preferences > General > Model language. 
    Remarks
      
      Use language to show language-specific messages. 
    
    
    Syntax
      
```
language → integer
```

    
    Return Value
      
      The return value has the data type integer.
      The return value 
`0`
 designates German,
          
`1`
 designates English, 
`2`

        designates Japanese, 
`3`
 designates
          Chinese, and 
`8`
 designates
          Hungarian.
    
    Example
      
```
print language
```

    
    See also
      
      userInterfaceLanguage [SimTalk]
      Model language [preferences]

---

## licenseName
Returns the name of the active Plant Simulation license. 

Syntax

```
licenseName → string
```

Return Value

The return value has the data type string.
| This license | Returns this string || Application | emplant_app || Educational | emplant_edu || Professional | emplant_pro || Foundation | emplant_fnd || Research | emplant_res || Runtime | emplant_run || Simulation | emplant_sim || Standard | emplant_std || Student | emplant_student || Viewer | emplant_view |

Example

```
print licenseName
```

See also

Starting Plant Simulation with Different Kinds of Licenses
Features of the Individual Licenses

---

## numOfLimitedObjects
  Counts all the built-in objects which are contained in the entire model. 
    Remarks
      
      numOfLimitedObject does not count Lists and
          Tables, Methods, Variables, Comments, MUs, Connectors, Interfaces, EventControllers, the  Toolbar, Folders, and Class objects.
      You might want to know this number if you are working with a Plant Simulation
        Standard License which is limited to 4000 objects.
      For licenses, which limit the number of objects you can use, the root object
        Basis in the Class Library
        shows how many objects are used and how many are allowed for the license you are using at
        the moment. 
      For the Student license it might
        look like this. Our simulation model contains our Frame named
          Model and 10 objects which we inserted into it. 80
        is the maximum number of objects which are allowed in the Student
          license.
      
    
    
    Syntax
      
```
numOfLimitedObjects → integer
```

    
    Return Value
      
      The return value has the data type integer.
    
    Example
      
```
print numOfLimitedObjects // returns 10 for the above model
```

    
    See also
      
      Console
      Console filter
      Starting Plant Simulation with Different Kinds of Licenses
      NumberOfLimitedObjects [SimTalk] of the Frame

---

## setEpsilon
   Sets the value for which Plant Simulation considers numerical
      values to be about equal.
      
      Syntax
         
```
setEpsilon(Value:real) → real
```

      
      Parameter
         
         The parameter Value of data type real designates the value.
         Note 
            Use the about equal comparison to prevent rounding errors when using
                  real values. 
            Specify 
```
print (1/3+1000-1000)*3
```
 and
               see which number your computer returns.
         
      
      Return Value
         
         The return value has the data type real.
      
      Example
         
```
setEpsilon(0.0001)
var a : real := 1.0003
var b : real := 1.00003
if a ~= 1.0  // this condition is false
   print "a is about equal to 1"
end
if b ~= 1.0  // this condition is true
   print "b is about equal to 1"
end
```

      
      See also
         
         Tolerance for about equal (~=) comparison [model settings]
         getEpsilon [SimTalk]

---

## setPythonDLLPath
Specifies the path to the Python installation to be use if you are have multiple Python
environments on your computer.
Remarks

Plant Simulation supports Python versions 3.12 and
3.13.
If you installed several Python versions on your computer, use setPythonLLPath to choose which version you want to use.

Syntax

```
setPythonDLLPath(dllpath:string)
```

Parameter

The parameter dllPath of data type string designates the path to the Python dll
that you want to use.

Example

```
setPythonDLLPath("C:\Program Files\Python312\python312.dll")
-- uses the Python version for all users, located in C:\Program Files\Python312, which is the default setting
```

```
setPythonDLLPath("C:\Users\<YourLoginName>\AppData\Local\Programs\Python\Python312\python312.dll")
-- uses the Python version for the current user located in the folder above
```

See also

PythonModule

---

## userInterfaceLanguage
   Returns the language of the user interface of Plant
      Simulation. 
      
      Syntax
         
```
userInterfaceLanguage → integer
```

      
      Return Value
         
         The return value has the data type integer.
         0 designates German, 1 English, 2
               Japanese, 3 Chinese, and 8 designates
               Hungarian
      
      Example
         
```
if userInterfaceLanguage = 0      // German
   print "Guten Morgen"
elseif userInterfaceLanguage = 1  // English
   print "Good morning"
elseif userInterfaceLanguage = 2  // Japanese
   print "Ohayo gozaimasu"
elseif userInterfaceLanguage = 3  // Chinese
   print "Zao an"
elseif userInterfaceLanguage = 8  // Hungarian
   print "Jó reggelt"
end
```

      
      See also
         
         language [SimTalk]
         Model language [model settings]
         Specifying Start Options, 
`/UILanguage:ENU`
, 
`/UILanguage:DEU`
, 
`/UILanguage:JPN`
, 
`/UILanguage:CHS`
, or 
`/UILanguage:HUN`
