---
name: simtalk
description: "SimTalk 2.0 reference for Siemens Plant Simulation. Use for SimTalk programming questions, function lookup, data type reference, code examples, and SimTalk 1.0 to 2.0 migration. Trigger on: \"SimTalk\", \"Plant Simulation\", \"PlantSim\", \"simtalk code\", \"SimTalk function\", \"SimTalk migration\", \"SimTalk 2.0\"."
---

# SimTalk 2.0 Reference Guide

Use for SimTalk 2.0 syntax, function lookup, data type reference, code examples, and SimTalk 1.0 → 2.0 migration in Siemens Plant Simulation.

## Rules

1. Apply one-page-at-a-time: open one reference page, extract decision-relevant facts, then return to the router before opening the next page.
2. Prefer **Language Basics** (01–06) for syntax questions; **Data Types** (07–10) for type details; **Syntax** (11–12) for operators/control flow; **Functions** (13–27) for API reference.
3. Always check `references/INDEX.md` Part 2 (Function → File Lookup) when looking up a specific function by name.
4. Generate **SimTalk 2.0 syntax only**. For 1.0 vs 2.0 comparison, refer to `references/02-migration.md`.
5. When migration questions arise, always open `references/02-migration.md` first.
6. For code examples and implementation patterns, check `assets/INDEX.md` first to find the right template, then open the specific asset file.

## Minimal Load Order

1. Use the **Depth 0** table below to identify the topic category.
2. Open `references/INDEX.md` to find the function's source file (Part 2: Function → File Lookup).
3. Open only one reference file unless a concrete gap remains.
4. For migration questions, start with `references/02-migration.md`.
5. For code examples and patterns, check `assets/INDEX.md` to find the right template.

## Reference Documents — Depth 0: Topic Router

| # | Category | File | Description | When to open |
|---|----------|------|-------------|--------------|
| 01 | **Language Basics** | 01-overview.md | SimTalk intro, quick tour, simple values, control flow | First contact, "what is SimTalk", quick syntax overview |
| 02 | **Language Basics** | 02-migration.md | SimTalk 2.0 vs 1.0 comparison + outdated names table | Migration, outdated function names, converting old code |
| 03 | **Language Basics** | 03-general-access.md | General access to simulation objects | Accessing object attributes, methods, read-only attributes |
| 04 | **Language Basics** | 04-names-identifiers.md | Identifiers, keywords, reserved words | Naming rules, keyword list, reserved word conflicts |
| 05 | **Language Basics** | 05-names-paths.md | Paths, namespaces, qualified names | Object paths, relative/absolute references, `basis` keyword |
| 06 | **Language Basics** | 06-constants-variables.md | Constants, variables, parameters, `var`, `param`, `const` | Variable declaration, parameter passing, `byref`, defaults |
| 07 | **Data Types** | 07-datatypes-primitive.md | Scalar types (acceleration, boolean, date, integer, length, real, speed, string, time, weight, etc.) | Primitive type ranges, units, type behavior |
| 08 | **Data Types** | 08-datatypes-array.md | Array type + all array methods | Array creation, indexing, `append`, `contains`, `dim`, `sort`, `copy*` |
| 09 | **Data Types** | 09-datatypes-json.md | JSON type + methods | JSON creation, parsing, `asString`, `contains`, `copy*` |
| 10 | **Data Types** | 10-datatypes-collections.md | List, Queue, Stack, Table | Collection types, `create`, nested lists, FIFO/LIFO |
| 11 | **Syntax** | 11-operators.md | Operators and expressions | Arithmetic, comparison, logical, `~=`, `mod`, `div`, `&` ref operator |
| 12 | **Syntax** | 12-control-flow.md | Control flow statements | `if`, `for`, `while`, `repeat`, `switch`, `waituntil`, `try`/`catch` |
| 13 | **Functions** | 13-fn-os.md | OS functions | File I/O, clipboard, folder browsing, `copyFile`, `deleteFile` |
| 14 | **Functions** | 14-fn-math.md | Math functions | `abs`, `ceil`, `floor`, `sqrt`, trig, random distributions |
| 15 | **Functions** | 15-fn-bits.md | Bit manipulation functions | `BitAND`, `BitOR`, `BitXOR`, `BitSet`, `BitTest`, `BitShift` |
| 16 | **Functions** | 16-fn-strings.md | String functions | `strlen`, `substr`, `strSearchAndReplace`, regex, formatting |
| 17 | **Functions** | 17-fn-datetime.md | Date/time functions | `CalendarWeek`, `CalendarYear`, `sysDate`, time arithmetic |
| 18 | **Functions** | 18-fn-http.md | HTTP functions | HTTP requests, REST API calls, web service integration |
| 19 | **Functions** | 19-fn-misc-app.md | App/environment functions | `applicationHome`, `applicationVersion`, license, environment |
| 20 | **Functions** | 20-fn-misc-model.md | Model/file functions | `closeModel`, `openModel`, `saveModel`, model file operations |
| 21 | **Functions** | 21-fn-misc-simulation.md | Simulation control functions | `callEvery`, `startSim`, `stopSim`, `resetSim`, event scheduling |
| 22 | **Functions** | 22-fn-misc-ui.md | UI/dialog functions | `clearConsole`, `openConsole`, `closeAllWindows`, dialog, HTML windows |
| 23 | **Functions** | 23-fn-misc-util.md | Utility/crypto functions | `animation`, `checkID`, `computeSHA*`, `createCombinations`, geometry |
| 24 | **Functions** | 24-fn-datatype-query.md | Data type query functions | Type checking, `is_*` functions, type introspection |
| 25 | **Functions** | 25-fn-io.md | Input/output functions | `print`, `beep`, `bell`, console I/O |
| 26 | **Functions** | 26-fn-conversion.md | Conversion functions | `*_to_num`, `*_to_str`, `num_to_*`, `str_to_*`, unit conversion |
| 27 | **Functions** | 27-fn-debug.md | Debug functions | Breakpoints, tracing, debug output, method debugging |

