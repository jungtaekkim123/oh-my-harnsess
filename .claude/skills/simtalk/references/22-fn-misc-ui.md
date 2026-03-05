> **Read this when:** UI/dialogs: `clearConsole`, `openConsole`, `messageBox`, color/date/object select boxes, HTML windows  
> **Skip this when:** Simulation control (see 21) or utility functions (see 23)


## Contents

- [clearConsole](#clearconsole)
- [clearLogFile](#clearlogfile)
- [closeAllWindows](#closeallwindows)
- [closeConsole](#closeconsole)
- [closeHTMLWindow](#closehtmlwindow)
- [getLogFile](#getlogfile)
- [getStandardColor](#getstandardcolor)
- [messageBox](#messagebox)
- [openColorSelectBox](#opencolorselectbox)
- [openConsole](#openconsole)
- [openDateSelectBox](#opendateselectbox)
- [openHTMLBrowser](#openhtmlbrowser)
- [openHTMLWindow](#openhtmlwindow)
- [openObjectSelectBox](#openobjectselectbox)
- [setConsoleFilter](#setconsolefilter)
- [updateGUI](#updategui)

## clearConsole
    Deletes the contents of the Console window.Remarks
            
            The screenshot shows which data will be deleted.
            
        
        
        Syntax
            
`clearConsole`

        
        Example
            
`clearConsole`

        
        See also
            
            Console
            closeConsole [SimTalk]
            openConsole [SimTalk]
            setConsoleFilter [SimTalk]
            print [SimTalk] - output function
            Specifying Start Options

---

## clearLogFile
    Deletes the contents of the log file into which Plant
            Simulation wrote all messages which were output to the Console
            window. 
        Remarks
            
            clearLogFile does not delete the log file itself.
        
        
        Syntax
            
```
clearLogFile → boolean
```

        
        Return Value
            
            The return value has the data type boolean. 
        
        Example
            
`clearLogFile`

        
        See also
            
            Console
            getLogFile [SimTalk]
            Specifying Start Options

---

## closeAllWindows
Closes all open object windows, even those that are minimized, including 3D windows. 
Remarks

Note 
The optional boolean parameter has no effect.

Syntax

```
closeAllWindows([UnusedParameter:boolean])
```

Example

`closeAllWindows`

See also

List of Open Windows

---

## closeConsole
Closes the open Console window. 
Remarks

All messages that were output to the Console will be lost. 

Note 
The optional boolean parameter has no effect.

Syntax

```
closeConsole[UnusedParameter:boolean] → boolean
```

Return Value

The return value has the data type boolean.

Example

`closeConsole`

See also

Console
clearConsole [SimTalk]
openConsole [SimTalk]
setConsoleFilter [SimTalk]
Specifying Start Options

---

## closeHTMLWindow
    Closes the browser window which you previously opened using the title of the window. 
        
        Syntax
            
```
closeHTMLWindow(CloseHTMLWindow:string) → boolean
```

        
        Parameter
            
            The parameter CloseHTMLWindow of data type string designates the
                title of the window you want to close. 
        
        Return Value
            
            The return value has the data type boolean.
        
        Example
            
```
closeHTMLWindow("Siemens Corporate Site")
closeHTMLWindow("Image of the ParallelStation")
```

        
        See also
            
            openHTMLWindow [SimTalk]

---

## getLogFile
    Gets the log file into which Plant Simulation wrote all
        messages which were output to the Console.
        
        Syntax
            
```
getLogFile → string
```

        
        Return Value
            
            The return value has the data type string. 
        
        Example
            
`getLogFile`

        
        See also
            
            clearLogFile [SimTalk]
            Specifying Start Options

---

## getStandardColor
Returns the specified color value from a standard color palette.
Remarks

You can, for example, use getStandardColor in the
entrance control of the Source to
assign different colors to the produced MUs.

Syntax

```
getStandardColor(Index:integer) -> integer
```

Parameter

The parameter Index of data type integer specifies one of 30 color values of a
standard color palette.

Return Value

The return value has the data type integer. 
Example
```
-- Entrance control of a Source object
@._3D.activateMaterialWithColor(getStandardColor(z_uniform(1,30))
-- Assigns a random color to the created part
```

See also

_3D.activateMaterialWithColor [SimTalk]

---

## messageBox
Shows a message box provided by the operating system. 
Remarks

Instead of directly typing the text and the numbers into the source code of the
method, you can also press Ctrl and the spacebar to open the
dialog MessageBox Settings. Then, type in the message text,
select the button combinations, and the symbol, and click OK.
|  |  |
In the screenshot below Plant Simulation shows the
string My message text, my text … , which we entered. The
number 
`50`
 designates the button combination Yes No Cancel, and the number 
`3`
 shows
the yellow triangle with the exclamation mark.

Syntax

```
messageBox([Text:string[, Buttons:integer[, Icons:integer]]) → integer
```

Parameters

The optional parameter Text of data type string designates the text, which you
are going to show. 
Type in the text, which you want to show in the title bar of the dialog, between two vertical
bars, for example 
```
messageBox("|My Company|This is a message.")
```
.

To insert a line break into your text, type in 
```
strChr(10)
```
, for example

```
messageBox("My message text," + strChr(10) + "my text, ...")
```
.

The optional parameter Buttons of data type real designates these buttons: 

`1`
 the OK button

`3`
 the button combination OK, Cancel

`10`
 the button combination Repeat, Retry, Cancel

`48`
 the button combination Yes, No

`50`
 the button combination Yes, No, Cancel

`76`
 the button combination Abort, Retry, Ignore

If you do not enter a value for the parameter Buttons, the message box only shows the
OK button.

The optional parameter Icons of data type real designates these icons: 

`0`
 no icon

`1`
 an error

`2`
 the question mark

`3`
 the exclamation mark

`4`
 Info

If you do not enter a value for the parameter Icons, the message box shows the
exclamation mark.
Plant Simulation recognizes parameters, which you already defined, and offers this
selection in the dialog MessageBox Parameters. When you change any of the
parameters here, Plant Simulation transfers your changed settings to the source code of the
Method and applies them.

Return Value

The return value has the data type integer. 
The return value tells you which button/button combinations the user clicked.

| Return Value | stands for || 1 | OK || 2 | Cancel || 4 | Ignore || 4 | Continue || 8 | Retry || 8 | Try Again || 16 | Yes || 32 | No |
Examples

```
switch messageBox("My message text, my text ... ",50, 3)
case 16 
   print "Yes"
case 32 
   print "No"
else
   print "Cancel"
end
```

```
messageBox("|My Company|This is a message.") // shows My Company in the title bar
```

---

## openColorSelectBox
    Opens the dialog Colors provided by Windows. Remarks
            
            The dialog looks like this:
        
        Syntax
            
```
openColorSelectBox(Color:integer) → integer
```

        
        Parameter
            
            The parameter Color of data type integer designates the active color value. Typically this
                will be a color which you define with the function makeRGBValue.
        
        Return Value
            
            The return value has the data type integer. 
            The return value is the RGB color value of the color selected by the user.
        
        Example
            
```
colorVar := openColorSelectBox(colorVar)
openColorSelectBox(makeRGBValue(255,150,0)) // current color is orange
```

        
        See also
            
            makeRGBValue [SimTalk]

---

## openConsole
    Opens the Console window. 
        
        Syntax
            
```
openConsole → boolean
```

        
        Return Value
            
            The return value has the data type boolean.
        
        Example
            
`openConsole`

        
        See also
            
            Console
            clearConsole [SimTalk]
            closeConsole [SimTalk]
            setConsoleFilter [SimTalk]
            Specifying Start Options

---

## openDateSelectBox
Opens a dialog in which you can select a date. 
Remarks

To set the date you select, click OK. If you
close the dialog with the Close button in the title bar, Plant Simulation returns 1900/01/01, the first of January, 1900.

Syntax

```
openDateSelectBox(TitleText:string[, InitialDate:date]) → date
```

Parameters

The parameter TitleText of data type string designates the caption that the
dialog shows in its title bar.

The optional parameter InitialDate of data type date sets the date you select
in the dialog.

Return Value

The return value has the data type date. 
The return value is the date that the user picked.

Examples

```
openDateSelectBox("Select a date")
print openDateSelectBox("Select a date") // returns 2024/05/18
```

```
openDateSelectBox("Select a date", str_to_date("2024-05-18"))
print openDateSelectBox("Select a date") // returns 2024/05/18
```

---

## openHTMLBrowser
Starts the HTML Browser and opens the address designated by the
parameter of data type string. 
Remarks

To make the HTML Browser open a connection to the local calling Plant Simulation process, type an 
`L`
 or a forward slash 
`/`
 as the first character of the address.
URLs that begin with 
`L/`
 only work when the web
server has been started.
The safety setting File > Model Settings >
General > Prohibit access to the computer affects the function openHTMLBrowser as follows:

It permits only URLs with the protocols http, https, file, UNC paths and normal
paths into the file system.

It does not permit references to executable files for paths into the file
system.
For Plant Simulation executable files are files whose
file extension is listed in the environment variable PATH_EXT.

For paths to files it only permits those paths that point to the model folder or
its sub-folders.

Syntax

```
openHTMLBrowser(WWWAddress:string) → string
```

Parameter

The parameter WWWAddress of data type string designates the address to be
opened.

Return Value

The return value has the data type string.

Examples

```
openHTMLBrowser("https://www.siemens.com/global/en.html")
```

```
openHTMLBrowser("https://www.siemens.com/global/de.html")
```

See also

Prohibit access to the computer [model settings]

---

## openHTMLWindow
Opens a browser window without the properties of a normal HTML browser
window.
Remarks

The safety setting File > Model Settings > General
> Prohibit access to the computer affects the function openHTMLWindow as follows:

It permits only URLs with the protocols http, https, file, UNC paths and normal
paths into the file system.

It does not permit references to executable files for paths into the file
system.
For Plant Simulation executable files are files whose
file extension is listed in the environment variable PATH_EXT.

For paths to files it only permits those paths that point to the model folder or
its sub-folders.

Syntax

```
openHTMLWindow(Address:string, WindowTitle:string, X:integer, Y:integer, Width:integer, Height:integer) → boolean
```

Parameters

The parameter Address of data type string designates the address of the browser
window. 

The parameter WindowTitle of data type string designates the title of the
window. 

The parameter X of data type integer designates the x-coordinate at which the
window opens on screen. 

The parameter Y of data type integer designates the y-coordinate at which the
window opens on screen. 

The parameter Width of data type integer designates the width of the
window.

The parameter Height of data type integer designates the height of the window.

Return Value

The return value has the data type boolean.

Example

```
openHTMLWindow("C:\Temp\mysite.htm", "My Page", 200,400,200,300)
```

See also

Prohibit access to the computer [model settings]
closeHTMLWindow [SimTalk]

---

## openObjectSelectBox
Opens the dialog Select Object. Remarks

The dialog Select Object looks like this:|  |  |

Syntax

```
openObjectSelectBox(Filter:string, FrameOrFolder:object) → string
```

Parameters

The parameter Filter of data type string designates the filter, i.e., the
objects which the list box below Objects shows.

Specify an empty string 
`""`
 to show all objects.

Specify the InternalClassType to only show objects of that type.

Specify 
`":Table"`
 to only show lists and tables.

Specify 
`":MatCarrier"`
 to only show material flow objects.

Specify 
`":Importer"`
 to only show material flow objects that have
importers. 
You can also enter several of these object types separated by colons.
Note 
The internal identifiers for the classes are case-sensitive.

The parameter FrameOrFolder of data type object designates the Frame or the folder for which the dialog Select Object will be initially opened.

Return Value

The return value has the data type string.

Examples

```
var path := openObjectSelectBox("Station", current)
// only shows the objects of type Station in the 'Select Object' dialog
// which are inserted into the simulation model
```

```
var path2 := openObjectSelectBox(":Table", .InformationFlow)
// shows all lists and tables in the 'Select Object' dialog
```

See also

Select Object [for controls]
InternalClassType [SimTalk]

---

## setConsoleFilter
Sets if the Console activates the designated filters or not. 

Syntax

```
setConsoleFilter(Filter:string, Activate:boolean) → boolean
```

Parameters

The parameter Filter of data type string designates the filter.

Info: Information about the model without user input.

Message: Information with user input from dialog windows and message
boxes.

Print: Information from 
`print`
 commands in
Methods.

Debug: Internal program messages for our software engineers.
You can also enter several filters, separated by the pipe symbol |. 

The parameter Activate of data type boolean sets if the filter will be
activated (
`true`
) tor not (
`false`
).

Return Value

The return value has the data type boolean.

Example

```
setConsoleFilter("Info|Message|Debug", false)
```

SimTalk

clearConsole [SimTalk]
closeConsole [SimTalk]
openConsole [SimTalk]

See also

Console
Console filter
Specifying Start Options, 
`-logfile <file name>`
, for example 
```
-logfile
MyLogFile.txt
`Specifying Start Options,`
-NoWarning
```

---

## updateGUI
   Updates the graphical user interface of Plant Simulation. 
      Remarks
         
         If executing a Method takes a long time, it might
            seem that Plant Simulation stopped responding to your input. To
            prevent this from happening, you can every now and then call the function updateGUI within this Method.
         updateGUI redraws the contents of the Frames, but only if the time has elapsed that is equal to the
            reciprocal of the frame rate you specified under File >
               Preferences > Simulation > Frame rate. This makes sure that Plant Simulation does not use up too much time for
            redrawing.
      
      
      Syntax
         
```
updateGUI -> integer
updateGUI([forceUpdateNow:boolean:=false]) -> integer
```

      
      Parameter
         
         Specify the optional parameter forceUpdateNow
            and set it to 
`true`
 to enforce an immediate update of
            the user interface. 
         Do not specify the parameter or set it to 
`false`
 to only redraw the user interface one time after some time has passed
            since the last update. This time depends on the frame rate that you specified under
               File > Preferences > Simulation > Frame
               rate.
         Default Value of the Parameter
         The default value is false.
      
      Example
         
```
for var y := 1 to JTFileTable.yDim 
   MyFrame._3D.importGraphics([0,y,0], JTFileTable[1,y], false, true)
   updateGUI
next 
```

      
      See also
         
         Frame rate [model settings]
