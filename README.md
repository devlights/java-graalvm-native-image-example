# java-graalvm-native-image-example

Oracle GraalVM example by java. (using native-image)

## Requirements

### [GraalVM](https://www.graalvm.org/)

```sh
$ wget https://download.oracle.com/graalvm/20/latest/graalvm-jdk-20_linux-x64_bin.tar.gz
$ tar zxf graalvm-jdk-*.tar.gz
$ mv graalvm-jdk-*/ graalvm
$ graalvm/bin/gu install native-image
```

### [Task](https://taskfile.dev/)

```sh
$ go install github.com/go-task/task/v3/cmd/task@latest
```

## How to

### Run

```sh
$ task helloworld
task: [install-nativeimage] /workspace/java-graalvm-native-image-example/graalvm/bin/gu install native-image
Picked up JAVA_TOOL_OPTIONS:  -Xmx3489m
Downloading: Artifacts catalog from gds.oracle.com
Skipping ULN EE channels, no username provided.
Downloading: Component catalog from www.graalvm.org
Processing Component: Native Image
Component Native Image (org.graalvm.native-image) is already installed.
task: [helloworld] rm -f ./app ./App.class
task: [helloworld] /workspace/java-graalvm-native-image-example/graalvm/bin/javac App.java
Picked up JAVA_TOOL_OPTIONS:  -Xmx3489m
task: [helloworld] /workspace/java-graalvm-native-image-example/graalvm/bin/native-image App
========================================================================================================================
GraalVM Native Image: Generating 'app' (executable)...
========================================================================================================================
[1/8] Initializing...                                                                                    (7.8s @ 0.18GB)
 Java version: 20.0.1+9, vendor version: Oracle GraalVM 20.0.1+9.1
 Graal compiler: optimization level: 2, target machine: x86-64-v3, PGO: ML-inferred
 C compiler: gcc (linux, x86_64, 11.3.0)
 Garbage collector: Serial GC (max heap size: 80% of RAM)
[2/8] Performing analysis...  [*****]                                                                   (12.9s @ 0.27GB)
   2,067 (61.54%) of  3,359 types reachable
   2,054 (47.01%) of  4,369 fields reachable
   9,606 (38.98%) of 24,641 methods reachable
     670 types,   106 fields, and   419 methods registered for reflection
      49 types,    32 fields, and    48 methods registered for JNI access
       4 native libraries: dl, pthread, rt, z
[3/8] Building universe...                                                                               (1.6s @ 0.42GB)
[4/8] Parsing methods...      [**]                                                                       (4.8s @ 0.40GB)
[5/8] Inlining methods...     [***]                                                                      (1.1s @ 0.34GB)
[6/8] Compiling methods...    [******]                                                                  (34.0s @ 0.35GB)
[7/8] Layouting methods...    [*]                                                                        (0.8s @ 0.38GB)
[8/8] Creating image...       [*]                                                                        (1.0s @ 0.42GB)
   3.70MB (48.26%) for code area:     4,490 compilation units
   3.61MB (47.09%) for image heap:   56,776 objects and 1 resources
 364.72kB ( 4.65%) for other data
   7.66MB in total
------------------------------------------------------------------------------------------------------------------------
Top 10 origins of code area:                                Top 10 object types in image heap:
   2.04MB java.base                                          721.46kB byte[] for code metadata
   1.32MB svm.jar (Native Image)                             473.01kB byte[] for java.lang.String
 100.54kB com.oracle.svm.svm_enterprise                      378.19kB java.lang.String
  51.70kB jdk.proxy1                                         344.98kB java.lang.Class
  44.55kB jdk.proxy3                                         264.89kB byte[] for general heap data
  34.19kB org.graalvm.nativeimage.base                       164.19kB java.util.HashMap$Node
  30.61kB org.graalvm.sdk                                    112.63kB char[]
  19.63kB jdk.internal.vm.compiler                            96.91kB byte[] for reflection metadata
  18.07kB jdk.internal.vm.ci                                  87.88kB java.lang.Object[]
  15.65kB jdk.proxy2                                          80.74kB com.oracle.svm.core.hub.DynamicHubCompanion
  816.00B for 1 more packages                                527.61kB for 553 more object types
------------------------------------------------------------------------------------------------------------------------
Recommendations:
 G1GC: Use the G1 GC ('--gc=G1') for improved latency and throughput.
 PGO:  Use Profile-Guided Optimizations ('--pgo') for improved throughput.
 HEAP: Set max heap for improved and more predictable memory usage.
 CPU:  Enable more CPU features with '-march=native' for improved performance.
 QBM:  Use the quick build mode ('-Ob') to speed up builds during development.
------------------------------------------------------------------------------------------------------------------------
                        2.3s (3.5% of total time) in 175 GCs | Peak RSS: 1.09GB | CPU load: 3.75
------------------------------------------------------------------------------------------------------------------------
Produced artifacts:
 /workspace/java-graalvm-native-image-example/helloworld/app (executable)
========================================================================================================================
Finished generating 'app' in 1m 4s.
task: [helloworld] file ./app
./app: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=acc49c38c534692b87b663e9b88fe8b2c4d0ed7e, for GNU/Linux 3.2.0, with debug_info, not stripped
task: [helloworld] ./app
hello world
```

## REFERENCES

- https://www.graalvm.org/
- https://medium.com/graalvm/a-new-graalvm-release-and-new-free-license-4aab483692f5
- https://www.graalvm.org/latest/reference-manual/native-image/
