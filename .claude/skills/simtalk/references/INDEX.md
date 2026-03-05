# SimTalk 2.0 Reference Index

**Jump to:** [Part 1 — File Router](#part-1--file-router) | [Part 2 — Function Lookup](#part-2--function-lookup)

## Part 1: File Router

| # | Category | File | Description | When to open |
|---|----------|------|-------------|--------------|
| 01 | Language Basics | 01-overview.md | SimTalk intro, quick tour, simple values | First contact, 'what is SimTalk' |
| 02 | Language Basics | 02-migration.md | SimTalk 2.0 vs 1.0 comparison + outdated names | Migration, converting old code |
| 03 | Language Basics | 03-general-access.md | General access to simulation objects | Accessing object attributes, methods |
| 04 | Language Basics | 04-names-identifiers.md | Identifiers, keywords, reserved words | Naming rules, keyword conflicts |
| 05 | Language Basics | 05-names-paths.md | Object paths, namespaces, qualified names | Object references, `basis` keyword |
| 06 | Language Basics | 06-constants-variables.md | Constants, variables, parameters | var/const/param declaration, byref |
| 07 | Data Types | 07-datatypes-primitive.md | Scalar types (boolean, integer, real, string, date, time, units) | Primitive type ranges, unit behavior |
| 08 | Data Types | 08-datatypes-array.md | Array type + all array methods | Array creation, indexing, append, sort |
| 09 | Data Types | 09-datatypes-json.md | JSON type + methods | JSON parsing, asString, nested access |
| 10 | Data Types | 10-datatypes-collections.md | List, Queue, Stack, Table | Collections, create, FIFO/LIFO |
| 11 | Syntax | 11-operators.md | Operators and expressions | Arithmetic, comparison, ~=, mod, div, & operator |
| 12 | Syntax | 12-control-flow.md | Control flow statements | if/for/while/switch/waituntil/try-catch |
| 13 | Functions | 13-fn-os.md | OS functions | File I/O, clipboard, folder browsing |
| 14 | Functions | 14-fn-math.md | Math functions | abs, ceil, floor, sqrt, trig, random |
| 15 | Functions | 15-fn-bits.md | Bit manipulation functions | BitAND/OR/XOR/Set/Test/Shift |
| 16 | Functions | 16-fn-strings.md | String functions | strlen, substr, regex, formatting |
| 17 | Functions | 17-fn-datetime.md | Date/time functions | CalendarWeek, sysDate, time arithmetic |
| 18 | Functions | 18-fn-http.md | HTTP client functions | REST API, GET/POST/PUT/DELETE, headers |
| 19 | Functions | 19-fn-misc-app.md | Application/environment functions | applicationHome, version, license |
| 20 | Functions | 20-fn-misc-model.md | Model/file operations | closeModel, loadModel, saveModel |
| 21 | Functions | 21-fn-misc-simulation.md | Simulation control functions | callEvery, event scheduling, seeds |
| 22 | Functions | 22-fn-misc-ui.md | UI/dialog functions | console, messageBox, HTML windows |
| 23 | Functions | 23-fn-misc-util.md | Utility/crypto functions | checkID, SHA hashing, geometry, profiling |
| 24 | Functions | 24-fn-datatype-query.md | Data type query functions | Type checking, is_* predicates |
| 25 | Functions | 25-fn-io.md | Input/output functions | print, beep, bell, console I/O |
| 26 | Functions | 26-fn-conversion.md | Type conversion functions | *_to_num, *_to_str, unit conversion |
| 27 | Functions | 27-fn-debug.md | Debug functions | Breakpoints, tracing, debugAssert |

---

## Part 2: Function → File Lookup

| Function | File |
|----------|------|
| Acceleration | 07-datatypes-primitive.md |
| acceleration_to_num | 26-fn-conversion.md |
| and | 04-names-identifiers.md |
| Any | 07-datatypes-primitive.md |
| append | 08-datatypes-array.md |
| appendArray (Array) | 08-datatypes-array.md |
| appendValueOfType | 08-datatypes-array.md |
| applicationVersion | 19-fn-misc-app.md |
| asAny | 08-datatypes-array.md |
| asString (JSON) | 09-datatypes-json.md |
| atan2 | 14-fn-math.md |
| autoexec | 04-names-identifiers.md |
| autoexecLoadObj | 04-names-identifiers.md |
| basis | 05-names-paths.md |
| beep | 25-fn-io.md |
| bell | 25-fn-io.md |
| BitAND | 15-fn-bits.md |
| BitClear | 15-fn-bits.md |
| BitOR | 15-fn-bits.md |
| BitSet | 15-fn-bits.md |
| BitShift | 15-fn-bits.md |
| BitTest | 15-fn-bits.md |
| BitXOR | 15-fn-bits.md |
| bool_to_num | 26-fn-conversion.md |
| bool_to_str | 26-fn-conversion.md |
| Boolean | 06-constants-variables.md |
| Boolean | 07-datatypes-primitive.md |
| browseForFolder | 13-fn-os.md |
| byref | 11-operators.md |
| bytes_to_str | 26-fn-conversion.md |
| calcBrakingDistance | 23-fn-misc-util.md |
| calcDroppedPerpendicularFootPoint | 23-fn-misc-util.md |
| CalendarWeek | 17-fn-datetime.md |
| CalendarYear | 17-fn-datetime.md |
| case | 04-names-identifiers.md |
| Cauchy | 14-fn-math.md |
| checkForLicense | 19-fn-misc-app.md |
| checkID | 23-fn-misc-util.md |
| clearLogFile | 22-fn-misc-ui.md |
| closeAllWindows | 22-fn-misc-ui.md |
| closeConsole | 22-fn-misc-ui.md |
| closeHTMLWindow | 22-fn-misc-ui.md |
| computeSHA1Hash | 23-fn-misc-util.md |
| computeSHA3Hash | 23-fn-misc-util.md |
| connectAutomatically | 20-fn-misc-model.md |
| contains | 08-datatypes-array.md |
| contains (JSON) | 09-datatypes-json.md |
| continue | 04-names-identifiers.md |
| copy (JSON) | 09-datatypes-json.md |
| copyFile | 13-fn-os.md |
| copyFromTable | 08-datatypes-array.md |
| copyFromTableColumn | 08-datatypes-array.md |
| copyObjectsToClipboard | 13-fn-os.md |
| copyTextToClipboard | 13-fn-os.md |
| copyToTable | 08-datatypes-array.md |
| copyToTableColumn | 08-datatypes-array.md |
| copyToTableColumn (JSON) | 09-datatypes-json.md |
| copyToTableRow (JSON) | 09-datatypes-json.md |
| create (List) | 10-datatypes-collections.md |
| createCombinations | 23-fn-misc-util.md |
| createLicenseFile | 19-fn-misc-app.md |
| createNestedList | 10-datatypes-collections.md |
| createPermutations | 23-fn-misc-util.md |
| current | 05-names-paths.md |
| currentEventCtl | 21-fn-misc-simulation.md |
| Date | 07-datatypes-primitive.md |
| DateTime | 07-datatypes-primitive.md |
| datetime_to_str | 26-fn-conversion.md |
| day | 17-fn-datetime.md |
| dayOfWeek | 17-fn-datetime.md |
| dayOfYear | 17-fn-datetime.md |
| debug | 27-fn-debug.md |
| decodeBase64Data | 18-fn-http.md |
| decodeQuotedPrintableString | 18-fn-http.md |
| deg2rad | 23-fn-misc-util.md |
| delete | 08-datatypes-array.md |
| delete (JSON) | 09-datatypes-json.md |
| deleteAllDebugExpressions | 23-fn-misc-util.md |
| deleteFile | 20-fn-misc-model.md |
| deleteSuspendedMethods | 27-fn-debug.md |
| deleteValue | 08-datatypes-array.md |
| Dim | 08-datatypes-array.md |
| Dim (JSON) | 09-datatypes-json.md |
| div | 04-names-identifiers.md |
| downto | 04-names-identifiers.md |
| else | 04-names-identifiers.md |
| elseif | 04-names-identifiers.md |
| Empty | 08-datatypes-array.md |
| enableFullScreenMode | 19-fn-misc-app.md |
| encodeDataBase64 | 18-fn-http.md |
| encodeStringQuotedPrintable | 18-fn-http.md |
| end | 04-names-identifiers.md |
| endSim | 04-names-identifiers.md |
| execute | 23-fn-misc-util.md |
| executePythonFile | 23-fn-misc-util.md |
| executeSilent | 23-fn-misc-util.md |
| existsFile | 20-fn-misc-model.md |
| existsMethod | 20-fn-misc-model.md |
| existsObject | 20-fn-misc-model.md |
| exitApplication | 19-fn-misc-app.md |
| exitloop | 04-names-identifiers.md |
| false | 04-names-identifiers.md |
| find | 08-datatypes-array.md |
| for | 04-names-identifiers.md |
| for | 12-control-flow.md |
| forget | 04-names-identifiers.md |
| Fréchet | 14-fn-math.md |
| getApplicationProcessID | 13-fn-os.md |
| getCallStack | 23-fn-misc-util.md |
| getCommandLineArg | 19-fn-misc-app.md |
| getCurrentDirectory | 13-fn-os.md |
| getDate | 17-fn-datetime.md |
| getEnv | 13-fn-os.md |
| getEpsilon | 19-fn-misc-app.md |
| getErrorStop | 27-fn-debug.md |
| getFileModificationDateTime | 20-fn-misc-model.md |
| getFilesOfFolder | 13-fn-os.md |
| getHighResolutionClock | 19-fn-misc-app.md |
| getLibrariesDirectories | 20-fn-misc-model.md |
| getLibraryFiles | 20-fn-misc-model.md |
| getLibraryVersionFromFile | 20-fn-misc-model.md |
| getLogFile | 22-fn-misc-ui.md |
| getOrCreateJSON (JSON) | 09-datatypes-json.md |
| getProfileCallCycles | 23-fn-misc-util.md |
| getRegistry | 13-fn-os.md |
| getSeedTable | 21-fn-misc-simulation.md |
| getSimTalkTypename | 24-fn-datatype-query.md |
| getStandardColor | 22-fn-misc-ui.md |
| getTextFromClipboard | 13-fn-os.md |
| getUnit | 25-fn-io.md |
| getValueOfType | 08-datatypes-array.md |
| Gumbel | 14-fn-math.md |
| hideBBL | 19-fn-misc-app.md |
| httpCreateFormURLEncodedString | 18-fn-http.md |
| httpCreateURL | 18-fn-http.md |
| httpDeleteRequest | 18-fn-http.md |
| httpGetRequest | 18-fn-http.md |
| httpGetTimeouts | 18-fn-http.md |
| httpHeadRequest | 18-fn-http.md |
| httpOptionsRequest | 18-fn-http.md |
| httpPostFileRequest | 18-fn-http.md |
| httpPostRequest | 18-fn-http.md |
| httpPutFileRequest | 18-fn-http.md |
| httpPutRequest | 18-fn-http.md |
| httpSetTimeouts | 18-fn-http.md |
| httpSplitFormUrlEncodedString | 18-fn-http.md |
| httpSplitURL | 18-fn-http.md |
| if | 04-names-identifiers.md |
| ignoreBreakpoints | 27-fn-debug.md |
| infoBox | 25-fn-io.md |
| init | 04-names-identifiers.md |
| Init | 04-names-identifiers.md |
| insert | 08-datatypes-array.md |
| Integer | 06-constants-variables.md |
| Integer | 07-datatypes-primitive.md |
| isAcceleration | 24-fn-datatype-query.md |
| isArray (Array) | 24-fn-datatype-query.md |
| isBoolean | 24-fn-datatype-query.md |
| isComputerAccessPermitted | 19-fn-misc-app.md |
| isDate | 24-fn-datatype-query.md |
| isDatetime | 24-fn-datatype-query.md |
| isInteger | 24-fn-datatype-query.md |
| isJson (JSON) | 24-fn-datatype-query.md |
| isLength | 24-fn-datatype-query.md |
| isList | 24-fn-datatype-query.md |
| isListRange | 24-fn-datatype-query.md |
| isObject | 24-fn-datatype-query.md |
| isQueue | 24-fn-datatype-query.md |
| isReal | 24-fn-datatype-query.md |
| isSet | 23-fn-misc-util.md |
| isSpeed | 24-fn-datatype-query.md |
| isStack | 24-fn-datatype-query.md |
| isString | 24-fn-datatype-query.md |
| isTable | 24-fn-datatype-query.md |
| isTime | 24-fn-datatype-query.md |
| isValidDateString | 26-fn-conversion.md |
| isValidDateTimeString | 26-fn-conversion.md |
| isValidTimeString | 26-fn-conversion.md |
| isWeight | 24-fn-datatype-query.md |
| join | 08-datatypes-array.md |
| keepWindowsAlwaysOnTop | 19-fn-misc-app.md |
| language | 19-fn-misc-app.md |
| Laplace | 14-fn-math.md |
| Length | 07-datatypes-primitive.md |
| length_to_num | 26-fn-conversion.md |
| licenseName | 19-fn-misc-app.md |
| loadModel | 20-fn-misc-model.md |
| Logistic | 14-fn-math.md |
| Loglogistic | 14-fn-math.md |
| loop | 04-names-identifiers.md |
| Magnitude | 08-datatypes-array.md |
| make2DimArray (Array) | 26-fn-conversion.md |
| makePathRelative | 20-fn-misc-model.md |
| makeRGBValue | 23-fn-misc-util.md |
| max | 08-datatypes-array.md |
| messageBox | 22-fn-misc-ui.md |
| Method | 07-datatypes-primitive.md |
| min | 08-datatypes-array.md |
| mod | 04-names-identifiers.md |
| modelFile | 20-fn-misc-model.md |
| month | 17-fn-datetime.md |
| next | 04-names-identifiers.md |
| normalize | 08-datatypes-array.md |
| not | 04-names-identifiers.md |
| num_to_acceleration | 26-fn-conversion.md |
| num_to_bool | 26-fn-conversion.md |
| num_to_hex | 26-fn-conversion.md |
| num_to_length | 26-fn-conversion.md |
| num_to_speed | 26-fn-conversion.md |
| num_to_str | 26-fn-conversion.md |
| num_to_time | 26-fn-conversion.md |
| num_to_weight | 26-fn-conversion.md |
| numOfLimitedObjects | 19-fn-misc-app.md |
| obj_to_str | 26-fn-conversion.md |
| Object | 05-names-paths.md |
| Object | 07-datatypes-primitive.md |
| openColorSelectBox | 22-fn-misc-ui.md |
| openConsole | 22-fn-misc-ui.md |
| openDateSelectBox | 22-fn-misc-ui.md |
| openHTMLBrowser | 22-fn-misc-ui.md |
| openHTMLWindow | 22-fn-misc-ui.md |
| openObjectSelectBox | 22-fn-misc-ui.md |
| or | 04-names-identifiers.md |
| Paralogistic | 14-fn-math.md |
| param | 04-names-identifiers.md |
| Pareto | 14-fn-math.md |
| parse | 09-datatypes-json.md |
| pi | 06-constants-variables.md |
| pop | 08-datatypes-array.md |
| print | 25-fn-io.md |
| prio | 04-names-identifiers.md |
| processTime | 21-fn-misc-simulation.md |
| profiler | 23-fn-misc-util.md |
| prompt | 25-fn-io.md |
| promptList1 | 25-fn-io.md |
| promptListN | 25-fn-io.md |
| putValuesIntoTable | 23-fn-misc-util.md |
| Queue | 10-datatypes-collections.md |
| rad2deg | 23-fn-misc-util.md |
| readBytesFromFile | 18-fn-http.md |
| readStringFromFile | 20-fn-misc-model.md |
| Real | 06-constants-variables.md |
| Real | 07-datatypes-primitive.md |
| regex_replace | 16-fn-strings.md |
| regex_search | 16-fn-strings.md |
| regex_search2 | 16-fn-strings.md |
| repeat | 04-names-identifiers.md |
| repeat | 12-control-flow.md |
| reset | 04-names-identifiers.md |
| resetProfile | 23-fn-misc-util.md |
| resetRandomNumberStream | 21-fn-misc-simulation.md |
| result | 04-names-identifiers.md |
| return | 04-names-identifiers.md |
| root | 05-names-paths.md |
| rootfolder | 05-names-paths.md |
| saveFolderModel | 20-fn-misc-model.md |
| saveModel | 20-fn-misc-model.md |
| saveProfile | 23-fn-misc-util.md |
| selectFileForOpen | 13-fn-os.md |
| selectFileForSave | 13-fn-os.md |
| self | 05-names-paths.md |
| sendSMTPMail | 23-fn-misc-util.md |
| setAnimationRefreshRate | 21-fn-misc-simulation.md |
| setAntitheticRandomNumbers | 21-fn-misc-simulation.md |
| setCodePage | 13-fn-os.md |
| setConsoleFilter | 22-fn-misc-ui.md |
| setCurrentDirectory | 13-fn-os.md |
| setDaylightSavingTime | 17-fn-datetime.md |
| setEnv | 13-fn-os.md |
| setEpsilon | 19-fn-misc-app.md |
| setErrorHandler | 27-fn-debug.md |
| setErrorStop | 27-fn-debug.md |
| setInfiniteLoopDetectionTimeout | 21-fn-misc-simulation.md |
| setMaxDepthOfCalls | 27-fn-debug.md |
| setMaxNumberOfCallChains | 27-fn-debug.md |
| setMaxNumberOfSamples | 27-fn-debug.md |
| setMaxSuspendedMethods | 27-fn-debug.md |
| setMUTraceRouteMethod | 21-fn-misc-simulation.md |
| setPythonDLLPath | 19-fn-misc-app.md |
| setRandomSeedCounter | 21-fn-misc-simulation.md |
| setSeedTable | 21-fn-misc-simulation.md |
| SHGetKnownFolderPath | 13-fn-os.md |
| showStatisticsReport | 21-fn-misc-simulation.md |
| sleep | 13-fn-os.md |
| sort | 08-datatypes-array.md |
| Speed | 07-datatypes-primitive.md |
| speed_to_num | 26-fn-conversion.md |
| splitString | 16-fn-strings.md |
| splitStringToNum | 16-fn-strings.md |
| Stack | 10-datatypes-collections.md |
| startExtProc | 13-fn-os.md |
| stopuntil | 04-names-identifiers.md |
| str_to_acceleration | 26-fn-conversion.md |
| str_to_bool | 26-fn-conversion.md |
| str_to_date | 26-fn-conversion.md |
| str_to_dateTime | 26-fn-conversion.md |
| str_to_length | 26-fn-conversion.md |
| str_to_method | 26-fn-conversion.md |
| str_to_num | 26-fn-conversion.md |
| str_to_obj | 26-fn-conversion.md |
| str_to_speed | 26-fn-conversion.md |
| str_to_table | 26-fn-conversion.md |
| str_to_time | 26-fn-conversion.md |
| str_to_weight | 26-fn-conversion.md |
| strAscii | 16-fn-strings.md |
| strChr | 16-fn-strings.md |
| strCopy | 16-fn-strings.md |
| strHash | 23-fn-misc-util.md |
| strIncl | 16-fn-strings.md |
| String | 06-constants-variables.md |
| String | 07-datatypes-primitive.md |
| strLen | 16-fn-strings.md |
| strLPos | 16-fn-strings.md |
| strOmit | 16-fn-strings.md |
| strRcopy | 16-fn-strings.md |
| strRpos | 16-fn-strings.md |
| strToHtml | 16-fn-strings.md |
| strToLower | 16-fn-strings.md |
| strToUpper | 16-fn-strings.md |
| strTrim | 16-fn-strings.md |
| sum | 08-datatypes-array.md |
| switch | 04-names-identifiers.md |
| sysDate | 17-fn-datetime.md |
| system | 13-fn-os.md |
| Table | 10-datatypes-collections.md |
| then | 04-names-identifiers.md |
| throwRuntimeError | 23-fn-misc-util.md |
| Time | 07-datatypes-primitive.md |
| Time | 12-control-flow.md |
| time_to_num | 26-fn-conversion.md |
| time_to_str | 26-fn-conversion.md |
| timeOfDay | 17-fn-datetime.md |
| timeRepresenation | 26-fn-conversion.md |
| to | 04-names-identifiers.md |
| to_str | 26-fn-conversion.md |
| true | 04-names-identifiers.md |
| unshareAndDelete | 09-datatypes-json.md |
| until | 04-names-identifiers.md |
| updateGUI | 22-fn-misc-ui.md |
| userInterfaceLanguage | 19-fn-misc-app.md |
| var | 04-names-identifiers.md |
| void | 11-operators.md |
| wait | 04-names-identifiers.md |
| waitExpired | 04-names-identifiers.md |
| waituntil | 04-names-identifiers.md |
| waituntil | 12-control-flow.md |
| week | 17-fn-datetime.md |
| Weight | 07-datatypes-primitive.md |
| weight_to_num | 26-fn-conversion.md |
| when | 04-names-identifiers.md |
| while | 04-names-identifiers.md |
| while | 12-control-flow.md |
| writeBytesToFile | 18-fn-http.md |
| writeStringToFile | 20-fn-misc-model.md |
| X | 08-datatypes-array.md |
| xDim | 08-datatypes-array.md |
| Y | 08-datatypes-array.md |
| yDim | 08-datatypes-array.md |
| year | 17-fn-datetime.md |
| Z | 08-datatypes-array.md |
