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
