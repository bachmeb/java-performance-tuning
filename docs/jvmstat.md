# jvmstat

## References
* http://www.oracle.com/technetwork/java/jvmstat-142257.html
* http://docs.oracle.com/javase/6/docs/technotes/tools/share/jstat.html

##### Tool Name
* jps	
  * Experimental: JVM Process Status Tool - Lists instrumented HotSpot Java virtual machines on a target system. (formerly jvmps)
* jstat	
  * Experimental: JVM Statistics Monitoring Tool - Attaches to an instrumented HotSpot Java virtual machine and collects and logs performance statistics as specified by the command line options. (formerly jvmstat)
* jstatd
  * Experimental: JVM jstat Daemon - Launches an RMI server application that monitors for the creation and termination of instrumented HotSpot Java virtual machines and provides a interface to allow remote monitoring tools to attach to Java virtual machines running on the local system. (formerly perfagent)
* visualgc
  * Experimental: Visual Garbage Collection Monitoring Tool - a graphical tool for monitoring the HotSpot Garbage Collector, Compiler, and class loader. It can monitor both local and remote JVMs.
* *Source: http://www.oracle.com/technetwork/java/jvmstat-142257.html*

### jps
##### See where is jps
```
whereis jps
```
```c
/*
jps: /usr/bin/jps /usr/share/man/man1/jps.1.gz
*/
```

##### Get a list of lvmids
```
jps
```
```c
/*
4345 Main
14519 Jps
*/
```
### jstat
##### See where is jstat
```
whereis jstat
```
```c
/*
jstat: /usr/bin/jstat /usr/share/man/man1/jstat.1.gz
*/
```
##### Get a list of jstat options
```
jstat -options
```
```c
/*
-class
-compiler
-gc
-gccapacity
-gccause
-gcnew
-gcnewcapacity
-gcold
-gcoldcapacity
-gcpermcapacity
-gcutil
-printcompilation
*/
```

##### Read the jstat help message
```
jstat -help
```
```c
/*
Usage: jstat -help|-options
       jstat -<option> [-t] [-h<lines>] <vmid> [<interval> [<count>]]

Definitions:
  <option>      An option reported by the -options option
  <vmid>        Virtual Machine Identifier. A vmid takes the following form:
                     <lvmid>[@<hostname>[:<port>]]
                Where <lvmid> is the local vm identifier for the target
                Java virtual machine, typically a process id; <hostname> is
                the name of the host running the target Java virtual machine;
                and <port> is the port number for the rmiregistry on the
                target host. See the jvmstat documentation for a more complete
                description of the Virtual Machine Identifier.
  <lines>       Number of samples between header lines.
  <interval>    Sampling interval. The following forms are allowed:
                    <n>["ms"|"s"]
                Where <n> is an integer and the suffix specifies the units as
                milliseconds("ms") or seconds("s"). The default units are "ms".
  <count>       Number of samples to take before terminating.
  -J<flag>      Pass <flag> directly to the runtime system.
*/
```

##### Show statistics of the behavior of the garbage collected heap
```
jstat -gc 14958
```
```c
/*
S0C     S1C      S0U      S1U   EC       EU        OC         OU        PC      PU           YGC  YGCT    FGC    FGCT     GCT
55552.0 110464.0 55551.6  0.0   224128.0 131690.4  889536.0   114546.0  61824.0 61709.4      6    0.853   1      0.327    1.180
*/
```
```c
/*
S0C	    Current survivor space 0 capacity (KB).
S1C	    Current survivor space 1 capacity (KB).
S0U	    Survivor space 0 utilization (KB).
S1U	    Survivor space 1 utilization (KB).
EC	    Current eden space capacity (KB).
EU	    Eden space utilization (KB).
OC	    Current old space capacity (KB).
OU	    Old space utilization (KB).
PC	    Current permanent space capacity (KB).
PU	    Permanent space utilization (KB).
YGC	    Number of young generation GC Events.
YGCT	Young generation garbage collection time.
FGC	    Number of full GC events.
FGCT	Full garbage collection time.
GCT	    Total garbage collection time.
*/
```

