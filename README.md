# drpin

1.build dynamorio
2.build drpin
3.using namespace dynamorio::droption
4.compile application

pinCMD
LaunchProcess

//////////////////////////////////////////////////////////////////This things might need to be included////////////////////////////////////////////////////////
aslr = conf.get<bool>("sim.aslr", false);
if (aslr) info("Not disabling ASLR, multiprocess runs will fail");

//Create children processes
pinCmd = new PinCmd(&conf, configFile, outputDir, shmid);
uint32_t numProcs = pinCmd->getNumCmdProcs();

for (uint32_t procIdx = 0; procIdx < numProcs; procIdx++) {
    LaunchProcess(procIdx);
}

if (numProcs == 0) panic("No process config found. Config file needs at least a process0 entry");
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////


ARGV: /work2/z50038971/dynamorio/clients/drpin/executables/../drpin/build/libdrpin.so
ARGV: --pintool
ARGV: ./obj-intel64-drpin/M000100_inscount0.so
ARGV: --pintool_op
ARGV: 
The determinant is: 14
Count 170117

ARGC: 5

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////[H] Starting zsim, built Thu Apr 18 18:52:20 CST 2024 (rev master:102:f524c05:7fc 56+ 17- 4504df90)
[H] Creating global segment, 1024 MBs
[H] Global segment shmid = 59441189
[H] Deadlock detection ON
Hello from PinCmd
numProcs: 2
1
2
CPID
1
2
CPID
2
3
2
3
4
5
6
7
8
9
10
/work2/z50038971/pin-2.14-71313-gcc.4.4.7-linux/intel64/bin/pinbin
-follow_execv
-tool_exit_timeout
1
-ifeellucky
-t
/work2/z50038971/zsim/build/opt/libzsim.so
-config
/work2/z50038971/zsim/tests/simple.cfg
-outputDir
/work2/z50038971/zsim
-shmid
59441189
-procIdx
0
--
pwd
4
5
6
7
8
9
10
/work2/z50038971/pin-2.14-71313-gcc.4.4.7-linux/intel64/bin/pinbin
-follow_execv
-tool_exit_timeout
1
-ifeellucky
-t
/work2/z50038971/zsim/build/opt/libzsim.so
-config
/work2/z50038971/zsim/tests/simple.cfg
-outputDir
/work2/z50038971/zsim
-shmid
59441189
-procIdx
1
--
ls
Hello from zsim.cpp
Hello from zsim.cpp
[S 1] Started instance
[S 0] Started instance
gm_Shmid: 59441189
gm_Shmid: 59441189
GM_BASE_ADDR: 0xabba000000
GM: 0xabba000000
GM_BASE_ADDR: 0xabba000000
GM: 0xabba000000
[S 0] Started RR scheduler, quantum=50 phases
Hello from PinCmd
[S 0] Initialized system
[S 0] HDF5 backend: Opening /work2/z50038971/zsim/zsim.h5
[S 0] HDF5 backend: Created table, 22624 bytes/record, 47 records/write
[S 0] HDF5 backend: Opening /work2/z50038971/zsim/zsim-ev.h5
[S 0] HDF5 backend: Created table, 22624 bytes/record, 6 records/write
[S 0] HDF5 backend: Opening /work2/z50038971/zsim/zsim-cmp.h5
[S 0] HDF5 backend: Created table, 2464 bytes/record, 1 records/write
[S 0] Initialization complete
[S 0] Started process, PID 43713
[S 0] procMask: 0x0
[S 0] [0] Adjusting clocks, domain 0, de-ffwd 0
[S 0] vDSO info initialized
[H] Attached to global heap
[S 1] Started process, PID 43714
[S 1] procMask: 0x400000000000000
[S 1] vDSO info initialized
[S 0] FF control Thread TID 43721
[S 0] Thread 0 starting
[S 0] Started contention simulation thread 0
[S 0] Started scheduler watchdog thread
[S 1] Thread 0 starting
[S 1] FF control Thread TID 43722
[S 0] Time slice ended, context-switched 1 threads, runQueue size 0, available 0
[S 0]  State:   0r
[S 1] Time slice ended, context-switched 1 threads, runQueue size 0, available 0
[S 1]  State:  65536r
/work2/z50038971/zsim
build  heartbeat  LICENSE  misc  out.cfg  pin.log  README.md  README.stats  SConstruct  src  tests  zsim-cmp.h5  zsim-ev.h5  zsim.h5  zsim.out
[H] Child 43714 done
[H] Child 43713 done
[H] All children done, exiting
