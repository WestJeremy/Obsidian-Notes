TensorRT is a deep learning inference library for use on NVIDIA GPUs.
Best for high speed low latency applications.

**Model Optimization**
	preforms transformations
		layer fusion
			fuse NN layers reducing model size
		precision calibration
		kernel auto-tuning
		dynamic tensor memory management
			handles memory as needed during inference, maximizing GPU memory

**Mixed Precision Inference**
	Combine Floating point (FP) 32 and 16
		less memory minimal loss in accuracy

**Support for Popular Frameworks**
	import models from Tensorflow, pytorch, ect then optimize for NVIDIA
	
**Scalability**
	Deploy small (jetson) to large (data center)


**Example Workflow**
1. Train model on python
2. Export to TensorRT accepted format
3. import model into TensorRT and apply optimizations
	1. TensorRT python api 
4. Deploy and run on NVIDIA GPU
5. Debug system with [[Nsight Systems]]. use [[TegraStats]] command to monitor resources such as CPU/GPU utility, memory, and power consumption in real time.