#####	Show statistics of the capacities of the generations and their corresponding spaces.
```
jstat -gccapacity 14958
```
```c
/*
 NGCMN    NGCMX     NGC     S0C   S1C       EC      OGCMN      OGCMX       OGC         OC      PGCMN    PGCMX     PGC       PC     YGC    FGC
444736.0 445056.0 445056.0 55552.0 110464.0 224128.0   889536.0   890240.0   889536.0   889536.0  21248.0 262144.0  61824.0  61824.0      6     1
*/
```
```c
/*
NGCMN   Minimum new generation capacity (KB).
NGCMX   Maximum new generation capacity (KB).
NGC     Current new generation capacity (KB).
S0C	    Current survivor space 0 capacity (KB).
S1C	    Current survivor space 1 capacity (KB).
EC	    Current eden space capacity (KB).
OGCMN   Minimum old generation capacity (KB).
OGCMX   Maximum old generation capacity (KB).
OGC	    Current old generation capacity (KB).
OC	    Current old space capacity (KB).
PGCMN	Minimum permanent generation capacity (KB).
PGCMX	Maximum Permanent generation capacity (KB).
PGC	    Current Permanent generation capacity (KB).
PC	    Current Permanent space capacity (KB).
YGC	    Number of Young generation GC Events.
FGC	    Number of Full GC Events.
*/
```

##### Summary of Garbage Collection Statistics
```
jstat -gcutil 14958
```
```c
/*
S0    S1     E      O      P       YGC   YGCT    FGC  FGCT     GCT
0.00  50.32  19.63  12.88  99.84   7     0.982   1    0.327    1.309
*/
```
```c
/*
 S0     S1    E      O      P      YGC   YGCT    FGC  FGCT     GCT
 0.22   0.00  82.96  15.00  60.58  10    1.237   2    1.927    3.164
*/
```
```c
/*
 S0     S1     E     O      P      YGC   YGCT    FGC  FGCT     GCT
 0.00   100.00 3.66  15.00  60.58  11    1.246   2    1.927    3.173
*/
```
```c
/*
S0      Survivor space 0 utilization as a percentage of the space's current capacity.
S1	    Survivor space 1 utilization as a percentage of the space's current capacity.
E	    Eden space utilization as a percentage of the space's current capacity.
O	    Old space utilization as a percentage of the space's current capacity.
P	    Permanent space utilization as a percentage of the space's current capacity.
YGC	    Number of young generation GC events.
YGCT	Young generation garbage collection time.
FGC	    Number of full GC events.
FGCT    Full garbage collection time.
GCT	    Total garbage collection time.
*/
```

##### Take 7 samples at 250 millisecond intervals and displays the output as specified by the -gcutil option
```
jstat -gcutil 14958 250 7
```
```c
/*
  S0     S1     E      O     P         YGC   YGCT      FGC  FGCT     GCT
  0.22   0.00   3.52  15.00  60.57     10    1.237     2    1.927    3.164
  0.22   0.00   3.52  15.00  60.57     10    1.237     2    1.927    3.164
  0.22   0.00   3.52  15.00  60.57     10    1.237     2    1.927    3.164
  0.22   0.00   3.52  15.00  60.57     10    1.237     2    1.927    3.164
  0.22   0.00   3.52  15.00  60.57     10    1.237     2    1.927    3.164
  0.22   0.00   3.52  15.00  60.57     10    1.237     2    1.927    3.164
  0.22   0.00   3.52  15.00  60.57     10    1.237     2    1.927    3.164
*/
```

