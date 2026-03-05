> **Read this when:** List, Queue, Stack, Table types, `create`, `createNestedList`, FIFO/LIFO patterns  
> **Skip this when:** Array methods (see 08) or JSON (see 09)

## List
A local variable of data type list shares
its built-in properties with the object DataList. Remarks
Note the difference between the object DataList, which you insert into your model, and the data type list. You can create user-defined attributes and local/global variables of data type list that are part
of another object and thus are not an object of their own and do not have their own icon. For this reason variables and attributes of data type list do not recognize all of the attributes, read-only attributes, and methods of the object DataList, such as Location or existsIcon. All other methods, especially for read and write access, apply to both the DataList and to variables and attributes of data type list.Note 
Before accessing the data type list for the first time, you have to create the local variable with the method create or you have to assign a value to the variable. 

Example

```
var l: list[string]
l.create
l.insert(1,"Hello")
```

See also

Instantiating Local Lists and Tables
isListRange [SimTalk]
isList [SimTalk]

---

## Queue
A local variable of data type queue
shares some of the built-in properties of the object DataQueue. Remarks
Note the difference between the object DataQueue, which you insert into your model, and the data type queue. You can create user-defined attributes and local/global variables of data type queue that are
part of another object and thus are not an object of their own and do not have their own icon. For this reason variables and attributes of data type queue do not recognize all of the attributes, read-only attributes, and methods of the object DataQueue, such as Location or existsIcon. All other methods, especially for read and write access, apply to both the DataQueue and to variables and attributes of data type queue. Note 
Before accessing the data type queue for the first time, you have to create the local variable with the method create or you have to assign a value to the variable. 

Example

```
var q: queue[string]
q.create
q.push("Hello")
```

See also

Instantiating Local Lists and Tables
isQueue [SimTalk]

---

## Stack
A local variable of data type stack
shares some of the built-in properties of the object DataStack. Remarks
Note the difference between the object DataStack, which you insert into your model, and the data type stack. You can create user-defined attributes and local/global variables of data type stack that are
part of another object and thus are not an object of their own and do not have their own icon. For this reason variables and attributes of data type stack do not recognize all of the attributes, read-only attributes, and methods of the object DataStack, such as Location or existsIcon. All other methods, especially for read and write access, apply to both the DataStack and to variables and attributes of data type stack. Note 
Before accessing the data type list for the first time, you have to create the local variable with the method create or you have to assign a value to the variable. 

Example

```
var s: stack[string]
s.create
s.push("Hello")
```

See also

Instantiating Local Lists and Tables
isStack [SimTalk]

---

## Table
A local variable of data type table
shares some of the built-in properties of the object DataTable. Remarks
Note the difference between the object DataTable that you can insert into models and the data type table. You can create user-defined attributes and local/global variables of data type table that are
part of another object and thus are not an object of their own and do not have their own icon. For this reason variables and attributes of data type table do not recognize all of the attributes, read-only attributes, and methods of the object DataTable, for example Location or existsIcon. All other methods, especially for read and write access apply to both the object DataTable and to variables and attributes of data type table. Note 
Before accessing the data type table for the first time, you have to create the local variable with the method create or you have to assign a value to the variable. 

Examples

```
var OrderList: table[string,real]
OrderList.create
OrderList[1,1] := "Cans"
OrderList[2,1] := 3000.0
```

```
var myWaitingTimesTable: table
MyAssembly.statWaitingTimeTable(myWaitingTimesTable)
```

See also

Instantiating Local Lists and Tables
isTable [SimTalk]

---

### Instantiating Local Lists and Tables
  create and createNestedList for instantiating them.

---

### create - local list
Creates an empty data structure without contents in the local
variable designated by <Local-variable>. 
Remarks

The method create applies to local
variables of data type list, queue, stack, and table. 

Syntax

```
<Local-variable>.create([NumberOfRows:integer])
```

Parameter

The optional parameter NumberOfRows of data type integer designates the number
of rows in the list or table.

Example

```
var orderlist: table[string,real]
orderlist.create
orderlist[1,1] := "cans"
orderlist[2,1] := 3000.0
orderlist.forget    // destroys the table
orderlist.create(4) // recreates the table with 4 rows
```

See also

Data Types in Local Variables

---

### createNestedList - local variable
Creates a new sublist or subtable in the local variable
designated by <local-list> or by <local-table>. Remarks
The local variable has to be of data type list, queue, stack, or table. The data type of the column of this list or table has to be of data type list, stack, queue, or table as well.

Syntax

```
<Local-list>.createNestedList(Column:integer, Row:integer[, Name:string]) → list
<Local-table>.createNestedList(Column:integer, Row:integer[, Name:string]) → list
```

Parameters

The parameter Column of data type integer designates the column of the
cell.

The parameter Row of data type integer designates the row of the cell.

The optional parameter Name of data type string designates the name of the sublist or subtable to be created. 

Note 
This method also applies to sublists and subtables!

Return Value

The return value has the data type list.
The return value is the nested list (DataList, DataQueue, DataStack,
or DataTable) that was created.

Examples

```
var t: table[table]
t.create                // creates a table
t.createNestedList(1,1) // creates a subtable
t[1,1][2,3] := "Hello world" // writes Hello world into the nested table
```

The code inserts a subtable into cell 1 of the our table. It then inserts Hello world into the
cell at the position 2,3.

```
var subtable: table
MyDataTable.createNestedList(2,3) // creates a subtable
subtable := MyDataTable[2,3]
subtable.createNestedList(1,1)    // creates a subtable within a subtable
subtable[1,1][4,4] := "Hello world"
```

See also

setCommonFormat [SimTalk]
Activating and Deactivating Common Format
createNestedList [SimTalk] - DataQueue
createNestedList [SimTalk] - DataList
createNestedList [SimTalk] - DataTable
