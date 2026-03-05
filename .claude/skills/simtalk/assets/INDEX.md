# SimTalk 2.0 Code Examples

## Template Router

| Category | File | Use When | Key Patterns |
|----------|------|----------|--------------|
| Simulation Control | `simulation-control/example.md` | Init/reset/endSim lifecycle, warm-up, EventController, speed | `init`, `reset`, `endSim`, `EventController.*`, `processTime` |
| File I/O | `file-io/example.md` | Reading/writing files, CSV parsing, path handling | `readStringFromFile`, `writeStringToFile`, `copyFile`, `existsFile` |
| Data Structures | `data-structures/example.md` | Arrays, 2D arrays, JSON, tables, nested lists | `var x: type[]`, `.append`, `.sort`, `json`, `copyFromTable` |
| String Processing | `string-processing/example.md` | String manipulation, search/replace, regex, formatting | `strLen`, `strCopy`, `splitString`, `regex_search`, `regex_replace` |
| HTTP Client | `http-client/example.md` | REST API calls, GET/POST, JSON payloads, headers | `httpGetRequest`, `httpPostRequest`, `httpCreateURL` |
| MU Handling | `mu-handling/example.md` | Moving units, routing, attributes, creation | `@.move`, `@.name`, `.create`, `MU.move` |
| Event Scheduling | `event-scheduling/example.md` | Timers, periodic calls, delayed execution, waiting | `callEvery`, `waituntil`, `executeIn`, `wait`, `processTime` |
| Migration (1.0 -> 2.0) | `migration-examples/example.md` | Converting old SimTalk 1.0 code to 2.0 syntax | `var` vs `dim`, `for..next` vs `loop`, `:=` operators |

## How to Use These Templates

- **Adapt** variable names, paths, and logic to the user's model
- **Cross-reference** with `references/` docs for parameter details and full signatures
- Templates show **common patterns**; combine as needed for complex use cases
- All examples use **SimTalk 2.0** syntax (new notation)
- When in doubt, check the migration guide for syntax differences