##### Run jstat 30 times once a minute with the -gcutil output and a timestamp 
```
jstat -gcutil -t 14958 60000 15
```
```c
/*
Timestamp         S0     S1     E      O      P     YGC     YGCT    FGC    FGCT     GCT
         6953.8   0.00 100.00  26.82  15.00  60.58     11    1.246     2    1.927    3.173
         7013.8   0.00 100.00  30.40  15.00  60.58     11    1.246     2    1.927    3.173
         7073.7   0.00 100.00  34.02  15.00  60.58     11    1.246     2    1.927    3.173
         7133.8  37.61   0.00  12.40  16.84  67.30     14    1.490     2    1.927    3.417
         7193.8  37.61   0.00  22.72  16.84  67.43     14    1.490     2    1.927    3.417
         7253.8   0.00   0.00   3.25  18.14  60.41     15    1.575     3    2.947    4.522
         7313.7   0.00   0.00   7.03  18.14  60.41     15    1.575     3    2.947    4.522
         7373.7   0.00   0.00  10.73  18.14  60.41     15    1.575     3    2.947    4.522
         7433.8   0.00   0.00  77.21  18.14  64.66     15    1.575     3    2.947    4.522
         7493.8   0.00   0.00  85.91  18.14  64.75     15    1.575     3    2.947    4.522
         7553.8   0.00   0.00  92.28  18.14  64.80     15    1.575     3    2.947    4.522
         7613.8   0.00   0.00  99.70  18.14  64.82     15    1.575     3    2.947    4.522
         7673.8  25.47   0.00  18.01  18.14  64.93     16    1.662     3    2.947    4.610
         7733.8  25.47   0.00  22.41  18.14  64.93     16    1.662     3    2.947    4.610
         7793.8  25.47   0.00  42.55  18.14  65.05     16    1.662     3    2.947    4.610
*/
```


##### Display the same summary of garbage collection statistics as the -gcutil option and also include the causes of the last garbage collection event and (if applicable) the current garbage collection event
```
jstat -gccause 14958
```
```c
/*
  S0    S1      E     O      P      YGC  YGCT      FGC  FGCT     GCT    LGCC                 GCC
  0.00  50.32   7.76  12.88  99.84  7    0.982     1    0.327    1.309  Allocation Failure   No GC
*/
```
```c
/*
LGCC    Cause of last Garbage Collection.
GCC     Cause of current Garbage Collection.
*/
```

##### New Generation Statistics
```
jstat -gcnew 14958
```
```c
/*
S0C      S1C       S0U      S1U  TT MTT  DSS      EC       EU        YGC   YGCT
100864.0 104448.0  224.0    0.0  2  15   104448.0 236160.0 156715.0  10    1.237
*/
```
```c
/*
S0C	    Current survivor space 0 capacity (KB).
S1C	    Current survivor space 1 capacity (KB).
S0U	    Survivor space 0 utilization (KB).
S1U	    Survivor space 1 utilization (KB).
TT	    Tenuring threshold.
MTT	    Maximum tenuring threshold.
DSS	    Desired survivor size (KB).
EC	    Current eden space capacity (KB).
EU	    Eden space utilization (KB).
YGC	    Number of young generation GC events.
YGCT	Young generation garbage collection time.
*/
```

##### Old and Permanent Generation Statistics
```
jstat -gcold 12345
```
```c
/*
   PC       PU        OC          OU       YGC    FGC    FGCT     GCT
 61856.0  61715.2   3022848.0     44974.3      0     1    0.490    0.490
*/
```
```c
/*
PC      Current permanent space capacity (KB).
PU	    Permanent space utilization (KB).
OC	    Current old space capacity (KB).
OU	    old space utilization (KB).
YGC	    Number of young generation GC events.
FGC	    Number of full GC events.
FGCT	Full garbage collection time.
GCT	    Total garbage collection time.
*/
```

