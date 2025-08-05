# Welcome !
Hewwo there, I'm glad you are here ! This instruction will guide you to use MeowIce's Flags to make your Minecraft server run as it best ^^
## Compatibility
My flags are only compatible and tested with:
- Java 24+,
- GraalVM JVM,
- Linux,
- Minecraft 1.20+  
> [!TIP]
> Using MeowIce's Flags with [Leaf](https://github.com/Winds-Studio/Leaf) as server software can boost more performance !
# TL;DR: The flags
## G1GC version (for server below 32GB allocated heap)
> [!NOTE]
> This is recommended for servers allocated below 32GB RAM with basic resource usage. Balanced between memory usage and performance.

`--add-modules=jdk.incubator.vector -XX:+UseG1GC -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=28 -XX:G1MaxNewSizePercent=50 -XX:G1HeapRegionSize=16M -XX:G1ReservePercent=15 -XX:G1MixedGCCountTarget=3 -XX:InitiatingHeapOccupancyPercent=20 -XX:G1MixedGCLiveThresholdPercent=90 -XX:SurvivorRatio=32 -XX:G1HeapWastePercent=5 -XX:MaxTenuringThreshold=1 -XX:+PerfDisableSharedMem -XX:G1SATBBufferEnqueueingThresholdPercent=30 -XX:G1ConcMarkStepDurationMillis=5 -XX:G1RSetUpdatingPauseTimePercent=0 -XX:+UseNUMA -XX:-DontCompileHugeMethods -XX:MaxNodeLimit=240000 -XX:NodeLimitFudgeFactor=8000 -XX:ReservedCodeCacheSize=400M -XX:NonNMethodCodeHeapSize=12M -XX:ProfiledCodeHeapSize=194M -XX:NonProfiledCodeHeapSize=194M -XX:NmethodSweepActivity=1 -XX:+UseFastUnorderedTimeStamps -XX:+UseCriticalJavaThreadPriority -XX:AllocatePrefetchStyle=3 -XX:+AlwaysActAsServerClassMachine -XX:+UseTransparentHugePages -XX:LargePageSizeInBytes=2M -XX:+UseLargePages -XX:+EagerJVMCI -XX:+UseStringDeduplication -XX:+UseAES -XX:+UseAESIntrinsics -XX:+UseFMA -XX:+UseLoopPredicate -XX:+RangeCheckElimination -XX:+OptimizeStringConcat -XX:+UseCompressedOops -XX:+UseThreadPriorities -XX:+OmitStackTraceInFastThrow -XX:+RewriteBytecodes -XX:+RewriteFrequentPairs -XX:+UseFPUForSpilling -XX:+UseFastStosb -XX:+UseNewLongLShift -XX:+UseVectorCmov -XX:+UseXMMForArrayCopy -XX:+UseXmmI2D -XX:+UseXmmI2F -XX:+UseXmmLoadAndClearUpper -XX:+UseXmmRegToRegMoveAll -XX:+EliminateLocks -XX:+DoEscapeAnalysis -XX:+AlignVector -XX:+OptimizeFill -XX:+EnableVectorSupport -XX:+UseCharacterCompareIntrinsics -XX:+UseCopySignIntrinsic -XX:+UseVectorStubs -XX:UseAVX=2 -XX:UseSSE=4 -XX:+UseFastJNIAccessors -XX:+UseInlineCaches -XX:+SegmentedCodeCache -Djdk.nio.maxCachedBufferSize=262144 -Djdk.graal.UsePriorityInlining=true -Djdk.graal.Vectorization=true -Djdk.graal.OptDuplication=true -Djdk.graal.DetectInvertedLoopsAsCounted=true -Djdk.graal.LoopInversion=true -Djdk.graal.VectorizeHashes=true -Djdk.graal.EnterprisePartialUnroll=true -Djdk.graal.VectorizeSIMD=true -Djdk.graal.StripMineNonCountedLoops=true -Djdk.graal.SpeculativeGuardMovement=true -Djdk.graal.TuneInlinerExploration=1 -Djdk.graal.LoopRotation=true -Djdk.graal.CompilerConfiguration=enterprise
`
## ZGC version (for server with 32GB+ allocated heap)
> [!NOTE]
> This is recommended for servers with more than 32GB of allocated memory and many CPU cores, allowing for minimizing the delay between each GC run with a larger heap size in an intensive environment.