> Depth 1 file listings and function signatures: `references/INDEX.md`

---

## Misc Functions Sub-Router

Since miscellaneous functions are split across 5 files, use this table for precise routing:

| Function Category | File | Example Functions | When to open |
|-------------------|------|-------------------|--------------|
| App / Environment | 19-fn-misc-app.md | `applicationHome`, `applicationVersion`, `checkForLicense`, `createLicenseFile` | Application info, licensing, version checks |
| Model / File Ops | 20-fn-misc-model.md | `closeModel`, `openModel`, `saveModel`, `connectAutomatically` | Opening/closing/saving models, file management |
| Simulation Control | 21-fn-misc-simulation.md | `callEvery`, `startSim`, `stopSim`, `resetSim`, event scheduling | Running simulations, event control, reset |
| UI / Dialog | 22-fn-misc-ui.md | `clearConsole`, `openConsole`, `closeAllWindows`, `closeHTMLWindow`, `clearLogFile` | Console, windows, dialogs, HTML UI |
| Utility / Crypto | 23-fn-misc-util.md | `animation`, `checkID`, `computeSHA1Hash`, `calcBrakingDistance`, `createCombinations` | Hashing, geometry, animation toggle, ID validation |

---

## Data Types Quick Reference

| Type | Category | Reference |
|------|----------|-----------|
| acceleration, length, speed, weight | Physical units (scalar) | 07-datatypes-primitive.md |
| boolean, integer, real | Numeric primitives | 07-datatypes-primitive.md |
| string | Text | 07-datatypes-primitive.md |
| date, dateTime, time | Temporal | 07-datatypes-primitive.md |
| object, any | Reference types | 07-datatypes-primitive.md |
| array (integer[], real[], string[], ...) | Ordered indexed collection | 08-datatypes-array.md |
| json | JSON object / array | 09-datatypes-json.md |
| list | Ordered rows (local DataList) | 10-datatypes-collections.md |
| queue | FIFO collection | 10-datatypes-collections.md |
| stack | LIFO collection | 10-datatypes-collections.md |
| table | Tabular data (local DataTable) | 10-datatypes-collections.md |

---

## SimTalk 2.0 — Syntax Quick Reference

| Feature | SimTalk 2.0 Syntax |
|---------|-------------------|
| Variable declaration | `var s: string` |
| If statement | `if a > 3 ... end` |
| For loop | `for var i := 1 to 10 ... next` |
| While loop | `while a < 10 ... end` |
| Switch/case | `switch a case 1 ... end` |
| Compound assign | `x += y`, `x -= y`, `x *= y` |
| About-equal operator | `~=`, `<~=`, `>~=` |
| Modulo operator | `mod` |
| Integer division | `div` |
| Reference operator | `&` (e.g., `.Models.Model.&Method`) |
| Semicolons | not required |
| Empty method body | (just leave empty) |
| Parameter declaration | `param v1, v2: integer` |
| Return type | `-> boolean` after params |
| Create nested list | `createNestedList` |

> For 1.0 → 2.0 migration comparison, see `references/02-migration.md`.

---

## Code Example Templates (Assets)

> Open `assets/INDEX.md` first to find the right example template.

| Category | Asset File | Use When |
|----------|-----------|----------|
| Simulation Control | assets/simulation-control/example.md | Init/reset/end methods, event scheduling, warm-up handling |
| File I/O | assets/file-io/example.md | Reading/writing files, CSV parsing, path handling |
| Data Structures | assets/data-structures/example.md | Arrays, JSON, tables, lists, createNestedList |
| String Processing | assets/string-processing/example.md | Text manipulation, parsing, regex, formatting |
| HTTP Client | assets/http-client/example.md | REST API calls, JSON requests/responses, headers |
| MU Handling | assets/mu-handling/example.md | Moving MUs, routing logic, MU attributes |
| Event Scheduling | assets/event-scheduling/example.md | callEvery, delayed execution, periodic tasks |
| Migration | assets/migration-examples/example.md | Converting SimTalk 1.0 → 2.0 code |

### Asset Use Rules

1. **Always check `assets/INDEX.md` first** — it has a routing table to find the right template.
2. **Adapt, don't copy** — templates show patterns; adjust variable names, paths, and logic to the user's model.
3. **Cross-reference with reference docs** — assets show "how", reference docs show "what" (parameter details, edge cases).
4. **Prefer assets for "how do I..." questions** — when the user asks for a code example or pattern, check assets before writing from scratch.
