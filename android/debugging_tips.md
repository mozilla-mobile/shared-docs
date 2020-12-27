# Debugging Tips


### Profiling code snippits

You easily profile a section of your application programatically starting and stopping the profiler.

```
Debug.startMethodTracingSampling("${context.filesDir}/something.trace", 0, 100)
// Code to profile
Debug.stopMethodTracing()
```

You can then find the results in the *Device File Explorer* under the path `Data > Data > org.mozilla.app.debug > something.trace` and load it in the profiler