> [!WARNING]
> Only use this if you have more than 10 CPU cores; using ZGC on systems with fewer than 8 cores may cause a significant performance impact !

`--add-modules=jdk.incubator.vector -XX:+UseZGC -XX:-ZProactive -XX:SoftMaxHeapSize=$((Memory - 2048))M -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:+PerfDisableSharedMem -XX:+UseNUMA -XX:-DontCompileHugeMethods -XX:MaxNodeLimit=240000 -XX:NodeLimitFudgeFactor=8000 -XX:ReservedCodeCacheSize=400M -XX:NonNMethodCodeHeapSize=12M -XX:ProfiledCodeHeapSize=194M -XX:NonProfiledCodeHeapSize=194M -XX:NmethodSweepActivity=1 -XX:+UseFastUnorderedTimeStamps -XX:+UseCriticalJavaThreadPriority -XX:AllocatePrefetchStyle=1 -XX:+AlwaysActAsServerClassMachine -XX:+UseTransparentHugePages -XX:LargePageSizeInBytes=2M -XX:+UseLargePages -XX:+EagerJVMCI -XX:+UseStringDeduplication -XX:+UseAES -XX:+UseAESIntrinsics -XX:+UseFMA -XX:+UseLoopPredicate -XX:+RangeCheckElimination -XX:+OptimizeStringConcat -XX:+UseCompressedOops -XX:+UseThreadPriorities -XX:+OmitStackTraceInFastThrow -XX:+RewriteBytecodes -XX:+RewriteFrequentPairs -XX:+UseFPUForSpilling -XX:+UseFastStosb -XX:+UseNewLongLShift -XX:+UseVectorCmov -XX:+UseXMMForArrayCopy -XX:+UseXmmI2D -XX:+UseXmmI2F -XX:+UseXmmLoadAndClearUpper -XX:+UseXmmRegToRegMoveAll -XX:+EliminateLocks -XX:+DoEscapeAnalysis -XX:+AlignVector -XX:+OptimizeFill -XX:+EnableVectorSupport -XX:+UseCharacterCompareIntrinsics -XX:+UseCopySignIntrinsic -XX:+UseVectorStubs -XX:UseAVX=2 -XX:UseSSE=4 -XX:+UseFastJNIAccessors -XX:+UseInlineCaches -XX:+SegmentedCodeCache -Djdk.nio.maxCachedBufferSize=262144 -Djdk.graal.UsePriorityInlining=true -Djdk.graal.Vectorization=true -Djdk.graal.OptDuplication=true -Djdk.graal.DetectInvertedLoopsAsCounted=true -Djdk.graal.LoopInversion=true -Djdk.graal.VectorizeHashes=true -Djdk.graal.EnterprisePartialUnroll=true -Djdk.graal.VectorizeSIMD=true -Djdk.graal.StripMineNonCountedLoops=true -Djdk.graal.SpeculativeGuardMovement=true -Djdk.graal.TuneInlinerExploration=1 -Djdk.graal.LoopRotation=true -Djdk.graal.CompilerConfiguration=enterprise`

# What is MeowIce's Flags ?
MeowIce's Flags aimed to blend Aikar's Flags optimization with new JVM features to further boost the overall performance, while allowing it to use advanced CPU instructions to accelerate some workloads.
> [!NOTE]
> Hey don't forget to leave a star !
> <img width="756" height="157" alt="image" src="https://github.com/user-attachments/assets/4db8d2e9-e2fa-448e-9a52-7af7a6c7369a" />

# Why would I have to... switch ?
Almost 99% of Minecraft servers use Aikar's Flags, and it is recommended by many people (some use nothing !). But why use other flags ?  
The answer is: We have now developed to Minecraft 1.21.x and Java 24 (at the time of writing this), and Aikar's Flags **was written mainly to optimize Minecraft's Garbage Collector** and Java version at that time (Java 8 and Java 11, around 2018 - 2020). Later Java versions (from Java 17 and above) have added many optimization options for the JVM. So I wrote a separate flag to support these optimizations and integrate new features of Java 17+ while still keeping Aikar's flags mainly to optimize GC. <ins>There's no risk in trying my flags !</ins>
# Why GraalVM but not AdoptiumJDK or OpenJDK ?
GraalVM with better JIT performance and more aggressive optimizations compared to traditional `HotSpot C2` found in many JDKs (including OpenJDK and AdoptiumJDK (aka. Eclipse Temurin)). This change makes inlining, loop unrolling, escape analysis, and vectorization work better while maintaining lower CPU usage.  
Furthermore, the GraalVM compiler compiles plugins and server code faster and smarter, adapting to actual usage and environment on the fly.  
> [!TIP]
> GraalVM allows you to inspect memory usage and trace down naughty plugins using VisualVM !

