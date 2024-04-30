1. In drpin/drpin/pin.cpp, added two function: INS_OprandIsAddressGenerator, INS_OperandReadOnly. These two functions are not mapped to the DynamoRio in drpin yet and zsim needs them, hence I simply wrote these two function in drpin and return false no matter what just for now, will complete them in the future.

2. In the same file pin.cpp. Author forgort to write a return in funcion INS_NEXT, resulting failure in zsim, so I added return here.

3. In zsim/SConstruct, I changed a lot.

4. In zsim/src/zsim_harness.cpp, I included a header file named <cstdlib>. Then, I wrote the followinig code so that it can set an environment variable SHMID equals to the shared memory id.
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
In the file zsim/src/zsim.cpp, it can retrieve the value of shared memory id by accessing to the environment variable SHMID.(I know it is a dumb method...)

5. In zsim/src/zsim.cpp, I included these code. It retrieves the shared memory id from the environment variable and attach to it.
```
    const char* str_shmid = getenv("SHMID");
    if (str_shmid == nullptr) {
        std::cerr << "Environment variable MY_VARIABLE is not set" << std::endl;
        return 1;
    }
    int int_shmid = std::stoi(str_shmid);
    gm_attach(int_shmid);
```
7. In zsim/src/zsim.cpp, I moved the whole delcaration of undordered map and other stuff related to vdso to the very beginning of the program, as there might be some issues with compiler or other factors that causing the program not recognising vdso unless I move the declarations.
```
// Initialization code and global per-process data

enum VdsoFunc {VF_CLOCK_GETTIME, VF_GETTIMEOFDAY, VF_TIME, VF_GETCPU};
extern bool INS_IsXend(INS ins);

static std::unordered_map<ADDRINT, VdsoFunc> vdsoEntryMap;
static uintptr_t vdsoStart;
static uintptr_t vdsoEnd;

//Used to warn
static uintptr_t vsyscallStart;
static uintptr_t vsyscallEnd;
static bool vsyscallWarned = false;

// Helper function from parse_vsdo.cpp
extern void vdso_init_from_sysinfo_ehdr(uintptr_t base);
extern void *vdso_sym(const char *version, const char *name);
```

8.There are other minor changes regarding to file paths will not be discussed here
