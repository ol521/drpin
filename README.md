1. In drpin/drpin/pin.cpp, added two function: INS_OprandIsAddressGenerator, INS_OperandReadOnly. These two functions are not mapped to the DynamoRio in drpin yet and zsim needs them, hence I simply wrote these two function in drpin and return false no matter what just for now, will complete them in the future.

2. In the same file pin.cpp. Arthur forgort to write a return in funcion INS_NEXT, resulting failure in zsim, so I added return here.

3. In zsim/SConstruct, I changed a lot.

4. In zsim/src/zsim_harness, I included a header file named <cstdlib>. Then,
```
    // Convert integer to string
    std::string str_shmid = std::to_string(shmid);

    // Set environment variable
    setenv("SHMID", str_shmid.c_str(), 1);
    const char* str_shmid2 = getenv("SHMID");
    if (str_shmid2 == nullptr) {
        std::cerr << "Environment variable MY_VARIABLE is not set" << std::endl;
        return 1;
    }
```