##### Show the old generation capacity (OGC) and the old space capacity (OC) increasing as the heap expands to meet allocation and/or promotion demands. 
```
jstat -gcoldcapacity 14958
```
```c
/*
   OGCMN       OGCMX        OGC         OC       YGC   FGC    FGCT     GCT
   889536.0    890240.0    889536.0    889536.0     6     1    0.327    1.180
*/
```
```c
/*
OGCMN	Minimum old generation capacity (KB).
OGCMX   Maximum old generation capacity (KB).
OGC	    Current old generation capacity (KB).
OC	    Current old space capacity (KB).
YGC     Number of young generation GC events.
FGC	    Number of full GC events.
FGCT    Full garbage collection time.
GCT	    Total garbage collection time.
*/
```

##### Show the new generation capacity  
```
jstat -gcnewcapacity 14958
```
```c
/*

*/
```
```c
/*
NGCMN   Minimum new generation capacity (KB).
NGCMX   Maximum new generation capacity (KB).
NGC     Current new generation capacity (KB).
S0CMX   Maximum survivor space 0 capacity (KB).
S0C	    Current survivor space 0 capacity (KB).
S1CMX   Maximum survivor space 1 capacity (KB).
S1C	    Current survivor space 1 capacity (KB).
ECMX    Maximum eden space capacity (KB).
EC	    Current eden space capacity (KB).
YGC	    Number of young generation GC events.
FGC	    Number of Full GC Events.
*/
```

### Download
##### Get a link to download the jvmstat 3.0 Maintenance Release
* http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-jvm-419420.html#jvmstat-3_0-mr-oth-JPR

##### Download jvmstat 3.0 Maintenance Release
```
cd ~/Downloads
wget http://download.oracle.com/otn-pub/java/jvmstat/3.0-mr/jvmstat-3_0.zip?AuthParam=SomeRandomCode
```

##### Unzip the package
```
unzip jvmstat-3_0.zip\?AuthParam\=SomeRandomCode
```
```c
/*
Archive:  jvmstat-3_0.zip?AuthParam=SomeRandomCode
   creating: jvmstat/
   creating: jvmstat/jars/
  inflating: jvmstat/jars/jvmstat_util.jar
  inflating: jvmstat/jars/jvmstat_graph.jar
  inflating: jvmstat/jars/visualgc.jar
   creating: jvmstat/bin/
  inflating: jvmstat/bin/visualgc
   creating: jvmstat/bat/
  inflating: jvmstat/bat/visualgc.cmd
   creating: jvmstat/etc/
  inflating: jvmstat/etc/linux.magic
  inflating: jvmstat/etc/solaris.magic
   creating: jvmstat/docs/
   creating: jvmstat/docs/images/
 extracting: jvmstat/docs/images/sunlogo64x30.gif
  inflating: jvmstat/docs/images/visualheap.jpg
  inflating: jvmstat/docs/images/visualgraph.jpg
 extracting: jvmstat/docs/images/javalogo52x88.gif
  inflating: jvmstat/docs/images/bullet-round.gif
  inflating: jvmstat/docs/index.html
   creating: jvmstat/docs/install/
  inflating: jvmstat/docs/install/solaris.html
  inflating: jvmstat/docs/install/windows.html
   creating: jvmstat/docs/instrumentation/
   creating: jvmstat/docs/instrumentation/1.4.1/
   creating: jvmstat/docs/instrumentation/1.4.2/
  inflating: jvmstat/docs/instrumentation/1.4.2/index.html
   creating: jvmstat/docs/instrumentation/5.0/
   creating: jvmstat/docs/tooldocs/
   creating: jvmstat/docs/tooldocs/solaris/
   creating: jvmstat/docs/tooldocs/linux/
   creating: jvmstat/docs/tooldocs/windows/
   creating: jvmstat/docs/tooldocs/share/
  inflating: jvmstat/docs/tooldocs/share/visualgc.html
  inflating: jvmstat/docs/tooldocs/share/notes.html
  inflating: jvmstat/docs/tooldocs/tools.html
  inflating: jvmstat/README
  inflating: jvmstat/LICENSE
*/
```
