# EventController -- Simulation Control

> Cross-reference: `references/21-fn-misc-simulation.md` for simulation functions (callEvery, seeds, etc.)

## Simulation Lifecycle

Plant Simulation uses **predefined method names** that are automatically called during each simulation phase. These correspond to the buttons on the EventController:

| Phase | Predefined Name | When Called | Typical Use |
|-------|----------------|-------------|-------------|
| Reset | `reset` | When clicking Reset Simulation or calling `EventController.reset` | Delete movables, reset counters, set initial values |
| Init | `init` | First event when simulation starts (after reset, before other events) | Create MUs, schedule timed events, open connections |
| End | `endSim` | When simulation ends (end time reached or event list empty) | Evaluate results, save data, close databases |
| Auto | `autoexec` | After opening the model (if in Class Library) | Start ExperimentManager, auto-run simulations |

## Core Methods

### EventController.start

Starts the simulation run. If the simulation was stopped, it resumes from the current state.

```simtalk
EventController.start
```

Example:

```simtalk
if not EventController.isRunning
   EventController.start
end
```

### EventController.stop

Stops (pauses) the simulation run. The simulation can be resumed with `EventController.start`.

```simtalk
EventController.stop
```

### EventController.reset

Resets the simulation to its initial state. This triggers all `reset` predefined methods, deletes all events from the list of scheduled events, sets simulation time to 0, deletes statistics data, and clears all failures.

```simtalk
EventController.reset
```

Note: `executeIn` calls do not work in reset methods because the EventController deletes every scheduled event during the reset phase. Use `init` methods instead to schedule events.

## Key Properties

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `.simTime` | time | read-only | Current simulation time |
| `.time` | time | read-only | Same as `simTime` (alias) |
| `.isRunning` | boolean | read-only | `true` if simulation is currently running |
| `.Speed` | real | read/write | Simulation speed multiplier |
| `.AbsTimeFormat` | boolean | read/write | If `true`, displays absolute time format |
| `.date` | date | read/write | Simulation start date |
| `.endTime` | time | read/write | Simulation end time |

## Common Patterns

### Reset then Start

```simtalk
EventController.reset
EventController.start
```

### Wait Until Condition

```simtalk
// In an init method:
wait 3600   // suspend for 3600 simulation seconds
// Code here executes after 3600 seconds of simulation time
print "Target time reached:", EventController.simTime
```

### Check Simulation State

```simtalk
if not EventController.isRunning
   EventController.start
end
```

### Reading Simulation Time

```simtalk
print EventController.simTime
```

### Setting Simulation Speed (in a reset method)

```simtalk
EventController.Speed := 60
```

### Converting Simulation Time to a Number

```simtalk
var w: real := time_to_num(EventController.simTime)
```

## Access Paths

- Relative: `EventController`
- Absolute: `root.EventController`
- Programmatic: `currentEventCtl` returns the EventController controlling the current simulation run

See also: `currentEventCtl` in `21-fn-misc-simulation.md`, predefined names (`reset`/`init`/`endSim`) in `04-names-identifiers.md`
