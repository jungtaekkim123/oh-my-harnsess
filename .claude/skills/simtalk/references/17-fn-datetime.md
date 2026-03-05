> **Read this when:** Date/time functions: `CalendarWeek`, `CalendarYear`, `sysDate`, `sysTime`, time arithmetic  
> **Skip this when:** String functions (see 16) or conversion functions (see 26)


## Contents

- [Functions for Managing Date and Time](#functions-for-managing-date-and-time)
  - [CalendarWeek](#calendarweek)
  - [CalendarYear](#calendaryear)
  - [day](#day)
  - [dayOfWeek](#dayofweek)
  - [dayOfYear](#dayofyear)
  - [getDate](#getdate)
  - [month](#month)
  - [setDaylightSavingTime](#setdaylightsavingtime)
  - [sysDate](#sysdate)
  - [timeOfDay](#timeofday)
  - [week](#week)
  - [year](#year)

## Functions for Managing Date and Time

### Functions for Managing Date and Time
Plant Simulation uses the date and time
format of the model language you selected.
|  |  |

See also

Date and time format [model settings]
Model language [model settings]

---

### CalendarWeek
Returns the calendar week of the specified date according to DIN 1355/ ISO 8601. 
Remarks

A new week always starts on Monday.
According to DIN 1355/ ISO 8601 the first calendar week of a year is the first
week that contains at least four days of the new year.
Note 
Plant Simulation uses the date and time
format of the model language you selected.
|  |  |

Syntax

```
CalendarWeek(Date:dateTime) → integer
```

Parameter

The parameter Date of data type dateTime designates the date.

Return Value

The return value has the data type integer.

Examples

```
print CalendarWeek(str_to_date("2023/11/21")) // returns 47, model language English
```

```
print CalendarWeek(str_to_date("21.11.2023")) // returns 47, model language German
```

See also

Date and time format [model settings]
Model language [model settings]
week [SimTalk]

---

### CalendarYear
Returns the current year of the Gregorian Calendar. 
Remarks

Plant Simulation uses the date
and time format of the model language you
selected.
|  |  |

Syntax

```
CalendarYear(Value:dateTime) → integer
```

Parameter

The parameter Value of data type dateTime designates the date.

Return Value

The return value has the data type integer.

Example

```
print(CalendarYear(sysdate)) // 2024
print(year(sysdate))         // 124
```

See also

Date and time format [model settings]
Model language [model settings]
year [SimTalk]

---

### day
Extracts the day from a dateTime value.
Remarks

Plant Simulation uses the date
and time format of the model language you
selected.
|  |  |

Syntax

```
day(Date:date) → integer
day(DateTime:dateTime) → integer
```

Parameter

The parameter Date of data type date designates the date.
The parameter DateTime of data type dateTime designates the date and time.

Return Value

The return value has the data type integer.

Examples

```
print day(str_to_date("23/12/24"))            // returns 24, model language English
print day(str_to_dateTime("24/1/1 1:00:00"))  // returns 1
```

```
print day(str_to_date("24.12.23"))            // returns 24, model language German
print day(str_to_dateTime("1.1.24 1:00:00"))  // returns 1
```

See also

Date and time format [model settings]
Model language [model settings]

---

### dayOfWeek
Returns the number of days that has elapsed since the last Sunday.
Remarks

Plant Simulation uses the date
and time format of the model language you
selected.
|  |  |

Syntax

```
dayOfWeek(Date:date) → integer
dayOfWeek(DateTime:dateTime) → integer
```

Parameter

The parameter Date of data type date designates the date.
The parameter DateTime of data type dateTime designates the date and time.

Return Value

The return value has the data type integer.
| Day of Week | Return Value || Monday | 1 || Tuesday | 2 || Wednesday | 3 || Thursday | 4 || Friday | 5 || Saturday | 6 || Sunday | 0 |

Examples

```
var d: date; var dt: dateTime
dt := str_to_dateTime("24/1/3 1:20:30")
d := str_to_date("24/1/1")
print dayOfWeek(dt)  // returns 3, model language English
print dayOfWeek(d)   // returns 1
```

```
var d: date; var dt: dateTime
dt := str_to_dateTime("3.1.24 1:20:30")
d := str_to_date("1.1.24")
print dayOfWeek(dt)  // returns 3, model language German
print dayOfWeek(d)   // returns 1
```

See also

Date and time format [model settings]
Model language [model settings]

---

### dayOfYear
Returns the number of days that has elapsed since January first.
Remarks

Plant Simulation uses the date
and time format of the model language you
selected.
|  |  |

Syntax

```
dayOfYear(Date:date) → integer
dayOfYear(DateTime:dateTime) → integer
```

Parameter

The parameter Date of data type date designates the date.
The parameter DateTime of data type dateTime designates the date and time.

Return Value

The return value has the data type integer.

Examples

```
var d: date; var dt: dateTime
dt := str_to_dateTime("23/12/31 23:59:59")
d := str_to_date("24/1/1")
print dayOfYear(dt)  // returns 364, model language English
print dayOfYear(d)   // returns 0
```

```
var d: date; var dt: dateTime
dt := str_to_dateTime("31.12.23 23:59:59")
d := str_to_date("1.1.24")
print dayOfYear(dt)  // returns 364, model language German
print dayOfYear(d)   // returns 0
```

See also

Date and time format [model settings]
Model language [model settings]

---

### getDate
Returns the date of a value containing date and time.
Remarks

Plant Simulation uses the date
and time format of the model language you
selected.
|  |  |

Syntax

```
getDate(Date/Datetime:dateTime)
```

Parameter

The parameter Date or DateTime of data type date or dateTime
designates the value containing date and time.

Examples

```
var d: date; var dt: dateTime
dt := str_to_dateTime("2023/11/12 11:30:00")
d := getDate(dt)
print d // returns 2023/11/11, model language English
```

```
var d: date; var dt: dateTime
dt := str_to_dateTime("12.11.2023 11:30:00")
d := getDate(dt)
print d // returns 12.11.2023, model language German
```

See also

Date and time format [model settings]
Model language [model settings]

---

### month
Returns the month of a value containing date and time.
Remarks

Plant Simulation uses the date
and time format of the model language you
selected.
|  |  |

Syntax

```
month(Date:date) → integer
month(DateTime:dateTime) → integer
```

Parameter

The parameter Date of data type date designates the date.
The parameter DateTime of data type dateTime designates the date.

Return Value

The return value has the data type integer.

Example

```
print month(str_to_date("24.12.23"))             // returns 12
print month(str_to_dateTime("1.1.24 1:00:00"))   // returns 1
```

See also

Date and time format [model settings]
Model language [model settings]

---

### setDaylightSavingTime
Sets the beginning and the end of daylight saving
time. 

Syntax

```
setDaylightSavingTime(BeginningAndEndOfDaylightSavingTime:string)
```

Parameter

The parameter BeginningAndEndOfDaylightSavingTime of data type string consists
of the following components. 
The first set of four numbers sets the beginning of daylight saving time: 

monthOfYear

weekOfMonth

dayInWeek

hour

The second set of four numbers sets the end of daylight saving time:

monthOfYear

weekOfMonth

dayInWeek

hour

To deactivate daylight saving time, you can specify an empty string 
`""`
. 

Example

```
setDaylightSavingTime("4,3,3,12,10,4,3,3")
setDaylightSavingTime("") // no daylight saving time
```

See also

Daylight saving time [preferences]

---

### sysDate
    Returns the current system time of the computer on which Plant
            Simulation runs.
        Title
            
            Function
        
        Syntax
            
```
sysDate → dateTime
```

        
        Return Value
            
            The return value has the data type dateTime. 
            The returned value has a resolution of 1 millisecond.
        
        Example
            
```
print sysDate                     // current time
EventController.date := sysDate   // apply to simulation
```

        
        See also
            
            getHighResolutionClock [SimTalk]
            processTime [SimTalk]

---

### timeOfDay
Returns the time portion of a value containing date and time.
Remarks

Plant Simulation uses the date
and time format of the model language you
selected.
|  |  |

Syntax

```
timeOfDay(DateTime:dateTime) → time
```

Parameter

The parameter DateTime of data type dateTime designates the value containing
date and time.

Return Value

The return value has the data type time.

Examples

```
var EclipseOfTheSun: datetime; var t: time; var d: date
EclipseOfTheSun := str_to_datetime("11.08.1999 11:30:00")
t := timeOfDay(EclipseOfTheSun)
print t // 11:30:00.0000
d := getDate(EclipseOfTheSun)
print d // returns 11.08.1999, model language English
```

```
var Sonnenfinsternis: datetime; var t: time; var d: date
Sonnenfinsternis := str_to_datetime("11.8.99 11:30:00")
t := timeOfDay(Sonnenfinsternis)
print t // 11:30:00.0000
d := getDate(Sonnenfinsternis)
print d // returns 11.08.1999, model language German
```

See also

Date and time format [model settings]
Model language [model settings]

---

### week
Returns the number of weeks that started since January first of a year. 
Remarks

The week always begins on a Monday. This week does not correspond to the calendar
week.

Syntax

```
week(Date:date) → integer
week(DateTime:dateTime) → integer
```

Parameter

The parameter Date of data type date designates the date.
The parameter DateTime of data type dateTime designates the date and the
time.

Return Value

The return value has the data type integer.

Example

```
print week(str_to_date("1.1.24"))             // returns 1
print week(str_to_date("1.2.24"))             // returns 5
print week(str_to_dateTime("1.1.24 1:00:00")) // returns 1
```

See also

CalendarWeek [SimTalk]

---

### year
Computes the number of years elapsed since the year 1900.
Remarks

Plant Simulation uses the date
and time format of the model language you
selected.
|  |  |

Syntax

```
year(Date:date) → integer
year(DateTime:dateTime) → integer
```

Parameter

The parameter Date of data type date designates the date.
The parameter DateTime of data type dateTime designates the date and the
time.

Return Value

The return value has the data type integer.

Examples

```
print year(str_to_date("1.1.2024"))           // returns 124
print year(str_to_dateTime("1.1.20 1:00:00")) // returns 120
```

```
print(CalendarYear(sysdate)) // 2024
print(year(sysdate))         // 124
```

See also

Date and time format [model settings]
Model language [model settings]
CalendarYear [SimTalk]

---
