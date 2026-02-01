# **!ВАЖНО! ДАННЫЕ ФЛАГИ НЕ ПРЕДНАЗНАЧЕНЫ ДЛЯ ИСПОЛЬЗОВАНИЯ ГДЕ ЛИБО КРОМЕ GRAALVM 25+ ВЕРСИИ**

Я решил сделать свой аналог этих меовси фагов. 
<br>Оригинальная страница с ними мне никогда не нравилась, поскольку там помимо действительно рабочих флагов насрано дефолтными флагами поверх. 
<br>Тут я к чёртовой матери вырезал все дефолтные, оставив только то, что не включено по умолчанию на graalvm25. А также добавил пару флагов от себя.

# The flags set
## Для G1GC

```--add-modules=jdk.incubator.vector -XX:+UseG1GC -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=28 -XX:G1MaxNewSizePercent=50 -XX:G1HeapRegionSize=16M -XX:G1ReservePercent=15 -XX:G1MixedGCCountTarget=3 -XX:InitiatingHeapOccupancyPercent=20 -XX:G1MixedGCLiveThresholdPercent=90 -XX:SurvivorRatio=32 -XX:G1HeapWastePercent=5 -XX:MaxTenuringThreshold=1 -XX:+PerfDisableSharedMem -XX:G1SATBBufferEnqueueingThresholdPercent=30 -XX:G1ConcMarkStepDurationMillis=5 -XX:G1RSetUpdatingPauseTimePercent=0 -XX:+UseNUMA -XX:-DontCompileHugeMethods -XX:MaxNodeLimit=240000 -XX:NodeLimitFudgeFactor=8000 -XX:ReservedCodeCacheSize=400M -XX:NonNMethodCodeHeapSize=12M -XX:ProfiledCodeHeapSize=194M -XX:NonProfiledCodeHeapSize=194M -XX:NmethodSweepActivity=1 -XX:+UseFastUnorderedTimeStamps -XX:+UseCriticalJavaThreadPriority -XX:AllocatePrefetchStyle=3 -XX:+AlwaysActAsServerClassMachine -XX:+UseTransparentHugePages -XX:LargePageSizeInBytes=2M -XX:+UseLargePages -XX:+UseStringDeduplication -XX:+OmitStackTraceInFastThrow -XX:+UseFastStosb -XX:+UseVectorCmov -XX:+AlignVector -XX:+EnableVectorSupport -XX:+UseCharacterCompareIntrinsics -XX:+UseVectorStubs -XX:UseAVX=2 -XX:+UseCompactObjectHeaders -XX:AutoBoxCacheMax=256 -XX:+TrustFinalNonStaticFields -Djdk.nio.maxCachedBufferSize=262144 -Djdk.graal.UsePriorityInlining=true -Djdk.graal.VectorizeHashes=true -Djdk.graal.VectorizeSIMD=true -Djdk.graal.TuneInlinerExploration=1 -Djdk.graal.CompilerConfiguration=enterprise```

## Аналог для ZGC (используйте только с большими объёмами памяти)

```--add-modules=jdk.incubator.vector -XX:+UseZGC -XX:-ZProactive -XX:SoftMaxHeapSize=$((Memory - 2048))M -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:+PerfDisableSharedMem -XX:+UseNUMA -XX:-DontCompileHugeMethods -XX:MaxNodeLimit=240000 -XX:NodeLimitFudgeFactor=8000 -XX:ReservedCodeCacheSize=400M -XX:NonNMethodCodeHeapSize=12M -XX:ProfiledCodeHeapSize=194M -XX:NonProfiledCodeHeapSize=194M -XX:NmethodSweepActivity=1 -XX:+UseFastUnorderedTimeStamps -XX:+UseCriticalJavaThreadPriority -XX:+AlwaysActAsServerClassMachine -XX:+UseTransparentHugePages -XX:LargePageSizeInBytes=2M -XX:+UseLargePages -XX:+UseStringDeduplication -XX:+OmitStackTraceInFastThrow -XX:+UseFastStosb -XX:+UseVectorCmov -XX:+AlignVector -XX:+EnableVectorSupport -XX:+UseCharacterCompareIntrinsics -XX:+UseVectorStubs -XX:UseAVX=2 -XX:+UseCompactObjectHeaders -XX:AutoBoxCacheMax=256 -XX:+TrustFinalNonStaticFields -Djdk.nio.maxCachedBufferSize=262144 -Djdk.graal.UsePriorityInlining=true -Djdk.graal.VectorizeHashes=true -Djdk.graal.VectorizeSIMD=true -Djdk.graal.TuneInlinerExploration=1 -Djdk.graal.CompilerConfiguration=enterprise```

# Пояснение

Касательно основы флагов можете почитать не оригинальной статье.
<br>Я же добавил следующие флаги:
<br> `-XX:+UseCompactObjectHeaders` - Флаг, который снижает расходы памяти на заголовки объектов, сжимая их до 64 бит на 64 битных архитектурах. После добавления заметен ощутимый спад потребления памяти.
<br> `-XX:AutoBoxCacheMax=256` - Флаг, задающий размер кеша интов для операций боксинга. Увеличен вдвое относительно базового значения. Потенциально может ускорить базовые операции при взаимодействии с коллекциями, где хранятся объекты Integer.
<br> `-XX:+TrustFinalNonStaticFields` - Флаг, который заставляет java оптимизировать не-static final поля так же как и static (т.е. константы), что позволяет значительно оптимизировать обращения к ним.
