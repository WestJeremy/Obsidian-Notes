Compute Unified Device Architecture

**Parallelism**
Allows GPUs to run parallel processing
CPUs run serial processing
CUDA cores = Number of executable threads
Jetson has 2048 CUDA Cores

**Executing instructions**
Each CUDA core runs a thread
A kernel (function that runs on GPU) splits into thousands of threads


**Floating point ops**
optimized for floating point 
Graphics, deep learning need floating point

**Architecture**
CUDA cores grouped into Streaming Multiprocessors (SM) withing the GPU
Each SM manage their CUDA cores that share memory and control logic

**How CUDA works:**
1. Written code runs on a GPU using CUDA.
2. Kernels executed in parallel by multiple CUDA cores.

CUDA Exceutable code is written in CUDA C using "global" and "device" tags for CUDA and "host " for CPU

CUDA is also available for python using CUDA Python
https://developer.nvidia.com/cuda-python









