---
title: FPGA'26 Tutorial Contents
style: /_styles/presentations/fpga26/custom.css
---

# FPGA'26 Tutorial Step-by-step Flow

In this tutorial, we will familiarize ourselves with setting up CEDR and performing the following set of tasks:
- [Getting started](#exercise-0-getting-started-with-cedr) with and compiling CEDR
- **Core Exercise 1** (75 minutes)
  - **Part-1**
    - **Activity-1** [Introducing CEDR APIs](#exercise-1-1-1-introducing-cedr-apis-to-baseline-c-applications) into baseline C++ applications
    - **Activity-2** [Multiple application instance workloads](#exercise-1-1-2-multiple-application-instance-workloads) using different schedulers and hardware compositions
  - **Part-2**
    - **Activity-1** - [Integrating new API calls](#exercise-1-2-1-introducing-a-new-api-call) to CEDR by adding ZIP as an API
    - **Activity-2** - [Integrating new Accelerator](#exercise-1-2-2-introducing-a-new-accelerator) to CEDR and verify it on FPGA
- **Core Exercise 2** (30 minutes)
  - **Activity** [Performing DSE](#exercise-2-design-space-exploration) by varying the number of compute resources across different scheduling heuristics in dynamically arriving workload scenarios on UAP-ZU3 board.

Additionally, we provide a number of supplemental tutorials on topics such as:
- [Integrating and evaluating scheduling heuristics](#supplemental-exercise-1-integration-and-evaluation-of-eft-scheduler) with CEDR and conducting performance evaluation with dynamically arriving workload scenarios.
- [Performing experiments with many simultaneous applications](#supplemental-exercise-2-running-multiple-applications-with-cedr-on-x86)
- [Conducting GPU-based experiments](#supplemental-exercise-3-gpu-based-soc-experiment-nvidia-jetson-agx-xavier)

## Tutorial Requirements
- Ubuntu-based Linux machine or ability to run a [docker image](https://hub.docker.com/r/uofarcl/cedr/tags)
  * Choose one of the supported environments:
    * [Docker-based setup (Start on any platform without root access)](#option-1-docker-based-instructions-linux-windows-and-mac)
    * [Native Linux-based setup (Requires root access)](#option-2-linux-native-instructions-requires-root-access)
    * [WSL based setup for Windows](#option-3-wsl-for-windows)
- CEDR Source Files: [CEDR repository for this tutorial](https://github.com/UA-RCL/CEDR/), checked out to the `tutorial` branch.

# Exercise 0: Getting Started with CEDR
[Return to top](#fpga26-tutorial-step-by-step-flow)

## Initial Setup:
### Option 1: Docker-based Instructions (Linux, Windows, and Mac)
Install Docker based on the host machine platform using the [link](https://docs.docker.com/engine/install/#desktop).
Pull the latest [Docker container](https://hub.docker.com/r/uofarcl/cedr/tags) with all dependencies installed. 
Open a terminal and run the Docker image using the following command: 
```bash 
docker run -it --name cedr_tutorial uofarcl/cedr:tutorial_isfpga26 /bin/bash
```

Within the Docker container clone CEDR from GitHub using one of the following methods:
  * Clone with ssh:
```bash
git clone -b tutorial git@github.com:UA-RCL/CEDR.git
```
  * Clone with https:
```bash
git clone -b tutorial https://github.com/UA-RCL/CEDR.git
```

***After cloning CEDR from GitHub, you can move to [Building CEDR for x86](#building-cedr-for-x86). Following few lines shows simple `docker` comments that would be useful for the following tutorials.***

We will need to copy files from the container to the host machine. Use one of these alternatives for this: 
  * Mount a volume while running Docker using a folder on the host machine: 
```bash
docker run -it --name cedr_tutorial -v <host-folder>:/root/repository/share uofarcl/cedr:tutorial_isfpga26 /bin/bash
```
  * Using `docker cp` to copy files from the container to the host: 
```bash
docker ps -a # Find the Container ID and Name
docker cp cedr_tutorial:/root/repository/CEDR ./
```
  * If you need to detach from Docker at any time, you can use `Ctrl+p` and `Ctrl+q` to detach and to open a new shell for the same container use: 
```bash
docker exec -it cedr_tutorial /bin/bash
```
  * Using `docker start` to restart a stopped Docker container: 
```bash
docker start -ai cedr_tutorial
```
  * Save your changes locally to start a new image with saved changes: 
```bash
docker commit cedr_tutorial <new_image_name>:<new_tag> # Save changes in the current running image to create a new container
docker run -it --name my_cedr_dev <new_image_name>:<new_tag> /bin/bash # Start a new image with the updated changes
```

### Option 2: Linux-native instructions (Requires root access)
Install git using the following command:
```bash
sudo apt-get install git-all
```

Clone CEDR from GitHub using one of the following methods:
  * Clone with ssh:
```bash
git clone -b tutorial git@github.com:UA-RCL/CEDR.git
```
  * Clone with https:
```bash
git clone -b tutorial https://github.com/UA-RCL/CEDR.git
```

Change your working directory to the cloned CEDR folder
```bash
cd CEDR
```

Install all the required dependencies using the following command (this will take some time):
```bash
sudo bash install_dependencies.sh
pip3 install --no-cache-dir -r requirements.txt
```

***After installations are completed, you can move to [Building CEDR for x86](#building-cedr-for-x86).***

### Option 3: WSL for Windows

Download `Ubuntu 20.04` (The tutorial was tested with Ubuntu 20.04; Ubuntu 22.04 is also expected to work) for WSL from Microsoft store and start WSL.

Install git using the following command:
```bash
sudo apt-get install git-all
```

Clone CEDR from GitHub using one of the following methods:
  * Clone with ssh:
```bash
git clone -b tutorial git@github.com:UA-RCL/CEDR.git
```
  * Clone with https:
```bash
git clone -b tutorial https://github.com/UA-RCL/CEDR.git
```

Change your working directory to the cloned CEDR folder
```bash
cd CEDR
```

Install all the required dependencies using the following command (this will take some time):
```bash
sudo bash install_dependencies.sh
pip3 install --no-cache-dir -r requirements.txt
```

***After installations are completed, you can move to [Building CEDR for x86](#building-cedr-for-x86). Following few lines shows helper commands for WSL.***

Opening Windows explorer for the current folder you are in WSL, you may use:
```bash
explorer.exe .
```

Accessing your Windows folders from WSL you can use the following pathing:
```bash
ls /mnt/c/
```

## Building CEDR for x86:

Navigate to the [root directory](https://github.com/UA-RCL/CEDR/tree/tutorial) and create a build folder
```bash
mkdir build
```
Change the current directory to build
```bash
cd build
```
Call cmake and make to create CEDR executables for x86. You can leave `$(nproc)` empty (`make -j`) or set it equal to the number of cores you have on the host machine (i.e., `make -j 12` for a 12 CPU core machine).
```bash
cmake ../
make -j $(nproc)
```
At this point, there are 4 important files that should be compiled:
 - *cedr:* CEDR runtime daemon
 - *sub_dag:* CEDR job submission process
 - *kill_daemon:* CEDR termination process
 - *libdash-rt/libdash-rt.so:* Shared object used by CEDR for API calls

Look into [dash.h](https://github.com/UA-RCL/CEDR/tree/tutorial/libdash/dash.h) under [libdash](https://github.com/UA-RCL/CEDR/tree/tutorial/libdash) folder and see available API calls.

# Exercise 1-1-1: Introducing CEDR APIs to Baseline C++ Applications
[Return to top](#fpga26-tutorial-step-by-step-flow)

## Application Overview

Move to the Radar Correlator folder in the [applications](https://github.com/UA-RCL/CEDR/tree/tutorial/applications/APIApps/radar_correlator/) folder from [root directory](https://github.com/UA-RCL/CEDR/tree/tutorial/)
```bash
cd applications/APIApps/radar_correlator
```

Look at the [non-API version](https://github.com/UA-RCL/CEDR/tree/tutorial/applications/APIApps/radar_correlator/radar_correlator_non_api.c) of the Radar Correlator and locate possible places for adding API calls to the application
 - Forward FFT call: Line 146
 - Forward FFT call: Line 167
 - Inverse FFT call: Line 194

Create a new file to place the API calls in the file and change the radar correlator to have DASH_FFT API calls.
```bash
cp radar_correlator_non_api.c radar_correlator_fft.c
```
    
Make sure the [dash.h](https://github.com/UA-RCL/CEDR/tree/tutorial/libdash/dash.h) is included in the application
```c
#include "dash.h"
```

Change the `radar_correlator_fft.c` to include `DASH_FFT` calls
```c
<gsl_fft_wrapper(fft_inp, fft_out, len, true);;
>DASH_FFT_flt(fft_inp, fft_out, len, true);

<gsl_fft_wrapper(fft_inp, fft_out, len, true);;
>DASH_FFT_flt(fft_inp, fft_out, len, true);

<gsl_fft_wrapper(fft_inp, fft_out, len, false);
>DASH_FFT_flt(fft_inp, fft_out, len, false);
```

Build radar correlator without API calls and observe the output
```bash
make non-api
./radar_correlator_non_api-x86.out
```

Build radar correlator with API calls (standalone execution outside CEDR) and compare the output against non-api version
```bash
make standalone
./radar_correlator_fft-x86.out
```

Build radar correlator shared object to be used with CEDR
```bash
make api
```

Copy the shared object and any input data files to the CEDR build folder
```bash
cp radar_correlator_fft-x86.so ../../../build
cp -r input/ ../../../build
``` 

## CPU-based Preliminary Validation of the API Based Code

Move back to the CEDR build folder containing CEDR binaries
```bash
cd ../../../build
```

Copy the daemon configuration file from the [root repository](https://github.com/UA-RCL/CEDR/tree/tutorial/./) base directory to the build folder
```bash
cp ../daemon_config.json ./
```

Observe the contents of the `daemon_config.json`
  * *Worker Threads*: Specify the number of PEs for each resource
  * *Features*: Enable/Disable CEDR features
    * *Cache Schedules*: Enable/**Disable** schedule caching
    * *Enable Queueing*: **Enable**/Disable Queueing
    * *Use PAPI*: Enable/**Disable** PAPI based performance counters
    * *Loosen Thread Permissions*: Thread permission setup (**Enable**/Disable)
    * *Fixed Periodic Injection*: Inject jobs with fixed injection rate
    * *Exit When Idle*: Kill CEDR once the all running applications are terminated
  * *Scheduler*: Type of scheduler to use (SIMPLE, RANDOM, EFT, ETF, MET, or HEFT_RT)
  * *Random Seed*: Seed to be used on random operations
  * *DASH Binary Path*: List of paths to the libdash shared objects

Modify the `daemon_config.json` file to set the number of CPUs to 3 (or any other number).

```
"Worker Threads": {
  "cpu": <b>3</b>,
  "fft": 0,
  "gemm": 0,
  "gpu": 0
},
```

Run CEDR using the config file
```bash
./cedr -c ./daemon_config.json
```

Push CEDR to the background or open another terminal and navigate to the same build folder ([root repository](https://github.com/UA-RCL/CEDR/tree/tutorial/)/build)
  * Option 1: Ctrl+z or run CEDR with `./cedr -c ./daemon_config.json &` in the previous step. Now this terminal can be used for running next steps.
  * Option 2: Open a second terminal and go to CEDR build directory, <code>cd ${repo_root}/build</code>. Now this second terminal can be used for running next steps.

Run `sub_dag` to submit application(s) to CEDR

```bash
./sub_dag -a ./radar_correlator_fft-x86.so -n 1 -p 0
```

  * We use `-a` to specify the application shared object to be submitted
  * We use `-n` to specify the number of instances that are to be submitted
  * We use `-p` to specify the injection rate (waiting period between two instances in microsecond unit) when `-n` is more than 1
    * This is an optional argument, if not set it will be set to 0 by default

Look at the results and terminate CEDR using `kill_daemon`

```bash
./kill_daemon
```

Now, observe the log files generated in `log_dir/experiment0`. 
* `appruntime_trace.log` stores the execution time of the application.
* `schedule_trace.log` tracks the ready queue size and overhead of each scheduling decision.
* `timing_trace.log` stores the computing resource and execution time of the API call.

We can generate a Gantt chart showing the distribution of tasks to the processing elements. Navigate the [scripts folder](https://github.com/UA-RCL/CEDR/tree/tutorial/./) and run `gantt_k-nk.py` script.

```bash
cd ../scripts/
python3 gantt_k-nk.py ../build/log_dir/experiment0/timing_trace.log
```

Having built CEDR and compiled radar correlator application, we can proceed to performing design-space exploration now. 

# Exercise 1-1-2: Multiple Application Instance Workloads
[Return to top](#fpga26-tutorial-step-by-step-flow)

## Multiple Applications
While in the build folder, run CEDR again using the config file
```bash
cd ../build
./cedr -c ./daemon_config.json &
```

Run `sub_dag` to submit applications to CEDR, this time using `-n 10` to submit 10 radar correlators and terminate CEDR using `kill_daemon`.

```bash
./sub_dag -a ./radar_correlator_fft-x86.so -n 10 -p 0
./kill_daemon
```

In this exercise we will be generating multiple Gantt charts for each step, as we change the configurations. After each step we will rename the generated Gantt chart based on the corresponding experiment.

```bash
python3 ../scripts/gantt_k-nk.py ./log_dir/experiment1/timing_trace.log
mv gantt.png gantt_10rc.png
```

## Multiple Applications with Injection Rates
While in the build folder, run CEDR again using the config file we can use `-l NONE` logging option to disable CEDR based logging prints on the terminal.
```bash
./cedr -c ./daemon_config.json -l NONE &
```

Run `sub_dag` to submit applications to CEDR, this time using `-n 10` with `-p 100000` to submit 10 radar correlators with 100ms delays between each instance and terminate CEDR using `kill_daemon`. Make sure you wait for all 10 instances to complete before running `kill_daemon` and generate the Gantt chart. 

```bash
./sub_dag -a ./radar_correlator_fft-x86.so -n 10 -p 100000
./kill_daemon
python3 ../scripts/gantt_k-nk.py ./log_dir/experiment2/timing_trace.log
mv gantt.png gantt_10rc_100ms.png
```

## Changing Hardware Composition
Until now, we have been using 3 CPUs. This time we will use 5 CPUs and run the same experiment. Modify the `daemon_config.json` file to set the number of CPUs to 5.

```
"Worker Threads": {
  "cpu": <b>5</b>,
  "fft": 0,
  "gemm": 0,
  "gpu": 0
},
```

While in the build folder, run CEDR again. Run `sub_dag` to submit applications to CEDR, this time using `-n 10` with `-p 100000` to submit 10 radar correlators with 100ms delays between each instance and terminate CEDR using `kill_daemon`. Make sure you wait for all 10 instances to complete before running `kill_daemon` and generate the Gantt chart. 

```bash
./cedr -c ./daemon_config.json -l NONE &
./sub_dag -a ./radar_correlator_fft-x86.so -n 10 -p 100000
./kill_daemon
python3 ../scripts/gantt_k-nk.py ./log_dir/experiment3/timing_trace.log
mv gantt.png gantt_10rc_100ms_5CPU.png
```

## Chaning the scheduler
Until now, we have been using Round Robin scheduler. This time we will run the same experiment using `ETF` scheduler. Modify the `daemon_config.json` file to set scheduler as `ETF`.

```
"Scheduler": "ETF",
```

While in the build folder, run CEDR again. Run `sub_dag` to submit applications to CEDR, this time using `-n 10` with `-p 100000` to submit 10 radar correlators with 100ms delays between each instance and terminate CEDR using `kill_daemon`. Make sure you wait for all 10 instances to complete before running `kill_daemon` and generate the Gantt chart. 

```bash
./cedr -c ./daemon_config.json -l NONE &
./sub_dag -a ./radar_correlator_fft-x86.so -n 10 -p 100000
./kill_daemon
python3 ../scripts/gantt_k-nk.py ./log_dir/experiment4/timing_trace.log
mv gantt.png gantt_10rc_100ms_5CPU_ETF.png
```

## Verification of Changes
After each step or once all is done you can see the how the changes are effecting the execution of the applications looking at the generated Gantt charts.

# Exercise 1-2-1: Introducing a New API Call
[Return to top](#fpga26-tutorial-step-by-step-flow)

In this section of the tutorial, we will demonstrate integration of a new API call to the CEDR. We will use `DASH_ZIP` API call as an example. 

Navigate to libdash folder from [root directory](https://github.com/UA-RCL/CEDR/tree/tutorial/./).
```bash
cd ../libdash
```

Add the API function definitions to the `dash.h`.

```c
void DASH_ZIP_flt(dash_cmplx_flt_type* input_1, dash_cmplx_flt_type* input_2, dash_cmplx_flt_type* output, size_t size, zip_op_t op);
void DASH_ZIP_flt_nb(dash_cmplx_flt_type** input_1, dash_cmplx_flt_type** input_2, dash_cmplx_flt_type** output, size_t* size, zip_op_t* op, cedr_barrier_t* kernel_barrier);

void DASH_ZIP_int(dash_cmplx_int_type* input_1, dash_cmplx_int_type* input_2, dash_cmplx_int_type* output, size_t size, zip_op_t op);
void DASH_ZIP_int_nb(dash_cmplx_int_type** input_1, dash_cmplx_int_type** input_2, dash_cmplx_int_type** output, size_t* size, zip_op_t* op, cedr_barrier_t* kernel_barrier);
```

There 4 different function definitions here:
  1. DASH_ZIP_flt: Supports blocking ZIP calls for `dash_cmplx_flt_type`
  2. DASH_ZIP_flt_nb: Supports non-blocking ZIP calls for `dash_cmplx_flt_type`
  3. DASH_ZIP_int: Supports blocking ZIP calls for `dash_cmplx_int_type`
  4. DASH_ZIP_int_nb: Supports non-blocking ZIP calls for `dash_cmplx_int_type`

Add supported ZIP operation enums to `dash_types.h`
```c
typedef enum zip_op {
  ZIP_ADD = 0,
  ZIP_SUB = 1,
  ZIP_MULT = 2,
  ZIP_DIV = 3
} zip_op_t;
```

Add CPU implementation of the ZIP to [libdash/cpu](https://github.com/UA-RCL/CEDR/tree/tutorial/libdash/cpu/) `zip.cpp`. For simplicity, we just copy the original implementation.
```bash
cp ../original_files/zip.cpp cpu/
```

In `zip.cpp`, we also have the `enqueue_kernel` call in the API definition, which is how the task for this API will be sent to CEDR. A prototype of the `enqueue_kernel` function is given in line 12, and `enqueue_kernel` is used in non-blocking versions of the function (lines 83 and 113). The prototype is the same for all the APIs created for CEDR. The first argument has to be the function name, the second argument has to be the precision to be used, and the third argument shows how many inputs are needed for the calling function (for ZIP, this is 6). Now let's look at the ZIP-specific `enqueue_kernel` call on line 83.

```c
enqueue_kernel("DASH_ZIP", "flt", 6, input_1, input_2, output, size, op, kernel_barrier);
```

In this sample `enqueue kernel` call, we have 4 important portions:
  * ***"DASH_ZIP"***: Name of the API call
  * ***"flt"***: Type of the inputs on the API call
  * ***6***: Number of variables for the API call
  * Variables:
    * ***input_1***: First input of the ZIP
    * ***input_2***: Second input of the ZIP
    * ***output***: Output of the ZIP
    * ***size***: Array size for inputs and output
    * ***op***: ZIP operation type (ADD, SUB, MUL, or DIV)
    * ***kernel_barrier***: Contains configuration information of barriers for blocking and non-blocking implementation

In the `zip.cpp`, we need to fill the bodies of the four function definitions that are used so the application will call `enqueue_kernel` properly and hand off the task to CEDR for scheduling:

1. DASH_ZIP_flt
2. DASH_ZIP_flt_nb
3. DASH_ZIP_int
4. DASH_ZIP_int_nb

We also implement two more functions, which contains implementation of CPU-based ZIP operations. Functions are created with `_cpu` suffix so that CEDR can identify the functions correctly for CPU execution:

1. DASH_ZIP_flt_cpu: `dash_cmplx_flt_type`
2. DASH_ZIP_int_cpu: `dash_cmplx_int_type`

Having included API implementation, we should introduce the new API call to the system by updating CEDR header file ([./src-api/include/header.hpp](https://github.com/UA-RCL/CEDR/tree/tutorial/src-api/include/header.hpp)):

```
enum api_types {DASH_FFT = 0, DASH_GEMM = 1, DASH_FIR = 2, DASH_SpectralOpening = 3, DASH_CIC = 4, DASH_BPSK = 5, DASH_QAM16 = 6, DASH_CONV_2D = 7, DASH_CONV_1D = 8, <b>DASH_ZIP = 9,</b> NUM_API_TYPES = <b>10</b>};

static const char *api_type_names[] = {"DASH_FFT", "DASH_GEMM", "DASH_FIR", "DASH_SpectralOpening", "DASH_CIC", "DASH_BPSK", "DASH_QAM16", "DASH_CONV_2D", "DASH_CONV_1D"<b>, "DASH_ZIP"</b>};
...
static const std::map<std::string, api_types> api_types_map = { {api_type_names[api_types::DASH_FFT], api_types::DASH_FFT},
                                                                {api_type_names[api_types::DASH_GEMM], api_types::DASH_GEMM},
                                                                {api_type_names[api_types::DASH_FIR], api_types::DASH_FIR},
                                                                {api_type_names[api_types::DASH_SpectralOpening], api_types::DASH_SpectralOpening},
                                                                {api_type_names[api_types::DASH_CIC], api_types::DASH_CIC},
                                                                {api_type_names[api_types::DASH_BPSK], api_types::DASH_BPSK},
                                                                {api_type_names[api_types::DASH_QAM16], api_types::DASH_QAM16},
                                                                {api_type_names[api_types::DASH_CONV_2D], api_types::DASH_CONV_2D},
                                                                {api_type_names[api_types::DASH_CONV_1D], api_types::DASH_CONV_1D},
                                                              <b>{api_type_names[api_types::DASH_ZIP], api_types::DASH_ZIP}</b>};
```

## Building CEDR with ZIP API
Navigate to the build folder, re-generate the files, and check the `libdash-rt.so` shared object to verify the new ZIP-based function calls.
```bash
cd ../build
nm -D libdash-rt/libdash-rt.so | grep -E '*_ZIP_*'
cmake ..
make -j $(nproc)
nm -D libdash-rt/libdash-rt.so | grep -E '*_ZIP_*'
```

## Modify Radar Correlator to Include ZIP API
After re-building CEDR with ZIP API, move to the Radar Correlator folder in the [applications](https://github.com/UA-RCL/CEDR/tree/tutorial/applications/APIApps/radar_correlator/)
```bash
cd ../applications/APIApps/radar_correlator
```

Create a new file to place the API calls in the file and change the radar correlator to have DASH_FFT API calls
```bash
cp radar_correlator_fft.c radar_correlator_zip.c
```

Look at the [non-API version](https://github.com/UA-RCL/CEDR/tree/tutorial/applications/APIApps/radar_correlator/radar_correlator_non_api.c) of the Radar Correlator and locate possible places for adding ZIP API calls to the application
 - Multiplication: Lines 173 to 176

Change the `radar_correlator_zip.c` to include `DASH_ZIP` calls
```c
/* Remove */
    for (i = 0; i < 2 * len; i += 2) {
      corr_freq[i] = (X1[i] * X2[i]) + (X1[i + 1] * X2[i + 1]);
      corr_freq[i + 1] = (X1[i + 1] * X2[i]) - (X1[i] * X2[i + 1]);
    }

/* Add */
    dash_cmplx_flt_type *zip_inp0 = (dash_cmplx_flt_type*) malloc(len * sizeof(dash_cmplx_flt_type));
    dash_cmplx_flt_type *zip_inp1 = (dash_cmplx_flt_type*) malloc(len * sizeof(dash_cmplx_flt_type));
    dash_cmplx_flt_type *zip_out = (dash_cmplx_flt_type*) malloc(len * sizeof(dash_cmplx_flt_type));
    for (size_t i = 0; i < len; i++) {
      zip_inp0[i].re = (dash_re_flt_type) X1[2*i];
      zip_inp0[i].im = (dash_re_flt_type) X1[2*i+1];
      zip_inp1[i].re = (dash_re_flt_type) X2[2*i];
      zip_inp1[i].im = (dash_re_flt_type) -X2[2*i+1]; // Conj Multiplication
    }
    DASH_ZIP_flt(zip_inp0, zip_inp1, zip_out, len, ZIP_MULT);
    for (size_t i = 0; i < len; i++) {
      corr_freq[2*i]   = (double) zip_out[i].re;
      corr_freq[2*i+1] = (double) zip_out[i].im;
    }
```

Build radar correlator with ZIP API calls, standalone as well as the shared object, and compare the output against other versions
```bash
make zip
./radar_correlator_zip-x86.out
```

Copy the shared object to the CEDR build folder change back to default config file, and run `cedr`, `sub_dag`, and `kill_daemon`.
```bash
cp radar_correlator_zip-x86.so ../../../build
cd ../../../build
cp ../daemon_config.json ./
./cedr -c ./daemon_config.json & # With print logs enabled, you can see `DASH_ZIP` API being located by CEDR now
./sub_dag -a ./radar_correlator_zip-x86.so -n 1 -p 0 # Verifiy the output!
./kill_daemon
```

Let's check the `timing_trace.log` for ZIP API calls.
```bash
cat log_dir/experiment5/timing_trace.log | grep -E '*ZIP*'
```
# Exercise 1-2-2: Introducing a New Accelerator
Before starting with new accelerator integration we will go through the cross compilation of CEDR and application for AUP-ZU3.

## FPGA Based SoC Experiment (AUP-ZU3)
[Return to top](#fpga26-tutorial-step-by-step-flow)

Moving on to the aarch64-based build for AUP-ZU3 FPGA with accelerators. We'll start by building CEDR itself. This time we will use the [toolchain](https://github.com/UA-RCL/CEDR/tree/tutorial/toolchains/aarch64-linux-gnu.toolchain.cmake) file for cross-compilation. If you are on Ubuntu 22.04, the toolchain requires running inside the docker container.
Simply run the following commands from the repository root folder:

```bash
cd ../
mkdir build-arm
cd build-arm
cmake -DLIBDASH_MODULES="FFT" --toolchain=../toolchains/aarch64-linux-gnu.toolchain.cmake ..
make -j $(nproc)
```

This will create an executable file for `cedr`, `sub_dag`, `kill_deamon`, and `libdash-rt` for aarch64 platforms. We can check the platform type of an executable using the `file` command:

```bash
file cedr
```
```
cedr: ELF 64-bit LSB pie executable, <b>ARM aarch64</b>, version 1 (GNU/Linux), dynamically linked, interpreter /lib/ld-linux-aarch64.so.1, BuildID[sha1]=c5913bcbf311f3df59cd3b7e3063856908cee207, for GNU/Linux 3.7.0, not stripped
```

Since we also used the `-DLIBDASH_MODULES="FFT"` flag, we also enabled FFT accelerator function calls for `DASH_FFT` API calls. We can test if these functions are available or not by running the following commands:

```bash
nm -D libdash-rt/libdash-rt.so | grep -E '*_fft$'
```
```
000057e1 T DASH_FFT_flt_fft
0000588f T DASH_FFT_int_fft
```

After this, we can go to build our application using cross-compilation for aarch64. 

## ZIP acceleretor Integration
Due to the overhead associated with SD Card based file transfor overheads, we will also include ZIP accelerator before moving on to the testing on the AUP-ZU3.

### Adding ZIP as Resource to CEDR

Update the CEDR header file ([./src-api/include/header.hpp](https://github.com/UA-RCL/CEDR/tree/tutorial/src-api/include/header.hpp)) to include zip as a resource by updating the following lines:

```
enum resource_type { cpu = 0, fft = 1, mmult = 2, gpu = 3, <b>zip = 4, NUM_RESOURCE_TYPES = 5 </b>};
static const char *resource_type_names[] = {"cpu", "fft", "gemm", "gpu"<b>, "zip"</b>};
static const std::map<std::string, resource_type> resource_type_map = {
                                                                       {resource_type_names[(uint8_t) resource_type::cpu], resource_type::cpu},
                                                                       {resource_type_names[(uint8_t) resource_type::fft], resource_type::fft},
                                                                       {resource_type_names[(uint8_t) resource_type::mmult], resource_type::mmult},
                                                                       {resource_type_names[(uint8_t) resource_type::gpu], resource_type::gpu}<b>,
                                                                       {resource_type_names[(uint8_t) resource_type::zip], resource_type::zip}</b>};
```

These lines makes sure the functions with `_zip` suffix are grabbed when CEDR starts and used when schedulers assigns tasks to ZIP accelerator.

### Accelerator Source File

Add accelerator implementation of the ZIP to [libdash/zip](https://github.com/UA-RCL/CEDR/tree/tutorial/libdash/). For simplicity, we just copy the original implementation.
```bash
cp -r ../original_files/zip_AUP-ZU3 ../libdash/zip
```

In the `libdash/zip/zip.cpp`, there is a `DASH_ZIP_flt_zip` function call. The version `DASH_ZIP_flt_cpu` we added in [Integrating new API calls](#exercise-1-2-1-introducing-a-new-api-call) was specifically for using the `cpu` resource while `_zip` suffix is the version that will be used when ZIP accelerator is used as a resource. The `DASH_ZIP_flt_zip` functions handles the input size limitations and data: type converstion and calls another function called `zip_accel` which handles the data transfers and signalling the ZIP accelerator to start execution. Looking deeper inthe function:

* ***config_zip_op(zip_control_base, op)***: Sets the ZIP operation as `op` (ADD/SUB/MULT/DIV)
* ***config_zip_size(zip_control_base, size)***: Sets the ZIP size as `size`
* ***memcpy((float\* ) udmabuf_base, input0, 2\*size \* sizeof(float))***: Sends the first input to UDMA for ZIP to use
* ***memcpy((float\* ) udmabuf_base+(2\*size), input1, 2\*size \* sizeof(float))***: Sends the second input to UDMA for ZIP to use
* ***setup_rx(dma_control_base, udmabuf_phys + (4 \* size \* sizeof(float)), 2\*size \* sizeof(float))***: Sets the return address for ZIP accelerator to put the output
* ***setup_tx(dma_control_base, udmabuf_phys, 4 \* size \* sizeof(float))***: Sets the input address for ZIP accelerator to start reading the input from
* ***zip_write_reg***: Starts the execution of ZIP accelerator
* ***dma_wait_for_rx_complete***: Waits for ZIP accelerator to complete writing the output
* ***memcpy(output, &(((float\*)udmabuf_base)[4 \* size]), 2 \* size \* sizeof(float))***: Copies the output back

These are some of the main steps for adding a new accelator to CEDR.

We also need to make sure `CMakeLists.txt` under `libdash` folder looks for ZIP as an accelerator as well. Update following line (19) in [libdash/CMakeLists.txt](https://github.com/UA-RCL/CEDR/tree/tutorial/libdash/CMakeLists.txt)
```
  set(ALL_LIBDASH_MODULES FFT GEMM GPU ZIP)
```

### Building CEDR with ZIP

In `build-arm` folder run the following steps to rebuild CEDR with ZIP as an accelerator.

```bash
rm -rf ./* # This can be skipped, used for showing fresh start of cmake with new accelerator
cmake -DLIBDASH_MODULES="FFT ZIP" --toolchain=../toolchains/aarch64-linux-gnu.toolchain.cmake ..
make -j
```

Now verifiy the functions with `_zip` suffix that are used for ZIP accelerator.

```bash
nm -D libdash-rt/libdash-rt.so | grep -E '*_zip$'
```

```
000065c5 T <b>DASH_ZIP_flt_zip</b>
```

### Application Cross-compilation

First, navigate to [applications/APIApps/radar_correlator](https://github.com/UA-RCL/CEDR/tree/tutorial/applications/APIApps/radar_correlator) folder. Then run the following command to build the executable for aarch64:

```bash
cd ../applications/APIApps/radar_correlator
ARCH=aarch64 make zip
file radar_correlator_zip-aarch64.so
```
```
radar_correlator_zip-aarch64.so: ELF 64-bit LSB shared object, ARM aarch64, version 1 (SYSV), dynamically linked, BuildID[sha1]=f86ca08b59c2769a26d2b236731e163ee8e0ba1f, not stripped
```

After verifying the file is compiled for the correct platform, copy the file and inputs to the build directory:

```bash
# Assuming your CEDR build folder is in the root directory and named "build-arm"
cp -r radar_correlator_zip-aarch64.{so,out} input/ ../../../build-arm
```

### Running CEDR on AUP-ZU3

Now, change your working directory to the `build-arm` directory. Before going into the AUP-ZU3 first copy the [daemon_config.json](https://github.com/UA-RCL/CEDR/tree/tutorial/daemon_config.json) file to the `build-arm` directory and create an output folder.

```bash
cd ../../../build-arm
cp ../daemon_config.json ./
ls
```

Now we will copy our files to AUP-ZU3, and enter the password `root` when prompted. Assuming using Docker, copy the `CEDR/build-arm` folder to the host machine. While we only need handful of files to actually run CEDR and Radar Correlator application, we will copy everything under `build-arm` to the SD Card's `System` partition. Running on the host machine:

```bash
docker cp <container_name>:/root/repository/CEDR/build-arm ./ # Run if using Docker
cp -r ./build-arm <path_to_external_drive>
``` 

After these steps are completed, remove the SD Card from the host machine and attach it to the AUP-ZU3 and turn on the AUP-ZU3. Using any serial communication tool like `Putty`, `screen`, or `minicom`, watch AUP-ZU3 as it boots and enter username and password as `root` when promted. After botting the board, navigate to System partition of the SD Card and after typing `ls` you should see all the files you copied on the AUP-ZU3.

```bash
screen /dev/ttyACM0 115200
Username: petalinux
Password: <set any password- it can be as simple as 1234>
# Find the USB path:
ls -al /run/media # or df -H
cp -r <USB_PATH>/build-arm ./ # Might need to run with sudo
# If needed sudo to copy run below commented line
# sudo chown -R petalinux:petalinux build-arm/
cd build-arm
ls
```

Before running CEDR, we need to enable FFT accelerator in the [daemon_config.json](https://github.com/UA-RCL/CEDR/tree/tutorial/daemon_config.json) file. By the time this tutorial was written, we had 2 FFT accelerators available in the FPGA image. We can put any number between 0-2 to the corresponding fields on the [daemon_config.json](https://github.com/UA-RCL/CEDR/tree/tutorial/daemon_config.json) file. Change the file with the following `Worker Threads` setup:

```json
"Worker Threads": {
        "cpu": 3,
        "fft": 2,
        "gemm": 0,
        "gpu": 0
    },
```
Execution of CEDR is the same as the x86_64 version. In one terminal launch CEDR:

```bash
sudo ./cedr -c ./daemon_config.json &
```
After launching CEDR, you should see the function handles for FFT accelerators are successfully grabbed.

In another terminal, we will submit 5 instances of `radar_correlator` using `sub_dag` and check the outputs:

```bash
sudo ./sub_dag -a ./radar_correlator_zip-aarch64.so -n 5 -p 0
```

Now kill CEDR by running `./kill_deamon` and check the `resource_name` fields for the first 10 APIs:

```bash
sudo ./kill_daemon
head -n 10 ./log_dir/experiment0/timing_trace.log
```

We can see that all the resources available for FFT execution (`cpu1`, `cpu2`, `cpu3`, `fft1`, and `fft2`) are being used and ZIP is only using CPU (`cpu1`, `cpu2`, or `cpu3`) for execution.

### Using the ZIP Accelerator
Now we can also test the newly added accelerator based ZIP implementation. Modify the `daemon_config.json` file to set the number of ZIPs to 2.

```json
"Worker Threads": {
        "cpu": 3,
        "fft": 2,
        "zip": 2,
        "gemm": 0,
        "gpu": 0
    },
```

Re-run CEDR:
```bash
sudo ./cedr -c ./daemon_config.json &
```
After launching CEDR, you should see the function handles for ZIP accelerators are successfully grabbed along with FFTs.

Submit 5 instances of `radar_correlator` using `sub_dag`, check the outputs, kill CEDR using `./kill_deamon`, and check the `resource_name` fields for the first 10 APIs once again:
```bash
sudo ./sub_dag -a ./radar_correlator_zip-aarch64.so -n 5 -p 0
sudo ./kill_daemon
head -n 10 ./log_dir/experiment1/timing_trace.log
```

#### Gantts from AUP-ZU3 Experiments:
After running these experiments you can copy the `log_dir` folder from AUP-ZU3 back to USB and go back to the host machine, you will need to copy `timing_trace.log` files for both experiments, and plot the Gantts using the same setup as before. The Gantt of `experiment0` will only show 3CPU and 2FFTs in use while `experiment1` will show 3CPU, 2FFTs, and 2ZIPs in use.

```bash
# On the Board
sudo cp -r ./log_dir <USB_PATH>/build-arm/
sudo umount <USB_PATH>
# After moving the USB to Host
cp -r <USB_PATH>/build-arm/log_dir build-arm/
cd build-arm
python3 ../scripts/gantt_k-nk.py ./log_dir/experiment0/timing_trace.log
mv gantt.png gantt_FFT.png
python3 ../scripts/gantt_k-nk.py ./log_dir/experiment1/timing_trace.log
mv gantt.png gantt_FFT_ZIP.png
```

## Exercise 2: Design Space Exploration
[Return to top](#fpga26-tutorial-step-by-step-flow)

CEDR includes scripts that enable rapid, easy design-space exploration (DSE). Now, we will go over the flow and define how to perform DSE step-by-step. First, navigate to the folder where we accommodate [DSE scripts](https://github.com/UA-RCL/CEDR/tree/tutorial/scripts/DSE).

```bash
cd ../scripts/DSE
```

First, we will look into a helper script [generate_daemon_config.sh](https://github.com/UA-RCL/CEDR/tree/tutorial/scripts/DSE/generate_daemon_config.sh), which generates `daemon_config.json` files for our sweeps. It uses the arguments given to the script to generate the corresponding `daemon_config.json` file. For each configuration, our main script will call this script to re-generate the `daemon_config.json` file for the current configuration under testing.

```bash
bash generate_daemon_config.sh <number of CPUs> <number of FFTs> <number of ZIPs> <number of GEMMs> <number of GPUs> <number of Conv_2Ds> <scheduler_name>
```

Next, move to [main DSE script](https://github.com/UA-RCL/CEDR/tree/tutorial/scripts/DSE/run_sweep.sh) that runs `./cedr` and `./sub_dag`.In `run_sweep.sh`, we need to set a few fields based on what we want to sweep.

 * Line 7: Schedulers to be used in the sweep
 * Lines 8-13: Resources to be swept
 * Lines 17-18: Injection rate to be used with `sub_dag` when submitting applications
 * Line 20: Applications to be submitted
 * Line 21: Number of instances for the given application(s)
 * Lines 27-62: Main sweep loop
 * Line 39: Calls the helper script `generate_daemon_config.sh` with the current resource and scheduler under test. 

```bash
# Line 7:
declare -a SCHEDS=("SIMPLE" "MET" "ETF")

# Lines 8-13:
CPUS=3
FFTS=2
MMULTS=0
ZIPS=2
GPUS=0
CONV_2DS=0

# Lines 17-18:
PERIODCOUNT=2
PERIODS=("1734" "2313" )

# Line 20:
APPS=("./radar_correlator_zip-x86.so")

# Line 21:
INSTS=("5")

# Line 39:
bash generate_daemon_config.sh $cpu $fft $zip $mmult $gpu $conv_2d $sched
```

Looking at the script's details, we see that `cedr` is started on line 42. A 5-second delay is added on line 43 to let Cedr complete all required initializations. Once the delay is over, on line 44, `sub_dag` is used to submit applications to `cedr`. Line 45 waits for `cedr` to complete all the running applications and write the log files. Once `cedr` is complete and logs are written, line 47 moves the log files for use with plotting scripts.

#### Getting ready to run DSE on AUP-ZU3:

To get ready for the execution on AUP-ZU3 boards, we will first move to the [root directory](https://github.com/UA-RCL/CEDR/tree/tutorial/./), copy these DSE scripts to the `build-arm` folder, and clean any existing log files within the `build-arm` folder.

```bash
cd ../../
cp scripts/DSE/*.sh build-arm/
rm -rf build-arm/log_dir/ # Be careful when using `rm -rf`!
```

Next, we will move the `build-arm` folder again to the AUP-ZU3 board, following the same steps we used in [Exercise 1-2-2](#exercise-1-2-2-introducing-a-new-accelerator).

```bash
docker cp <container_name>:/root/repository/CEDR/build-arm ./build-arm-DSE # Run if using Docker
cp -r ./build-arm-DSE <path_to_external_drive>/build-arm-DSE

###############################
# Move USB to the AUP-ZU3 board
###############################

# Run on the AUP-ZU3 board:
cd ..
cp -r <USB_PATH>/build-arm-DSE ./ # Might need to run with sudo
# If needed sudo to copy run below commented line
# sudo chown -R petalinux:petalinux build-arm-DSE/
cd build-arm-DSE
ls
```

Now that we have everything we need to start DSE sweeps on AUP-ZU3 board, we will start the sweeps by simply running the `run_sweep.sh` script:

```bash
sudo bash run_sweep.sh
```

Once all the DSE is completed, move the log folder back to the USB for analysis on the host machine, following a similar command we used in [Exercise 1-2-2](#exercise-1-2-2-introducing-a-new-accelerator).


```bash
# On the Board
sudo cp -r ./log_dir <USB_PATH>/build-arm-DSE/
sudo umount <USB_PATH>

###############################
# Move USB to the Host machine
###############################

# On the Host machine
cp -r <USB_PATH>/build-arm-DSE/log_dir build-arm/
```

Inside the `log_dir` folder, there should be a folder named `HIGH` containing as many files as there are trials. Each folder should have log files for each hardware composition, scheduler, and injection rate. These logs will be used to plot all DSE results in 3D. We will now navigate to `scripts/scripts-API/` from [root directory](https://github.com/UA-RCL/CEDR/tree/tutorial/./).

```bash
cd scripts/scripts-API/
```

There are two scripts under [scripts/scripts-API/](https://github.com/UA-RCL/CEDR/tree/tutorial/scripts/scripts-API/) folder, named `makedataframe.py` and `plt3dplot_inj.py` that we will be using for plotting a 3D diagram. For each DSE experiment, the following lines in [makedataframe.py](https://github.com/UA-RCL/CEDR/tree/tutorial/scripts/scripts-API/makedataframe.py) should be modified as needed.

```python
corelist = [' cpu1', ' cpu2', ' cpu3', ' fft0', ' fft1', ' zip0', ' zip1']  # Line 38

############# Edit parameters here ####################
# Starting from line 179
CPUS=3
FFTS=2
MMULTS=0
ZIPS=2

SCHEDS=["SIMPLE", "MET", "ETF"]

if WORKLOAD == 'HIGH':
    # Use following INJ_RATES and PERIODS for High latency workload data
    INJ_RATES=[10, 20]
    PERIODS=[1734, 2313]
elif WORKLOAD == 'LOW':
    print('Low workload is not specified for this setup')
else:
    print('Wrong workload type ', WORKLOAD, ' chosen, please choose either "HIGH" or "LOW"!')
    exit()

INJ_COUNT=int(args.injectionRateCount)
TRIALS=int(args.trial)
corelist = [' cpu1', ' cpu2', ' cpu3', ' fft0', ' fft1', ' zip0', ' zip1']  # Edit here

#######################################################
```

To learn about the input arguments of `makedataframe.py`, execute the script with the `-h` option. Then, execute the `makedataframe.py` script using the given arguments below for the DSE experiment in this tutorial. Other DSE experiments may require different input arguments. 

```bash
python3 makedataframe.py -h
python3 makedataframe.py -i ../../build-arm/log_dir/ -w HIGH -o dataframe.csv -t 2 -r 2
```

Modify the following lines in the [plt3dplot_inj.py](https://github.com/UA-RCL/CEDR/tree/tutorial/scripts/scripts-API/plt3dplot_inj.py).

```python
### Configuration specification ###
### Starting from line 27
CPUS = 3
FFTS = 2
MMULTS = 0
ZIPS = 2
GPUS = 0
WORKLOAD = 'High'
TRIALS = 2
schedlist = {'SIMPLE':1, 'MET':2, 'ETF':3}
schedmarkerlist = {'SIMPLE':'o', 'MET':'o', 'ETF':'o'}
schednamelist = ['RR', 'MET', 'ETF']
```

Execute the script using the following commands. 

```bash
python3 plt3dplot_inj.py <input file name> <metric>
python3 plt3dplot_inj.py dataframe.csv CUMU  # Accumulates execution time of each API call
python3 plt3dplot_inj.py dataframe.csv EXEC  # Application execution time
python3 plt3dplot_inj.py dataframe.csv SCHED # Scheduling overhead
```

# Supplemental Exercises:

## Supplemental Exercise 1: Integration and Evaluation of EFT Scheduler
[Return to top](#fpga26-tutorial-step-by-step-flow)

Now navigate to [scheduler.cpp](https://github.com/UA-RCL/CEDR/tree/tutorial/scr-api/scheduler.cpp). This file contains various schedulers already tailored to work with CEDR. In this part of the tutorial, we will add the Earliest Finish Time(EFT) scheduler to CEDR. EFT heuristic schedules all the tasks in the `read queue` one by one based on the earliest expected finish time of the task on the available resources (processing elements -- PE). 

First, we will write the EFT scheduler as a C/C++ function. We will utilize the available variables for all the schedulers in CEDR. A list of the useful variables and their explanations can be found in the bulleted list below.

* cedr_config: Information about the current configuration of CEDR
* ready_queue: Tasks ready to be scheduled at the time of the scheduling event
* hardware_thread_handle: List of hardware threads that manages the available resources (PEs)
* resource_mutex: Mutex protection for the available resources (PEs)
* free_resource_count: Number of free resources (PEs) at the time of scheduling event, only useful if PE queues are disabled -- Not used in the tutorial

Based on the available variables, we will construct the prototype of the EFT scheduler as shown:

```c
int scheduleEFT(ConfigManager &cedr_config, std::deque<task_nodes *> &ready_queue, worker_thread *hardware_thread_handle, pthread_mutex_t *resource_mutex, uint32_t &free_resource_count)
```

Leveraging the available variables, we will implement the EFT in C/C++ step by step. First, we will handle the initializations, then the main loop body for task-to-PE mapping based on the heuristic, followed by the actual PE assignment for the task, and end with final checks. After implementing the scheduler, we will add the EFT scheduler as one of the schedulers for CEDR and enable it in the runtime config.

### Initialization

Here we will initialize some of the required fields for the EFT heuristic. We will use this function's start time as the reference current time while computing the expected finish time of a task on the PEs.

```c
  unsigned int tasks_scheduled = 0; // Number of tasks scheduled so far
  int eft_resource = 0; // ID of the PE that will be assigned to the task
  unsigned long long earliest_estimated_availtime = 0; // Estimated finish time initialization
  bool task_allocated; // Task assigned to PE successfully or not

  /* Get current time in nanosecond scale */
  struct timespec curr_timespec {};
  clock_gettime(CLOCK_MONOTONIC_RAW, &curr_timespec);
  long long curr_time = curr_timespec.tv_nsec + curr_timespec.tv_sec * SEC2NANOSEC;

  long long avail_time; // Current available time of the PEs
  long long task_exec_time; // Estimated execution time of the task

  unsigned int total_resources = cedr_config.getTotalResources(); // Total Number of PEs available
```


### EFT heuristic - Task-to-PE mapping

Here, we will have a double nested loop, where the outer loop will traverse all the tasks in the ready queue using the `ready_queue` variable. The inner loop will traverse all the PEs in the current runtime by indexing the `hardware_thread_handle`. 

```c
  // For loop to iterate over all tasks in Ready queue
  for (auto itr = ready_queue.begin(); itr != ready_queue.end();) {
    earliest_estimated_availtime = ULLONG_MAX;
    // For each task, iterate over all PEs to find the earliest finishing one
    for (int i = total_resources - 1; i >= 0; i--) {
      auto resourceType = hardware_thread_handle[i].thread_resource_type; // FFT, ZIP, GEMM, etc.
      avail_time = hardware_thread_handle[i].thread_avail_time; // Based on estimated execution times of the tasks in the `todo_queue` of the PE
      task_exec_time = cedr_config.getDashExecTime((*itr)->task_type, resourceType); // Estimated execution time of the task
      auto finishTime = (curr_time >= avail_time) ? curr_time + task_exec_time : avail_time + task_exec_time; // estimated finish time of the task on the PE at i^th index
      auto resourceIsSupported = ((*itr)->supported_resources[(uint8_t) resourceType]); // Check if the current PE support execution of this task
      /* Check if the PE supports the task and if the estimated finish time is earlier than what is found so far */
      if (resourceIsSupported && finishTime < earliest_estimated_availtime) {
        earliest_estimated_availtime = finishTime;
        eft_resource = i;
      }
    }
```

### EFT heuristic - Task-to-PE assignment

Here, we will utilize a built-in function that does final checks before assigning the task to the given PE. Based on this assignment, it also handles the actual queue management and modification of any required field. Details of this function can be found [here](https://github.com/UA-RCL/CEDR/blob/tutorial/src-api/scheduler.cpp#L17-L64).

```c
    // Attempt to assign task on earliest finishing PE
    task_allocated = attemptToAssignTaskToPE(
      cedr_config, // Current configuration of the CEDR
      (*itr), // Task that is being scheduled
      &hardware_thread_handle[eft_resource], // PE that is mapped to the task based on the heuristic
      &resource_mutex[eft_resource], // Mutex protection for the PE's todo queue
      eft_resource // ID of the mapped PE
      );
```

### Final checks

In the last part, we will check whether the task assignment to given PE was successful and move on to the next task in the `ready queue`.

```c
    if (task_allocated) { // If task allocated successfully
      tasks_scheduled++; // Increment the number of scheduled tasks
      itr = ready_queue.erase(itr); // Remove the task from ready_queue
      /* If queueing is disabled, decrement free resource count*/
      if (!cedr_config.getEnableQueueing()) {
        free_resource_count--;
        if (free_resource_count == 0)
          break;
      }
    } else { // If task is not allocated successfully
      itr++; // Go to the next task in ready_queue
    }
  }
  return tasks_scheduled;
```

### Full EFT in C/C++

Now collecting all the steps, we will have the EFT function written in C/C++ that is tailored to CEDR, as shown:

```c
int scheduleEFT(ConfigManager &cedr_config, std::deque<task_nodes *> &ready_queue, worker_thread *hardware_thread_handle, pthread_mutex_t *resource_mutex, uint32_t &free_resource_count) {

  unsigned int tasks_scheduled = 0; // Number of tasks scheduled so far
  int eft_resource = 0; // ID of the PE that will be assigned to the task
  unsigned long long earliest_estimated_availtime = 0; // Estimated finish time initialization
  bool task_allocated; // Task assigned to PE successfully or not

  /* Get current time in nanosecond scale */
  struct timespec curr_timespec {};
  clock_gettime(CLOCK_MONOTONIC_RAW, &curr_timespec);
  long long curr_time = curr_timespec.tv_nsec + curr_timespec.tv_sec * SEC2NANOSEC;

  long long avail_time; // Current available time of the PEs
  long long task_exec_time; // Estimated execution time of the task

  unsigned int total_resources = cedr_config.getTotalResources(); // Total Number of PEs available

  // For loop to iterate over all tasks in Ready queue
  for (auto itr = ready_queue.begin(); itr != ready_queue.end();) {
    earliest_estimated_availtime = ULLONG_MAX;
    // For each task, iterate over all PEs to find the earliest finishing one
    for (int i = total_resources - 1; i >= 0; i--) {
      auto resourceType = hardware_thread_handle[i].thread_resource_type; // FFT, ZIP, GEMM, etc.
      avail_time = hardware_thread_handle[i].thread_avail_time; // Based on estimated execution times of the tasks in the `todo_queue` of the PE
      task_exec_time = cedr_config.getDashExecTime((*itr)->task_type, resourceType); // Estimated execution time of the task
      auto finishTime = (curr_time >= avail_time) ? curr_time + task_exec_time : avail_time + task_exec_time; // estimated finish time of the task on the PE at i^th index
      auto resourceIsSupported = ((*itr)->supported_resources[(uint8_t) resourceType]); // Check if the current PE support execution of this task
      /* Check if the PE supports the task and if the estimated finish time is earlier than what is found so far */
      if (resourceIsSupported && finishTime < earliest_estimated_availtime) {
        earliest_estimated_availtime = finishTime;
        eft_resource = i;
      }
    }

    // Attempt to assign task on earliest finishing PE
    task_allocated = attemptToAssignTaskToPE(
      cedr_config, // Current configuration of the CEDR
      (*itr), // Task that is being scheduled
      &hardware_thread_handle[eft_resource], // PE that is mapped to the task based on the heuristic
      &resource_mutex[eft_resource], // Mutex protection for the PE's todo queue
      eft_resource // ID of the mapped PE
      );

    if (task_allocated) { // If task allocated successfully
      tasks_scheduled++; // Increment the number of scheduled tasks
      itr = ready_queue.erase(itr); // Remove the task from ready_queue
      /* If queueing is disabled, decrement free resource count*/
      if (!cedr_config.getEnableQueueing()) {
        free_resource_count--;
        if (free_resource_count == 0)
          break;
      }
    } else { // If task is not allocated successfully
      itr++; // Go to the next task in ready_queue
    }
  }
  return tasks_scheduled;
}
```

### Adding EFT as a scheduling option

Now, the only thing left is to ensure CEDR can run this function during scheduling events. To do this in the same [scheduler.cpp](https://github.com/UA-RCL/CEDR/tree/tutorial/scr-api/scheduler.cpp) file, we go to the end and update the [performScheduling](https://github.com/UA-RCL/CEDR/blob/tutorial/src-api/scheduler.cpp#L406) function. In the function where `sched_policy` is checked, we add another `else if` segment that checks whether the scheduling policy is `EFT`. If it is, we will call the function we just created.

```c
else if (sched_policy == "EFT") {
    tasks_scheduled += scheduleEFT(cedr_config, ready_queue, hardware_thread_handle, resource_mutex, free_resource_count);
  }
```

After adding EFT as one of the scheduling heuristic options to CEDR, we will need to rebuild CEDR in the `build` directory. First, navigate to [root directory](https://github.com/UA-RCL/CEDR/tree/tutorial/./), then follow the steps below to rebuild CEDR with EFT.

```bash
cd build
make -j
```

### Enabling EFT for CEDR

In the [daemon_config.json](https://github.com/UA-RCL/CEDR/tree/tutorial/daemon_config.json) file, we updated the ["Scheduler"](https://github.com/UA-RCL/CEDR/blob/tutorial/daemon_config.json#L35) field to be "EFT" before running CEDR with the updated daemon config file.

```JSON
    "Scheduler": "EFT",
```

### Running CEDR with EFT Scheduler

Using the same methods as in Section 3.2, we will run CEDR and see the use of the EFT scheduler. After running the following command, we will see that the scheduler to be used is selected as EFT in the displayed logs.

```bash
./cedr -c ./daemon_config.json -l VERBOSE | grep -E "(Scheduler|scheduler)" &
```

```
[...] DEBUG [312918] [ConfigManager::parseConfig@136] Config contains key 'Scheduler', assigning config value to <b>EFT</b>
```

After submitting the application with `sub_dag`, we will see that the newly added EFT scheduler is used during the scheduling event. 

```bash
./sub_dag -a ./radar_correlator_fft-x86.so -n 1 -p 0
```

```
[...] DEBUG [312918] [performScheduling@475] Ready queue non-empty, performing task scheduling using <b>EFT</b> scheduler.
[...] DEBUG [312918] [performScheduling@475] Ready queue non-empty, performing task scheduling using <b>EFT</b> scheduler.
[...] DEBUG [312918] [performScheduling@475] Ready queue non-empty, performing task scheduling using <b>EFT</b> scheduler.
```

Once everything is completed, we will terminate CEDR with `kill_daemon`.

```bash
./kill_daemon
```

## Supplemental Exercise 2: Running Multiple Applications with CEDR on x86
[Return to top](#fpga26-tutorial-step-by-step-flow)

### Compilation of Applications
In this section, we will demonstrate CEDR's ability to manage dynamically arriving applications. Assuming you already have built CEDR following the previous steps, we will directly delve into compiling and running two new applications that are lane detection and pulse doppler.

Firstly, navigate to lane detection folder from the root folder of the repository, compile it for x86 and move shared object and input files to `build` folder for running with CEDR. (If you have already done this for the previous section, you don't have to compile the lane detection once more.)

```bash
cd applications/APIApps/lane_detection/
make fft_nb.so
cp track_nb.so image.png ../../../build
```

Now, let's do the above steps for pulse doppler application and create a output directory in `build` for writing its output. 

```bash
cd ../pulse_doppler/
make nonblocking
cp -r pulse_doppler-nb-x86.so input/ ../../../build
mkdir ../../../build/output
```

### Running the Applications with CEDR

Now that we have all binaries and input files ready, we can proceed with running these applications with CEDR. First, navigate to `build` directory.

```bash
cd ../../../build
```

Then, launch CEDR with your desired configuration and submit both applications with varying number of instances and injection rates. 

```bash
./cedr -c ./daemon_config.json -l NONE &
./sub_dag -a ./track_nb.so,./pulse_doppler-nb-x86.so -n 1,5 -p 0,100
```

Observe the [output image of lane detection](./build/output_fft.png) and the [shift and time delay](./build/output/pulse_doppler_output.txt) calculated by pulse doppler.

## Supplemental Exercise 3: GPU Based SoC Experiment (Nvidia Jetson AGX Xavier)
[Return to top](#fpga26-tutorial-step-by-step-flow)

### Building CEDR
Firstly, we need to connect to the Nvidia Jetson board through ssh connection. 
```bash
ssh <user-name>@<jetson-ip>
``` 

Clone CEDR from GitHub using one of the following methods <b>(we need to add one more line that's checking out to tutorial branch)</b>:
  * Clone with ssh:
```bash
git clone -b tutorial git@github.com:UA-RCL/CEDR.git
```
  * Clone with https:
```bash
git clone -b tutorial https://github.com/UA-RCL/CEDR.git
```

Then, we can build CEDR. Cross compiler is not necessary in this case since we are already logged into the host machine. We enable `GPU` flag for the CMake to be able to make use of the GPU as an accelerator. 
```bash
mkdir build
cd build
cmake -DLIBDASH_MODULES="GPU" ../
make -j -$(nproc)
```

### Compilation

Now, we can compile the lane detection application running the following commands. This creates an executable shared object that we will move to `build` folder along with input image to run the `lane_detection`:
```bash
cd ../applications/APIApps/lane_detection/
make fft_nb.so
cp track_nb.so image.png ../../../build/
```

Also, let's compile the pulse doppler application running the following commands and move shared object and input to 'build' folder:
```bash
cd ../pulse_doppler/
make nonblocking
cp -r pulse_doppler-nb-x86.so input/ ../../../build/
```

### Running the Applications with CEDR

Now, we need to go back to `build` folder and move `daemon_config.json` to it. Also, create a `output` folder for storing `pulse doppler` output:
```bash
cd ../../../build/
cp ../daemon_config.json ./
mkdir output/
```

We should enable `GPU` in `daemon_config.json` so that runtime will use it as a computing resource.

```JSON
"Worker Threads": {
        "cpu": 7,
        "fft": 0,
        "gemm": 0,
        "gpu": 1
    },
...
"Loosen Thread Permissions": true,
```

Execution of CEDR is the same as the x86_64 version. In one terminal launch CEDR:

```bash
./cedr -c ./daemon_config.json -l NONE &
```

In another terminal, we will submit an instance of `lane_detection` and five instances of `pulse doppler` using `sub_dag`:

```bash
./sub_dag -a ./track_nb.so,./pulse_doppler-nb-x86.so -n 1,5 -p 0,100
```

Now kill the CEDR by running `./kill_deamon` on the second terminal and check the resource_name fields for the first 5 FFT tasks:

```bash
head -n 10 ./log_dir/experiment0/timing_trace.log
```

```
app_id: 3, app_name: track_nb, task_id: 0, task_name: DASH_FFT, resource_name: <b>cpu1</b>, ref_start_time: 15215236842193792, ref_stop_time: 15215236873412128, actual_exe_time: 31218336
app_id: 3, app_name: track_nb, task_id: 1, task_name: DASH_FFT, resource_name: <b>cpu2</b>, ref_start_time: 15215236842244288, ref_stop_time: 15215236873341824, actual_exe_time: 31097536
app_id: 3, app_name: track_nb, task_id: 2, task_name: DASH_FFT, resource_name: <b>cpu3</b>, ref_start_time: 15215236842259136, ref_stop_time: 15215236873367616, actual_exe_time: 31108480
app_id: 3, app_name: track_nb, task_id: 3, task_name: DASH_FFT, resource_name: <b>cpu4</b>, ref_start_time: 15215236842278592, ref_stop_time: 15215236873329504, actual_exe_time: 31050912
app_id: 3, app_name: track_nb, task_id: 4, task_name: DASH_FFT, resource_name: <b>cpu5</b>, ref_start_time: 15215236842303616, ref_stop_time: 15215236873309984, actual_exe_time: 31006368
app_id: 3, app_name: track_nb, task_id: 7, task_name: DASH_FFT, resource_name: <b>gpu1</b>, ref_start_time: 15215236842359360, ref_stop_time: 15215236878110208, actual_exe_time: 35750848
app_id: 3, app_name: track_nb, task_id: 5, task_name: DASH_FFT, resource_name: <b>cpu6</b>, ref_start_time: 15215236842560224, ref_stop_time: 15215236873353824, actual_exe_time: 30793600
app_id: 3, app_name: track_nb, task_id: 6, task_name: DASH_FFT, resource_name: <b>cpu7</b>, ref_start_time: 15215236843057888, ref_stop_time: 15215236873386784, actual_exe_time: 30328896
app_id: 3, app_name: track_nb, task_id: 11, task_name: DASH_FFT, resource_name: <b>cpu4</b>, ref_start_time: 15215236873349088, ref_stop_time: 15215236873802944, actual_exe_time: 453856
app_id: 3, app_name: track_nb, task_id: 9, task_name: DASH_FFT, resource_name: <b>cpu2</b>, ref_start_time: 15215236873349440, ref_stop_time: 15215236873780032, actual_exe_time: 430592
```

Lastly, let's compare the outputs with x86 results to validate the correctness.

```bash
xdg-open output_fft.png
cat output/pulse_doppler_output.txt
```


# Contact

For any questions and bug reports, please email [sahilhassan@arizona.edu](mailto:sahilhassan@arizona.edu), [gener@arizona.edu](mailto:gener@arizona.edu), or [suluhan@arizona.edu](mailto:suluhan@arizona.edu).
