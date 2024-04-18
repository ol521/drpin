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
