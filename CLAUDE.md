# Ftrace Tool

## Purpose
Facilitates execution and post-processing of the Linux ftrace kernel tracing tool using trace-cmd as the recording interface.

## Language
Bash — start/stop scripts

## Key Files
| File | Purpose |
|------|---------|
| `ftrace-start` | Launches `trace-cmd record` with configurable `--record-opts` (default: `-e all`) |
| `ftrace-stop` | Stops trace-cmd via interrupt signal |
| `rickshaw.json` | Rickshaw integration: endpoint allow/block lists, file deployment, post-process script |
| `workshop.json` | Engine image build: compiles trace-cmd v2.8.3 from source |

## Conventions
- Primary branch is `master`
- Runs as a profiler tool on master/worker/profiler roles, blocked on client/server
- Standard Bash modelines and 4-space indentation
