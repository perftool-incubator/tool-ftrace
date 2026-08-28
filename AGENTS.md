# Tool-ftrace

## Purpose
Crucible tool for executing Linux kernel ftrace tracing via `trace-cmd` as the recording interface during benchmark runs. Collects binary `trace.dat` trace streams for kernel and scheduler diagnostic analysis.

## Languages
- Bash: start/stop wrapper scripts (`ftrace-start`, `ftrace-stop`)

## Key Files
| File | Purpose |
|------|---------|
| `ftrace-start` | Launches `trace-cmd record` with configured `--record-opts` |
| `ftrace-stop` | Sends SIGINT to `trace-cmd` to stop recording and finalize `trace.dat` |
| `rickshaw.json` | Rickshaw integration: collector scripts, blacklist/whitelist |
| `workshop.json` | Engine image build: compiles `trace-cmd` from source |
| `tool-metadata.json` | Machine-readable description and CDM-indexed status (consumed by `crucible tools list`) |
| `multiplex.json` | Parameter validation rules and `defaults` preset for multiplex (mirrors benchmark `multiplex.json`) |

## Configuration
- `--record-opts <options>` — Options passed directly to `trace-cmd record` (default: `-e all`)

## Architecture
- `ftrace-start` — Launches `trace-cmd record $record_opts &` in the background and writes PID to `ftrace-pid.txt`
- `ftrace-stop` — Sends SIGINT to `trace-cmd` PID, allowing `trace-cmd` to flush buffers and finalize the binary `trace.dat` file
- No post-processing script: ftrace is not indexed into CDM (`cdm_indexed: false`); raw binary `trace.dat` is archived for offline trace inspection (e.g. via `trace-cmd report` or KernelShark)

## Conventions
- Primary branch is `master`
- Runs as a profiler tool on master/worker/profiler roles, blocked on client/server
- Standard Bash modelines and 4-space indentation
