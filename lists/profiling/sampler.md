[Return back](../profiling.md#Profiling-Tools)

----
## Sampler

Its most important features are:

- A sampling profiler (sampler) to see exactly where the Minecraft client/server spends its time: start, (wait), stop, export sub-commands
- Event-based sampling triggers, e.g. to capture only lag spikes: trigger sub-command
- Actually precise tickrate information: tps sub-command or F3
- Counts for ticking game objects to notice any excess: counts sub-command, more detailed when invoked with the dimension id
- Memory information and garbage collection statistics: memory sub-command
- Highlights for tile entity special renderers (potentially expensively rendered blocks): tesr sub-command
- Highlights for the sources of chunk updates: renderupdates sub-command
- Various other sub-commands for investigating network I/O, chunk loads, saves, finding blocks/entities, ...

----
[Scroll back](#Sampler)