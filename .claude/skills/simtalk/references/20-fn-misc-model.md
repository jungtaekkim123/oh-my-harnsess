> **Read this when:** Model operations: `closeModel`, `loadModel`, `saveModel`, `existsFile`, `existsObject`, library management  
> **Skip this when:** Application environment (see 19) or simulation runtime control (see 21)


## Contents

- [closeModel - global function](#closemodel---global-function)
- [connectAutomatically](#connectautomatically)
- [deleteFile](#deletefile)
- [existsFile](#existsfile)
- [existsMethod](#existsmethod)
- [existsObject - 2D](#existsobject---2d)
- [getFileModificationDateTime](#getfilemodificationdatetime)
- [getLibrariesDirectories](#getlibrariesdirectories)
- [getLibraryFiles](#getlibraryfiles)
- [getLibraryVersionFromFile](#getlibraryversionfromfile)
- [loadModel](#loadmodel)
- [makePathRelative](#makepathrelative)
- [modelFile](#modelfile)
- [readStringFromFile](#readstringfromfile)
- [saveFolderModel](#savefoldermodel)
- [saveModel](#savemodel)
- [writeStringToFile](#writestringtofile)

## closeModel - global function
Closes the open simulation model without saving it. 
Remarks

Note 
You can also define a Method with the name onCloseModel in any folder in the Class Library,
including the Basis folder. This Method is being executed when you close the model or when you exit Plant
Simulation. You can, for example, program clean-up tasks, delete temporary files, etc. 
The method onCloseModel has to declare the boolean
parameter 
`onExitApplication`
. Plant
Simulation sets this parameter to 
`false`
 when onCloseModel is called when you close the model. Plant
Simulation sets this parameter to 
`true`
 when onCloseModel is called when you exit Plant Simulation.

You can also program several onCloseModel methods and
place them into different folders. Plant Simulation then calls all existing
onCloseModel method classes in the Class Library
when you close the model or exit the application.

Syntax

```
closeModel → boolean
```

Return Value

The return value has the data type boolean.
Plant Simulation returns 
`false`
 in these cases and does not close the
model:

When you call the function in sub-routines.

When you call the function in user-defined attributes of data type method.

When you call the function in formulas.
Note 
If you want to save your simulation model before you close it, you have to call
the function saveModel before calling the function closeModel.

Note 
If the model is closed, all existing onCloseModel method classes in the Class
Library, including the onCloseModel method located in the Basis
folder, are called. Within these methods you can execute clean-up tasks, for example delete
temporary files.

Example

`closeModel`

See also

Close Model
close3D [SimTalk]
loadModel [SimTalk]
saveModel [SimTalk]

---

## connectAutomatically
    Automatically connects the object designated by <Path> with objects located in
        its vicinity whose entrances and exits are close together. 
        Remarks
            
            We added this function because creating an object with SimTalk does not automatically connect it.
            The following applies for automatically connecting the length-oriented
                objects Turnplate, Turntable, AngularConverter, Conveyor, Converter, Track, and TwoLaneTrack in 3D: 
            If TransferLengthToObject is off for one of these objects in
                3D, but if a suitable MU animation path
                exists, then Plant Simulation uses the start point and the
                end point of these animation paths for automatically connecting the objects and for
                displaying Connectors. Suitable MU animation paths are Default or Cross for the Converter, lane A or lane B for the TwoLaneTrack and Default for the
                remaining objects. This applies for Connect objects
                    automatically and for the method connectAutomatically.
        
        
        Syntax
            
```
<Path>.connectAutomatically -> boolean
```

        
        Return Value
            
            The return value has the data type boolean.
        
        Example
            
`MyStation.connectAutomatically`

        
        See also
            
            Connect objects automatically [model settings]
            TransferLengthToObject [SimTalk]

---

## deleteFile
    Deletes the specified file for good. 
        Remarks
            
            You can use deleteFile to delete any file you
                do not need any longer.
        
        
        Syntax
            
```
deleteFile(FileName:string) -> integer
```

        
        Parameter
            
            The parameter FileName of data type string designates the file you
                want to delete.
        
        Return Value
            
            The return value has the data type integer. 
            Is the Windows error code.
            Is 0 if no error occurred.
        
        Example
            
```
deleteFile("MyFile")              // deletes the file named MyFile from the installation folder
deleteFile("D:\Publisher.gif")    // deletes the graphics file from the D drive
```

---

## existsFile
   Returns if a file or folder exists (true) or does not exist (false).
      
      Syntax
         
```
existsFile(NameOfFileOrFolder:string) → boolean
```

      
      Parameter
         
         The parameter NameOfFileOrFolder of data type string designates the
            file or the folder.
      
      Return Value
         
         The return value has the data type boolean.
      
      Examples
         
```
var fileName: string
fileName := "MyDataTable.tab"
if not existsFile(fileName) 
   table.writeFile(fileName)
else
   print "The file ",fileName," already exists."
end
```

```
print existsFile("noname.mod")
print existsFile("C:\Program Files\Siemens\Tecnomatix Plant Simulation XX\Help\PlantSimulationENU.chm")
```

---

## existsMethod
    Returns if a path points to a Method object or to a user-defined attribute of data type method
        or not.
        
        Syntax
            
```
existsMethod(NameOfMethod:string) → boolean
```

        
        Parameter
            
            The parameter NameOfMethod of data type string designates the path
                of the Method.
        
        Return Value
            
            The return value has the data type boolean.
            true if the Method object or the user-defined attribute of data type method exists.
            false if it does not exist. 
        
        Example
            
```
print existsMethod("Station.MethodAttr")
```

---

## existsObject - 2D
   Returns if a path to a simulation object is valid or not.
      
      Syntax
         
```
existsObject(NameOfObject:string) → boolean
```

      
      Parameter
         
         The parameter NameOfObject of data type string designates the path of
            the object.
      
      Return Value
         
         The return value has the data type boolean.
         true if the object exists.
         false if it does not exist.
      
      Examples
         
```
print existsObject(".Mus.Part:123")
```

```
if existsObject("ProdFrame")
   ProdFrame.derive(current,100,200)
end
```

      
      See also
         
         _3D.existsObject [SimTalk]
         extendPath [SimTalk]

---

## getFileModificationDateTime
    Returns the date and the point in time at which the file was last
        written.
        
        Syntax
            
```
getFileModificationDateTime(FilePath:string) → dateTime
```

        
        Parameter
            
            The parameter FilePath of data type string designates the path of a
                file for which you would like to know when it was written to last. 
            You have to enter the entire file path, including the name of the file and the file
                extension .spp.
        
        Return Value
            
            The return value has the data type dateTime.
        
        Example
            
```
print getFileModificationDateTime("D:\MyControls.spp") 
// might, for example, return 26.10.2016 14:53:15.7710
```

---

## getLibrariesDirectories
    Returns the Libraries directories which you set
        in the Preferences.
        
        Syntax
            
```
getLibrariesDirectories → string[]
```

        
        Return Value
            
            The return value is an array of data type string.
        
        Example
            
```
print getLibrariesDirectories // might return [D:\MeineBibliotheken\, D:\MyLibraries\]
```

        
        See also
            
            Libraries directories

---

## getLibraryFiles
   Returns the file paths to .pslib files and all their versions.
      
      Syntax
         
```
getLibraryFiles(FolderPath:string) → string[]
```

      
      Parameter
         
         The parameter FolderPath of data type string is the path of a library
            folder. The library does not have to exist in the currently loaded model.
      
      Return Value
         
         The return value is an array of data type string. 
         The return value contains all file paths to .pslib files and all versions. The
               array always contains a files path and the associated library version
            alternating. The  array is sorted in descending order according to version
            number. 
         The returned array is empty if no .pslib file is found for the library.
      
      Example
         
```
var arr: string[] := getLibraryFiles(".Tools.ExperimentManager")
print "Number of library files: ", arr.dim / 2
print "Newest file: ", when arr.dim > 0 then arr[1] else "(not found)"
var i : integer := 1
while i < arr.dim
   print "File: ", arr[i], "  Version: ", arr[i+1]
   i += 2
end
```

---

## getLibraryVersionFromFile
    Returns the version of the library designated by <Path>. 
        
        Syntax
            
```
<Path>.getLibraryVersionFromFile(FilePath:string) → string
```

        
        Parameter
            
            The parameter FilePath of data type string has to be the path to a
                library file (.pslib).
        
        Return Value
            
            The return value has the data type string. 
        
        Example
            
```
print getLibraryVersionFromFile("C:\Program Files\Siemens\Plant Simulation 2404\Libraries\Tools\MyLibrary.pslib")
```

        
        See also
            
            getLibraryInfo [SimTalk]

---

## loadModel
  Loads the specified simulation model.
    Remarks
      
      If you cleared the security setting File >
          Model Settings > General > Prohibit access to the computer, the function
        can copy data from another folder and write it to the model folder or its sub-folders. It
        cannot copy data from the model folder or its sub-folders.
    
    
    Syntax
      
```
loadModel(ModelName:string[, Password:string]) → boolean
```

    
    Parameters
      
      
        
          The parameter ModelName of data type string designates the path of
            the simulation model.
        
        
          The optional parameter Password of data type string designates the
            password that is used for opening an encrypted model file.
        
      
      Note 
        The function only works if no model is loaded at the moment. Typically,
          you will use the function directly after a call of the function closeModel, or
          from external interfaces, such as the COM interface.
      
    
    Return Value
      
      The return value has the data type boolean.
    
    Examples
      
```
closeModel
loadModel("C:\MySimulationData\myModel.spp", "MyPassword123")
```

```
closeModel
loadModel("D:\MyModels\MyFolderModel.psfm\$.spp")
```

    
    See also
      
      Prohibit access to the computer [model settings]
      Open Model File
      Save As Folder Model
      closeModel [SimTalk] - global function
      saveFolderModel [SimTalk]
      saveModel [SimTalk]

---

## makePathRelative
Converts an absolute path to a relative path. 

Syntax

```
makePathRelative(Path:string[, StartObject:object]) → string
makePathRelative(Path:object[, StartObject:object]) → string
```

Parameters

The parameter Path of data type string or object designates the path. 
Plant Simulation converts this path into a relative path starting with the
Frame in which the Method is located. 

The optional parameter StartObject of data type object sets the object from
which on Plant Simulation starts evaluating the Path. 

Return Value

The return value has the data type string. 
Is an empty string "" if the path is not valid. 

Example

```
Station.ExitCtrl := makePathRelative(Station.ExitCtrl)
```

See also

The Absolute Path
The Relative Path

---

## modelFile
    Returns the name of the active model file and the folder within which it is
        located.
        
        Syntax
            
```
modelFile → string
```

        
        Return Value
            
            The return value has the data type string.
        
        Example
            
```
print modelFile // outputs for example D:\Public\Plant Models\MyPlantAnytown.spp
```

        
        See also
            
            Open Model File
            saveModel [SimTalk]

---

## readStringFromFile
    Reads the entire contents of the file and returns it as a value of data type string. 
        Remarks
            
            If the file starts with a BOM (Byte Order Mark), it will be evaluated
                and not returned as part of the string.
        
        
        Syntax
            
```
readStringFromFile(FileName:string) -> string
```

        
        Parameter
            
            The parameter FileName of data type string designates the file
                whose contents you would like to read. 
        
        Return Value
            
            The return value has the data type string. 
        
        Example
            
```
var s: string := readStringFromFile(ApplicationHome + "Templates\English\Interaction\Interaction_connect.txt")
print s
```

        
        See also
            
            writeStringToFile [SimTalk]
            bytes_to_str [SimTalk]

---

## saveFolderModel
Saves the simulation model in a folder/file structure which facilitates storing your
model in a version control system such as Git.

Syntax

```
saveFolderModel(FileName:string[, CompactFormat:boolean:=false, UseGit:boolean:=false])
```

Parameters

The parameter FileName of data type string sets the path to and the name of the
model. 

The optional parameter CompactFormat of data type boolean sets if Plant
Simulation saves the objects inside of Frames, which have an origin, to an individual
.yaml file (
`true`
) or not (
`false`
). 
For the default setting false all the objects are saved into the $.yaml
file of the Frame. This reduces the number of files stored in the file system. This can be
important for very large models to get a reasonable performance.
Default Value of the Parameter
The default value is false.

The optional parameter UseGit of data type boolean sets if Plant
Simulation creates a Git repository when the folder model is saved for
the first time (
`true`
) or not (
`false`
). 
The initial version will be committed automatically. This option is only available if
Git is installed on your computer. In addition a .gitignore file is
created in the top level folder. The content of this file ignores the
.UserSettings.yaml so that it is not put under version control. 
Default Value of the Parameter
The default value is false.

Example

```
saveFolderModel("D:\MyModels\MyDeportioner.psfm", true, true)
```

See also

Save As Folder Model
loadModel [SimTalk]

---

## saveModel
    Saves the current model with the file name you specify. 
        Remarks
            
            If the file name does not specify a directory, Plant Simulation saves the model into the current directory which you can
                set with the function setCurrentDirectory. 
            If you did not set the current directory, it will be the directory
                into which you last saved a Plant Simulation model or a Plant Simulation item (icon, data table, etc.). 
            The method modelFile returns the current name of the model
                and the current folder of the model file. 
            Note 
                If you call the function saveModel
                    within a formula or within an executeSilent command,
                        Plant Simulation does not save any call chains into
                    the model. This means that it does not save the currently called Method or the already scheduled Methods nor suspended Methods. 
            
            If you deactivate the safety setting File
                    > Model Settings > General > Prohibit access to the
                    computer, the function saveModel can copy
                data from another folder and write them to the model folder or its sub-folders. The
                function cannot copy files from the model folder or its sub-folders. 
        
        
        Syntax
            
```
saveModel(ModelName:string[, StopMethodExecution:boolean[, UseNewName:boolean[, SaveCallChains:boolean]]]) → boolean
```

        
        Parameters
            
            
                
                    The parameter ModelName of data type
                            string designates the name of the model file.
                        This can be a fully qualified path.
                
                
                    The optional parameter StopMethodExecution of data type
                            boolean sets if Plant Simulation stops executing
                        methods (
`true`
) or if method execution will be continued
                            (
`false`
) after loading the model. If method execution is
                        stopped, Plant Simulation opens the Method Debugger and
                        highlights the line after the saveModel instruction. The default
                        setting is 
`false`
.
                    The simulation is stopped in both cases after loading the
                        model. The parameter StopMethodExecution of data
                        type boolean only affects method execution.
                
                
                    The optional parameter UseNewName of data type boolean sets
                        if the current model is to use the file name designated by the parameter of
                        data type string (
`true`
), or if the model is to
                        keep its name (
`false`
). 
                    Default Value of the Parameter
                    The default value is true.
                
                
                    The optional parameter SaveCallChains of data type boolean
                        sets if all call chains in the model file are going to be saved
                            (
`true`
) or not (
`false`
).
                    When you specify 
`false`

                        Plant Simulation does not save the Methods being executed at the moment and suspended
                            Methods.
                    Default Value of the Parameter
                    The default value is true.
                
            
        
        Return Value
            
            The return value has the data type boolean.
        
        Example
            
```
print saveModel("C:\Temp\MyModel1.spp", false)

if not EventController.isRunning // was the model just loaded?
   if messageBox("Continue the simulation?",48,2) = 16 // Yes?
       EventController.start
   end
end 
```

        
        See also
            
            Prohibit access to the computer [model settings]
            Save Model File
            setCurrentDirectory [SimTalk]
            closeModel [SimTalk] - global function
            loadModel [SimTalk]
            modelFile [SimTalk]

---

## writeStringToFile
Writes the contents of the specified Text to a file.

Syntax

```
writeStringToFile(Text:string, FileName:string[, Append:boolean, Encoding:string:="UTF-8"])
```

Parameters

The parameter Text of data type string designates the text which you would like
to write to the file.

The parameter FileName of data type string designates the file or the directory
path and the name of the file into which the file will be written. If the file exists, it will be
overwritten. 

The optional parameter append of data type boolean sets if Plant
Simulation deletes the existing content before writing (
`false`
) or if it does
not delete it before writing and appends a line break (Carriage Return + Line Feed) to the written
text (
`true`
).

Do not specify the optional parameter Encoding of data
type string or specify 
`"UTF-8"`
, to save
the file in UTF-8-format with a BOM (Byte Order Mark). 
Specify 
`"Unicode"`
 or 
`"UTF-16"`
 for Encoding, to save the file in UTF-16-format with a
BOM. 
Specify an empty string 
`""`
 to save the file as
UTF-8 without BOM.
Default Value of the Parameter
The default value is 
`"UTF-8"`
.

Examples

```
writeStringToFile("hello world", "C:\Users\Public\Public Documents\a.txt")
```

```
var data:json

data["Name"] = "John Doe"
data["Profession"] = "Simulation specialist"
data["NumProjects"] = 378

// JSON must have a BOM, so turn it off with empty last argument
writeStringToFile(data.asString, "D:\tnt.json", false, "")

```

See also

readStringFromFile [SimTalk]
