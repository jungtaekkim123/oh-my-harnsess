> **Read this when:** JSON type, JSON creation, parsing, `asString`, `contains`, `copy*`, JSON methods  
> **Skip this when:** Array methods (see 08) or primitive types (see 07)


## Contents

- [JSON](#json)
- [Elements of Data Type Object in JSON Variables](#elements-of-data-type-object-in-json-variables)
- [Methods and Attributes of JSON](#methods-and-attributes-of-json)
- [asString - JSON](#asstring---json)
- [contains - JSON](#contains---json)
- [copy - JSON](#copy---json)
- [copyToTableColumn - JSON](#copytotablecolumn---json)
- [copyToTableRow - JSON](#copytotablerow---json)
- [delete - JSON](#delete---json)
- [Dim - JSON](#dim---json)
- [getOrCreateJSON](#getorcreatejson)
- [parse](#parse)
- [unshareAndDelete](#unshareanddelete)

## JSON
A local variable of data type JSON can hold values in the JSON
data format. Remarks

JSON, standing for JavaScript Object Notation, is a standardized data format that can be used for exchanging
data between applications. Many web applications and web services expect their input data and return
their results in JSON format.
JSON data is structured data that can be nested arbitrarily. The data consists of
one, none, or several elements. Each element is a name-value-pair. The name can contain spaces and
special characters. 
Note 
Names in JSON are case-sensitive. 

The values of a name-value-pair can have the following data types:

Integer: A signed integer number

Real: A floating point number

Boolean: true or false

String: A string within quotation marks, for example

`"my string"`

Array: An ordered list of values within brackets 
```
[]
```
 and separated by commas

JSON: An unordered list of elements (name-value-pairs)
within braces 
```
{}
```
 and separated by commas

Void: An empty value that JSON displays as

`null`

```
var person: json
person["Name"] := "Robert"
person["Age"] := 42
person["Personnel No"] := "007-1234-55"
```

```
var person
person["age"] := 30
person["age"] += 1  // Congratulations :-)
```

You can also address a name-value-pair via an integer
index. This way you can iterate across all name-value-pairs. You always have to either
select the name or the value from such a name-value-pair by appending 
`.Name`
 or 
`.Value`
 respectively.
```
var j: json
    j["color"] := "red"
    j["shape"] := "triangle"
    for var i := 1 to j.dim
      print j[i].Name, " ", j[i].Value
    next
```

For more information about JSON, consult Wikipedia https://en.wikipedia.org/wiki/JSON.

See also

Elements of Data Type Object in JSON Variables
Methods and Attributes of JSON
isJson [SimTalk]

---

## Elements of Data Type Object in JSON Variables
```
var j: json
j["o"] := MyStation    -- element "o" is of data type object
j["o"].Label := "ABC"  -- assigns a label to the object MyStation
```
Note 
JSON, standing for JavaScript Object Notation, is a standardized data format that can be used for exchanging
data between applications. 
The element type object is an extension
that is not defined within the JSON standard and which only Plant
Simulation provides. When JSON data is converted into a string, for
example to send it via an interface, all object elements will be written as a string with their absolute path to the object. This is necessary so
that the created string is a standard-conform representation which other
applications can process.
```
var json1, json2: json
json1["o"] := MyStation          -- element "o" is of data type object
var s : string := to_str(json1)  -- convert data into a string
json2.parse(s)                   -- element "o" is of data type string
```

---

## Methods and Attributes of JSON
You can also address a name-value-pair via an integer
index. This way you can iterate across all name-value-pairs. 
You always have to either select the name or the value from such a name-value-pair by appending 
`.Name`
 or 
`.Value`
 respectively.
```
var j: json
    j["color"] := "red"
    j["shape"] := "triangle"
    for var i := 1 to j.dim
      print j[i].Name, " ", j[i].Value
    next
```

---

## asString - JSON
Returns the string representation of the JSON object designated by <json>. Remarks
You can, for example, send the returned string to a Web-server. The method parse can re-transform such a string into the JSON format.

Syntax

```
<json>.asString([MultiLine:boolean:=true]) -> string
```

Parameter

The optional parameter MultiLine of data type boolean sets if the method
returns the result with line breaks and indenting spaces (
`true`
) or without them
(
`false`
).
Default Value of the Parameter
The default value is true.

Return Value

The return value has the data type string.

Example

```
var j: json
j["Name"] := "Tom"
j["Age"] := 32
var s: string := j.asString(false)
```

See also

parse [SimTalk]

---

## contains - JSON
   Returns if the JSON object designated by <json> contains a name-value-pair with
      the passed name (true) or not (false).
      
      Syntax
         
```
<json>.contains(Name:string) -> boolean
```

      
      Parameter
         
         The parameter Name of data type string designates the name which you
            would like to know if it is contained in the JSON object.
      
      Return Value
         
         The return value has the data type boolean.
      
      Example
         
```
var j: json
j["Body color"] := "blue"
if a.contains("Body color")
   print "This code will always be reached."
end
```

---

## copy - JSON
Returns a copy of the JSON object designated by <json>. 

Syntax

```
<json>.copy -> json
```

Return Value

The return value has the data type json.

Examples

```
var Person1, Person2: json
Person2 := Person1          -- Person1 and Person2 reference the same JSON object
Person2["Name"] := "Alice"  -- also changes Person1["Name"]
print Person1["Name"]       -- returns Alice 

Person2 := Person1.copy     -- Person1 and Person2 now are different JSON objects
Person2["Name"] := "Bob"    -- does not change Person1["Name"]
print Person1["Name"]       -- returns Alice 
```

```
var Person, Job: json
Job["Description"] := "engineer"
Person["Job"] := Job.copy    -- inserts a copy of Job in Person 
Job["Company"] := "Siemens"  -- does not change Person["Job"]
```

---

## copyToTableColumn - JSON
Copies the contents of the json array designated by <json
array> to the specified column of a table. 

Syntax

```
<json array>.copyToTableColumn(TargetTable:table, Column:integer)
```

Parameters

The parameter TargetTable of data type table designates the table to which you
would like to copy data.

The parameter Column of data type integer designates the column into which you
would like to paste data.

Example

```
var j:json
j["a"] := ["hello", "world", 42]
j["a"].copyToTableColumn(DataTable, 2) 
-- copies the three array elements into the first 
-- three cells of the second column of the table
```

---

## copyToTableRow - JSON
Copies the contents of the json array designated by <json
array> to the specified row of a table. 

Syntax

```
<json array>.copyToTableRow(TargetTable:table, Row:integer)
```

Parameters

The parameter TargetTable of data type table designates the table to which you
would like to copy data.

The parameter Row of data type integer designates the row into which you would
like to paste data.

Example

```
var j:json
j["a"] := ["hello", "world", 42]
j["a"].copyToTableRow(DataTable, 2) 
-- copies the three array elements into the first 
-- three cells of the second row of the table
```

---

## delete - JSON
   The method delete without parameter deletes the entire
      contents of the JSON object designated by <json>. The method delete with parameter deletes the specified name-value pair. 
      
      Syntax
         
```
<json>.delete([Name:string]) -> boolean
```

      
      Parameter
         
         Specify the optional parameter Name of data
            type string to delete the name-value-pair with the specified
            name.
      
      Return Value
         
         The return value has the data type boolean.
         The return value is true if the JSON object did contain the name before.
         The return value is false if it did not contain the name before.
      
      Example
         
```
var person: json
person["Name"] := "Jason"

if person.delete("name")
   print "This code will never be reached."
elseif person.delete("Name")
   print "This code will always be reached."
end
```

---

## Dim - JSON
   Returns the number of name-value-pairs which the JSON object designated by
      <json> contains.
      
      Syntax
         
```
<json>.Dim -> integer
```

      
      Return Value
         
         The return value has the data type integer.
      
      Example
         
```
param s: string
var j: json
j.parse(s)
if j.Dim = 0
   print "No data available."
end
```

---

## getOrCreateJSON
Returns a reference to the empty JSON object designated by <json>.Remarks
If the JSON object does not contain a name-value-pair with the specified name yet in the variable, Plant Simulation creates a new name-value-pair and sets an empty JSON object as value. The method getOrCreateJSON returns a reference to this empty JSON object.If the JSON object designated already contains a name-value-pair with the specified name yet in the variable and the value has the data type json, the method getOrCreateJSON returns a reference to the contained value. If the value has another data type than json, Plant Simulation shows an error.

Syntax

```
<jsonVariable>.getOrCreateJSON(Name:string) -> json
```

Parameter

The parameter Name of data type string designates the name of the
name-value-pair.

Return Value

The return value has the data type json.
The return value is a reference to the empty JSON object.
The return value is a reference to the value contained in the JSON object.

Example

```
-- source code of Method1:
var JsonObj: json

var ColorInfo := JsonObj.getOrCreateJSON("ColorInfo")  
-- JSON-subobject named "ColorInfo" will be created and returned
ColorInfo["color"] := "red"
ColorInfo["NumberChangesColor"] += 1

Method2(JsonObj)

-- source code of Method2:
param JsonObj: json

var ColorInfo := JsonObj.getOrCreateJSON("ColorInfo")  
-- existing JSON-subobject will be returned
ColorInfo["color"] := "green"
ColorInfo["NumberChangesColor"] += 1   
-- the value will be increased to 2
```

---

## parse
Parses the text passed by the parameter Data and returns the
parsed value. 
Remarks

The text usually starts with an opening curly brace { and specifies a complex JSON object, although the value can also be a single value of
data type integer, real, boolean, or an array.

Syntax

```
<json>.parse(Data:string) -> any
```

If the value is a JSON object, this value will also be assigned to the variable <json>,
otherwise the variable <json> will be set to an empty JSON object.

Parameter

The parameter Data of data type string designates the text to be parsed.

Return Value

The return value has the data type any.
Examples
```
var j: json

var value1 := j.parse("{ \"count\": 123 }")
// value1: json = { "count": 123 }
// j     : json = { "count": 123 }
```
```
var value2 := j.parse("123")
// value2: integer = 123
// j     : json = {}
```

```
var arr := j.parse("[3.141, 100, true]")
// arr   : any[] = [3.141, 100, true]
// j     : json = {}
```
```
var arr := j.parse("[3.141, 100, true]")
// arr   : any[] = [3.141, 100, true]
// j     : json = {}
```

See also

asString [SimTalk] - JSON

---

## unshareAndDelete
Unshares the reference to the JSON object designated by <json> and
assigns an empty JSON object to the local variable or to the user-defined attribute. 

Syntax

`<json>.unshareAndDelete`

Example

```
var person1, person2 : json
person2 := person1          -- person1 and person2 reference the same JSON object
person2["Name"] := "Alice"  -- also changes person1["Name"]
person2.unshareAndDelete    -- person2 is an empty JSON object
person2["Name"] := "Bob"    -- only changes person2["Bob"]
```
