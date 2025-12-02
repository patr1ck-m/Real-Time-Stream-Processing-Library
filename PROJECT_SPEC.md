# Real-Time Stream Processing Library

This project implements a modular, effect-driven library for processing real-time data streams from e.x. sensors.
It simulates continuous sensor input, aggregates the data over time windows, detects anomalies using multiple strategies, and logs results and alerts.  
The system is highly adaptible: all core components (data sources, aggregators, detection strategies, loggers) are exposed as effects and handlers, allowing users to plug in their own logic or use the provided library handlers.  
The library provides sample inputs with theoretical distribution generators for testing. These input streams can simply be exchanged by replacing the input stream generator (pull stream provider).


## Must-have

- Data input (stream)
  - Simulated data using simple distributions (uniform, normal, exponential, ...)
- Window based aggregation
  - Input is a pull stream and output is a push stream (aggregated by parameters)
  - Support `min`, `max`, `mean`, `median`
- Analysis and Detection of out of scope values and alert
  - Output is an alert stream (alert events are called whenever a value is out of scope) and an additional stream with tagged events (out of scope or not with a score value how much it is out of bounds for logging purpose)
  - Simple `min - max` scope handler
  - `z-score` handler (bit more advanced because mean and standard derivation over whole stream is needed (without storing all datapoints because of performance reasons))
- Logging
  - handling the events from above
  - console logging and/or file logging (CSV)
- Example setup using the effects and handlers from the library with simulated data


## Can-have

- Live tracking of mean and standard derivation inside console
- Input stream for computer resources (CPU, RAM usage) for an example with real world sensor data
- Example with real sensor data (CPU/RAM)


## Will-not-have

- GUI (no graphical interface, results can be plotted using external tools and the output csv)


## Effects and Handlers

- Since everything works on streams, the whole application works with effects and handlers
- `Alert` effect
- `TaggedEvent` as output event of the detection handler
- The whole application is more like a library with effects where the user can switch out handlers (library provided handlers and own handlers)

## FFI and Libraries

<!-- rule "Keep FFI surface minimal" applies:
     implement as much as possible in Effekt directly and keep FFI bindings small. -->

- CSV library for logging?
- Request current CPU usage and RAM usage from OS?