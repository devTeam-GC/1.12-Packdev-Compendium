[Return To Articles](../articles.md#Articles)

----
## Java Optimization

This page is about selecting the appropriate Java version and JVM arguments. 

>Java tweaks improve server performance and reduce client stuttering, but they don't boost average client FPS much (if at all). For that, running correct/up-to-date graphics drivers and performance mods is far more important.

---
## Picking a Java Runtime Environment

Generally Java 17 or upcoming 21 is better in terms of performance and GC stuttering, but we have to use Java 8 due to old Forge being incompatible with anything newer then Java 8. To check it you can launch vanilla 1.12.2 on Java 17.<br>Until we have [CleanroomLoader](https://github.com/CleanroomMC/Cleanroom) released, we have to use slow Java 8. 

I recommend to use latest **Adoptium Java 8** releases for client, this implemention has no memory leaks and has optimal CPU usage compared to **GraalVM**. You can download it from [here](https://adoptium.net/temurin/releases/?os=windows&arch=x64&version=8&package=jre).

For servers I recomend you use **GraalVM Enterprise Edition Java 8**. 

>GraalVM is a new Java VM from Oracle that can improve the performance of (modded and vanilla) Minecraft. While client FPS gains are modest, server-side workloads like chunk generation can get a 20%+ boost!

It has optimizations that can increase server TPS and also increases RAM usage and CPU usage a lot (in my tests), so thats why I don't recommend to use it on the client.
## Memory Allocation

>Minimum and maximum (`-xms` and `-xmx`) memory should be set to the same value, as explained here: [https://dzone.com/articles/benefits-of-setting-initial-and-maximum-memory-siz](https://dzone.com/articles/benefits-of-setting-initial-and-maximum-memory-siz)
>Sizes are set in megabytes (`-Xms4096M`) or gigabytes (`-Xmx8G`)
>
>Allocating too much memory can break the GC or just slow Minecraft down, even if you have plenty RAM to spare. Allocating too little can also slow down or break the game. Keep a close eye on the Windows Task manager (or your DE's system monitor) as Minecraft is running, and allocate only as much as it needs (which is usually less than 8G). `sparkc gcmonitor` will tell you if your allocation is too high (the pauses will be too long) or too low (frequent GC with a low memory warning in the notification).
## JVM Optimization Arguments

Base Java 8 optimization flags to use everywhere:
```
-XX:+PerfDisableSharedMem -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:+AggressiveOpts -XX:+UseFastAccessorMethods -XX:MaxInlineLevel=15 -XX:MaxVectorSize=32 -XX:+UseCompressedOops -XX:ThreadPriorityPolicy=1 -XX:NmethodSweepActivity=1 -XX:ReservedCodeCacheSize=350M -XX:MaxNodeLimit=240000 -XX:NodeLimitFudgeFactor=8000 -XX:+UseFPUForSpilling -XX:+UseXMMForArrayCopy
```

> ATTENTION! `-XX:+PerfDisableSharedMem` optimization disables the possibility to profile your Minecraft process with Java profiling tools such as VisualVM, JProfiler, etc.

If you use GraalVM Enterprise Edition, it also has a lot of other optimization arguments, you can check them out [here](https://github.com/brucethemoose/Minecraft-Performance-Flags-Benchmarks#java-8).
## JVM GC Arguments

If you have less than 6 cores better to not use G1GC GC, it has terrible stuttering in many cases on low end PCs. Instead I recommend you use CMS GC (ConcMarkSweepGC).<br>Developer of VintageFix, ModernFix said that's the best GC available on Java 8 if your pack uses 4 GB of RAM or less.

These JVM arguments allow you to enable CMS GC:
```
-XX:+UseConcMarkSweepGC -XX:+UseParNewGC -XX:+CMSConcurrentMTEnabled -XX:+ExplicitGCInvokesConcurrent -XX:ParallelGCThreads=2 -XX:MaxGCPauseMillis=10 -XX:GCPauseIntervalMillis=50 -XX:NewSize=84m -XX:+UseAdaptiveGCBoundary -XX:NewRatio=3
```

G1GC JVM arguments (use them if your pack uses more than 4 GB of RAM):
```
-XX:+UseG1GC -XX:MaxGCPauseMillis=37 -XX:G1HeapRegionSize=16M -XX:G1NewSizePercent=23 -XX:G1ReservePercent=20 -XX:SurvivorRatio=32 -XX:G1MixedGCCountTarget=3 -XX:G1HeapWastePercent=20 -XX:InitiatingHeapOccupancyPercent=10 -XX:G1RSetUpdatingPauseTimePercent=0 -XX:MaxTenuringThreshold=1 -XX:G1SATBBufferEnqueueingThresholdPercent=30 -XX:G1ConcMarkStepDurationMillis=5.0 -XX:G1ConcRSHotCardLimit=16 -XX:G1ConcRefinementServiceIntervalMillis=150 -XX:GCTimeRatio=99
```


---
## Sources

- Most of the information in this guide is based on: https://github.com/brucethemoose/Minecraft-Performance-Flags-Benchmarks
- https://cassiofernando.netlify.app/blog/minecraft-java-arguments

----
[Return To Title](#Java-Optimization)