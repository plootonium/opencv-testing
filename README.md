# Experiment with OpenCV Image Classification
## Summary
This experiment, derived from [this](https://github.com/Geekgineer/YOLOs-CPP/blob/main/src/camera_inference.cpp)
OpenCV example, classifies objects in a real-time video stream.

## Prerequisites
- CMake
- OpenCV
- OpenCL
- ONNX Runtime
- (optional, for NVIDIA GPU havers) CUDA

### Installation
#### Arch Linux:
```bash
sudo pacman -S gcc cmake opencv-cuda ocl-icd opencl-headers onnxruntime-opt
```

TODO: will the above "just work" on an Intel CPU?

For NVIDIA:
```bash
sudo pacman -S opencl-nvidia cuda cudnn
```

## Build
```bash
mkdir build; cd build
cmake ..
make
```

## Run
```bash
build/image_classification_example
```

This will launch a GUI window that shows the video camera output overlayed with bounding boxes around classfied objects, with a small class name and percent confidence.
