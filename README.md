# tool-ftrace

Facilitates execution and post-processing of the Linux ftrace kernel tracing tool for the [crucible](https://github.com/perftool-incubator/crucible) performance testing framework, using [trace-cmd](https://www.trace-cmd.org/) as the recording interface.

## Configuration

The start script accepts one parameter:
- `--record-opts <opts>` — Options passed to `trace-cmd record` (default: `-e all`)

## Integration

Ftrace runs as a profiler tool on endpoint nodes. It is allowed on profiler, master, and worker collector roles but blocked on client and server roles. Collection is stopped by sending an interrupt signal to the trace-cmd process.
