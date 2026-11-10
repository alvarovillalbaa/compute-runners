# compute-runners specification

Last updated: 2026-11-10

Status: planned. All runtime capabilities below remain planned.

## Responsibility

Local/cluster/provider execution adapters, lifecycle status, cancellation, logs, and execution receipts.

## First next work

- [ ] Implement a local command runner with explicit working directory, inputs, outputs, and cancellation.
- [ ] Define submit/status/cancel/logs capabilities with accurate unsupported states.
- [ ] Add one backend only after its access, budget, and artifact retention are decided.

## Interfaces and composition

A future runner accepts an explicit command/workload, resources, working directory, input artifact references, and output destination. It reports identity, lifecycle state, logs, and output references. Planner recommendations are inputs, never automatic authorization to allocate resources. No wire format or backend capability is implemented yet.

[Inherited blueprint](blueprint.md) preserves the relevant original design sections. Provider claims, dates, estimates, and unimplemented features there are historical requirements, not new measurements.

## Acceptance

The first implementation must install/run independently, declare dependencies, include a useful example and focused behavior checks, and record remaining limitations. Do not mark this project implemented solely because the documentation exists.