# Flags explanation
- `--add-modules=jdk.incubator.vector` Enables advanced vector computation capabilities for Pufferfish/Purpur 1.18+. Useful for optimizing chunk loading and rendering.
- ` -XX:+UseG1GC -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=28 -XX:G1MaxNewSizePercent=50 -XX:G1HeapRegionSize=16M -XX:G1ReservePercent=15 -XX:G1MixedGCCountTarget=3 -XX:InitiatingHeapOccupancyPercent=20 -XX:G1MixedGCLiveThresholdPercent=90 -XX:SurvivorRatio=32 -XX:G1HeapWastePercent=5 -XX:MaxTenuringThreshold=1 -XX:+PerfDisableSharedMem -XX:G1SATBBufferEnqueueingThresholdPercent=30 -XX:G1ConcMarkStepDurationMillis=5 -XX:G1RSetUpdatingPauseTimePercent=0` These are very generic G1GC flags, based on [Aikar's Flags](https://aikar.co/2018/07/02/tuning-the-jvm-g1gc-garbage-collector-flags-for-minecraft/).
- `-XX:+UseNUMA` Enables NUMA or (Non Uniform Memory Access) for supported architecture.
- `-XX:-DontCompileHugeMethods` Allows the JVM to compile larger methods to optimize performance.
- `-XX:MaxNodeLimit=240000 -XX:NodeLimitFudgeFactor=8000` Sets the maximum number of nodes for the compiler's intermediate representation.
- `-XX:ReservedCodeCacheSize=400M` Sets the cache size for compiled codes. This will ensure the JIT have enough space for compiling.
- `-XX:NonNMethodCodeHeapSize=12M` Sets the code heap size for non-method codes.
- `-XX:ProfiledCodeHeapSize=194M -XX:NonProfiledCodeHeapSize=194M` Same as above but for profiled and non profiled methods.
- `-XX:NmethodSweepActivity=1` Helps managing code cache more efficiently by keeping "cold" code in the cache for a longer time. There is no risk of "filling up" the code cache either, as cold code is more aggressively removed as it fills up.
## Advanced Performance Tuning
- `-XX:+UseFastUnorderedTimeStamps` This option enables the usage of fast unordered timestamps for time-related operations in the JVM.
- `-XX:+UseCriticalJavaThreadPriority` This option assigns a higher priority to critical Java threads, which can improve responsiveness and reduce latency in critical parts of the application.
- `-XX:AllocatePrefetchStyle=3` This will instruct JVM to use code style 3 for faster memory allocation. A value of 3 enables the most aggressive prefetching. More aggressive prefetching is generally useful on newer CPUs with large caches.
- `-XX:+AlwaysActAsServerClassMachine` Forces the JVM to act as if it's running on a server-class machine.
- `-XX:+UseTransparentHugePages` As it name said.
- `-XX:LargePageSizeInBytes=2M` Size of huge (large) pages.
- `-XX:+UseLargePages` Enables the usage of large pages for the JVM's memory allocation. Large pages can improve performance by reducing Translation Lookaside Buffer misses.
- `-XX:+EagerJVMCI` Enables the JVM Compiler Interface as early as needed, especially with GraalVM.
- `-XX:+UseStringDeduplication` Reduces memory ussage by deduping identical strings. Might reduce frequent GCs.
- `-XX:+UseAES -XX:+UseAESIntrinsics` Enables Hardware accelerated Advanced Encryption Standart intrinsics.
- `-XX:+UseFMA` Enables Fused Multiply Add instructions.
- `-XX:+UseLoopPredicate` Enables loop predicate optimization.
- `-XX:+RangeCheckElimination` Enables the elimination of range checks.
- `-XX:+OptimizeStringConcat` Enables optimization of string concatenation in the JVM, which can lead to improved performance when working with string concatenation operations.
- `-XX:+UseCompressedOops` Enables the use of compressed object pointers (Oops) which reduces memory usage on 64-bit systems.
- `-XX:+UseThreadPriorities` Enables the use of thread priorities.
- `-XX:+OmitStackTraceInFastThrow` Omits the stack trace for exceptions that are frequently thrown.
- `-XX:+RewriteBytecodes -XX:+RewriteFrequentPairs` Improves performance by actively rewriting byte codes and its pairs.
- `-XX:+UseFPUForSpilling` Provides a faster temporary storage for spills, so when we need just a few additional spill slots, we can avoid tripping to L1 cache-backed stack for this.
- `-XX:+UseFastStosb` Enables support for fast string operations.
- `-XX:+UseNewLongLShift` Use optimized bitwise shift left.
- `-XX:+UseVectorCmov` This option enables the usage of vectorized compare and move (cmov) instructions for better performance on CPUs that support these instructions.
- `-XX:+UseXMMForArrayCopy -XX:+UseXmmI2D -XX:+UseXmmI2F -XX:+UseXmmRegToRegMoveAll` Uses XMM registers for Array Copy, int2double, int2float, register2register move operations
- `-XX:+UseXmmLoadAndClearUpper` Same as above but to load and clear upper registers.
- `-XX:+EliminateLocks` Improves single-threaded performance.
- `-XX:+DoEscapeAnalysis` Escape analysis is a technique by which the Java Hotspot Server Compiler can analyze the scope of a new object's uses and decide whether to allocate it on the Java heap.
- `-XX:+AlignVector` Aligns vectors for optimization.
- `-XX:+OptimizeFill` Enables optimization of memory fill operations.
- `-XX:+EnableVectorSupport` Its name suggested.
- `-XX:+UseCharacterCompareIntrinsics` Enables intrinsification of java.lang.Character functions.
- `-XX:+UseCopySignIntrinsic` Enables intrinsification of Math.copySign.
- `-XX:+UseVectorStubs` Optimizes vector operations.
- `-XX:UseAVX=2 -XX:UseSSE=4` Enable supported AVX, SSE instructions set on x86/x64 compatible CPUs.
- `-XX:+UseFastJNIAccessors` Use optimized versions of GetField.
- `-XX:+UseInlineCaches` Use Inline Caches for virtual calls
- `-XX:+SegmentedCodeCache` Enables the segmented code cache, which improves code cache management.
## GraalVM Compiler Specific Flags
- `-Djdk.nio.maxCachedBufferSize=262144` Sets the maximum size for cached direct buffers.  
- `-Djdk.graal.UsePriorityInlining=true` Enables priority inlining in the Graal compiler.  
- `-Djdk.graal.Vectorization=true` Enables vectorization in the Graal compiler.  
- `-Djdk.graal.OptDuplication=true` Enables optimization duplication in the Graal compiler.  
- `-Djdk.graal.DetectInvertedLoopsAsCounted=true` Enables detection of inverted loops as counted loops.  
- `-Djdk.graal.LoopInversion=true` Enables loop inversion in the Graal compiler.  
- `-Djdk.graal.VectorizeHashes=true` Enables vectorization of hash computations.  
- `-Djdk.graal.VectorizeSIMD=true` Enables SIMD (Single Instruction - Multiple Data) vectorization.  
- `-Djdk.graal.StripMineNonCountedLoops=true` Enables strip mining of non-counted loops.  
- `-Djdk.graal.SpeculativeGuardMovement=true` Enables speculative guard movement in the Graal compiler.  
- `-Djdk.graal.TuneInlinerExploration=1` Tunes the inliner exploration parameter in the Graal compiler.  
- `-Djdk.graal.LoopRotation=true` Enables loop rotation in the Graal compiler.  
- `-Djdk.graal.UseCountedLoopSafepoints=true` Enables safepoint insertion in counted loops.  
- `-Djdk.graal.EnterprisePartialUnroll=true` Enables partial unrolling optimizations in enterprise mode.  
- `-Djdk.graal.CompilerConfiguration=enterprise` Enables Enterprise mode optimizations in the Graal compiler.

# Comparison
I have made a comparison with one of my customers' servers.
## Spark
Aikar's Flags and Adoptium JDK:

<img width="1909" height="398" alt="image" src="https://github.com/user-attachments/assets/eae32edc-f162-4b33-9246-2443933621ac" />


MeowIce's Flags and GraalVM:

<img width="1920" height="423" alt="image" src="https://github.com/user-attachments/assets/dcd97360-d73e-49f3-a4b2-1869bb581686" />

## TPS
With only Aikar's flags and OpenJDK:
<img width="1405" height="202" alt="image" src="https://github.com/user-attachments/assets/42e6dab1-76ed-4c1b-b320-d4d0a3407cf1" />
With MeowIce's flags and GraalVM:
<img width="1296" height="255" alt="image" src="https://github.com/user-attachments/assets/c8280ebd-f51e-43fb-a16a-62340c8829ca" />


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


## Another benchmark from user.
### System specs
- 10700K @ 5.00 GHz OC
- RAM DDR4 96 GB @ 3000 MT/s
- OS Proxmox `8.4.1` (Running Ubuntu 24.04.2 LTS Pterodactyl Panel)

Version used to test is `leaf-1.21.8-52.jar`. Both servers had 6 GB of allocated RAM and 16 dedicated threads. For monitoring and measuring data [UnifiedMetrics](https://github.com/Cubxity/UnifiedMetrics) was used.

Java Docker Image for Pterodactyl used: ghcr.io/vanes430/java:graaljdk_24-debian from https://github.com/vanes430/java

For Aikar's i used 

`java -Xms6G -Xmx6G -XX:+AlwaysPreTouch -XX:+DisableExplicitGC -XX:+ParallelRefProcEnabled -XX:+PerfDisableSharedMem -XX:+UnlockExperimentalVMOptions -XX:+UseG1GC -XX:G1HeapRegionSize=8M -XX:G1HeapWastePercent=5 -XX:G1MaxNewSizePercent=40 -XX:G1MixedGCCountTarget=4 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1NewSizePercent=30 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:G1ReservePercent=20 -XX:InitiatingHeapOccupancyPercent=15 -XX:MaxGCPauseMillis=200 -XX:MaxTenuringThreshold=1 -XX:SurvivorRatio=32 --add-modules=jdk.incubator.vector -DLeaf.enableFMA=true -Dusing.aikars.flags=https://mcflags.emc.gs -Daikars.new.flags=true -jar server.jar nogui`  

And for MeowIce i used 

`java -Xms6G -Xmx6G --add-modules=jdk.incubator.vector -XX:+UseG1GC -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=28 -XX:G1MaxNewSizePercent=50 -XX:G1HeapRegionSize=16M -XX:G1ReservePercent=15 -XX:G1MixedGCCountTarget=3 -XX:InitiatingHeapOccupancyPercent=20 -XX:G1MixedGCLiveThresholdPercent=90 -XX:SurvivorRatio=32 -XX:G1HeapWastePercent=5 -XX:MaxTenuringThreshold=1 -XX:+PerfDisableSharedMem -XX:G1SATBBufferEnqueueingThresholdPercent=30 -XX:G1ConcMarkStepDurationMillis=5 -XX:G1RSetUpdatingPauseTimePercent=0 -XX:+UseNUMA -XX:-DontCompileHugeMethods -XX:MaxNodeLimit=240000 -XX:NodeLimitFudgeFactor=8000 -XX:ReservedCodeCacheSize=400M -XX:NonNMethodCodeHeapSize=12M -XX:ProfiledCodeHeapSize=194M -XX:NonProfiledCodeHeapSize=194M -XX:NmethodSweepActivity=1 -XX:+UseFastUnorderedTimeStamps -XX:+UseCriticalJavaThreadPriority -XX:AllocatePrefetchStyle=3 -XX:+AlwaysActAsServerClassMachine -XX:+UseTransparentHugePages -XX:LargePageSizeInBytes=2M -XX:+UseLargePages -XX:+EagerJVMCI -XX:+UseStringDeduplication -XX:+UseAES -XX:+UseAESIntrinsics -XX:+UseFMA -XX:+UseLoopPredicate -XX:+RangeCheckElimination -XX:+OptimizeStringConcat -XX:+UseCompressedOops -XX:+UseThreadPriorities -XX:+OmitStackTraceInFastThrow -XX:+RewriteBytecodes -XX:+RewriteFrequentPairs -XX:+UseFPUForSpilling -XX:+UseFastStosb -XX:+UseNewLongLShift -XX:+UseVectorCmov -XX:+UseXMMForArrayCopy -XX:+UseXmmI2D -XX:+UseXmmI2F -XX:+UseXmmLoadAndClearUpper -XX:+UseXmmRegToRegMoveAll -XX:+EliminateLocks -XX:+DoEscapeAnalysis -XX:+AlignVector -XX:+OptimizeFill -XX:+EnableVectorSupport -XX:+UseCharacterCompareIntrinsics -XX:+UseCopySignIntrinsic -XX:+UseVectorStubs -XX:UseAVX=2 -XX:UseSSE=4 -XX:+UseFastJNIAccessors -XX:+UseInlineCaches -XX:+SegmentedCodeCache -Djdk.nio.maxCachedBufferSize=262144 -Djdk.graal.UsePriorityInlining=true -Djdk.graal.Vectorization=true -Djdk.graal.OptDuplication=true -Djdk.graal.DetectInvertedLoopsAsCounted=true -Djdk.graal.LoopInversion=true -Djdk.graal.VectorizeHashes=true -Djdk.graal.EnterprisePartialUnroll=true -Djdk.graal.VectorizeSIMD=true -Djdk.graal.StripMineNonCountedLoops=true -Djdk.graal.SpeculativeGuardMovement=true -Djdk.graal.TuneInlinerExploration=1 -Djdk.graal.LoopRotation=true -Djdk.graal.CompilerConfiguration=enterprise -DLeaf.enableFMA=true -jar server.jar nogui`


**So now with results**

Aikar's Grafana https://snapshots.raintank.io/dashboard/snapshot/2PwtSHpB6w3BT2jStlYWAbCaKoGf2WJ1?orgId=0

MeowIce's Grafana https://snapshots.raintank.io/dashboard/snapshot/xPugteW5fyKu6Mpq4Zi8J0HgTRU4KEDF?orgId=0

Data showing all of quantile's 

Aikar's: https://snapshots.raintank.io/dashboard/snapshot/KqirFpcpC4Smo6qrSjfKf6aQeee4KvJy?orgId=0

MeowIce's: https://snapshots.raintank.io/dashboard/snapshot/IpKM7ZpJOrwJTwErZucogu79Akzmx9JR?orgId=0

Some screenshots
<img width="940" height="418" alt="image" src="https://github.com/user-attachments/assets/ca24329e-5d2b-42f5-9b8e-d21c49305cc8" />

<img width="939" height="409" alt="image" src="https://github.com/user-attachments/assets/1b904c7b-6c15-4773-9bb3-622ed86b0941" />

  Overall, I observed an average performance uplift of around 20 MSPT. 
  However, the most crucial difference appeared once I reached 1k simulated players:
  
  **MeowIce’s flags consistently held around 30–35 MSPT**
  
  **Aikar’s flags spiked to and held around 90–95 MSPT**

I did my best to minimize variance in the testing process. Please disregard the [initial](https://i.imgur.com/Mw1hkXx.png) segment of the data, as it isn’t relevant due to me forgetting to kill all entities (they were removed on Aikar’s setup from the star).

This oversight does not affect the main conclusion: **MeowIce’s flags demonstrated a significant performance advantage over Aikar’s.**

You can confirm these findings by reviewing the Grafana snapshots. 

One final note: I only encountered a single G1 Old Gen event, which caused a minor spike. Aside from that, the performance was very stable and highly impressive.


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


### Sources
- [Java Flags Benchmarked](https://github.com/brucethemoose/Minecraft-Performance-Flags-Benchmarks)
- [Obydux GraalVM Flags](https://github.com/Obydux/Minecraft-GraalVM-Flags/)
- [Optimize MC Server on RedHat](https://www.redhat.com/en/blog/optimizing-rhel-8-run-java-implementation-minecraft-server)
### My Optimization service:
- [Dịch vụ tối ưu, fix lag máy chủ Minecraft](https://minecraftvn.net/toi-uu-fix-lag-cuc-cang-may-chu-minecraft.t47454/)
