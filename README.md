# Experiment with OpenCV Image Classification
## Summary
This experiment, derived from [this](https://docs.opencv.org/4.x/d5/de7/tutorial_dnn_googlenet.html)
OpenCV example, classifies input images using the GoogLeNet DNN.

## Prerequisites
- CMake
- OpenCV
- OpenCL
- (optional, for NVIDIA GPU havers) CUDA

### Installation
#### Arch Linux:
```bash
sudo pacman -S gcc cmake opencv-cuda ocl-icd opencl-headers 
```

For NVIDIA:
```bash
sudo pacman -S opencl-nvidia cuda cudnn
```

For Intel:
```bash
sudo pacman -S onednn
sudo yay -S openvino
```

## Build
```bash
mkdir build; cd build
cmake ..
make
```

## Run
```bash
build/image_classification_example                          \
    --model=models/bvlc_googlenet.caffemodel                \
    --config=models/bvlc_googlenet.prototxt                 \
    --width=224                                             \
    --height=224                                            \
    --classes=classes/classification_classes_ILSVRC2012.txt \
    --input=img/moodeng.jpg                                 \
    --mean="150 117 75"                                     \
    --rgb                                                   \
    --backend=3                                             \
    --target=1
```

A few notes:
- There are a few images under the `img` folder you can experiment with.
- The mean needs to be adjusted for each picture to get best results.
    - this mean value is how much the mean R, G, and B values of the image should be adjusted.
    - this changes how well the neural net is able to detect and classify images.
    - the value of `"104 117 123"` works well for `space_shuttle.jpg`.
    - the value in the above command works well for `moodeng.jpg`.
- Backend and target
    - if you have an NVIDIA GPU, use CUDA for best performance. use `--backend=6 --target=6`.
    - for okay-ish performance on non-NVIDIA, use `--backend=3 --target=1` for the OpenCV backend
      running OpenCL.
    - to use an Intel iGPU, use `--backend=2 --target=1` for the OpenVINO backend running OpenCL.
    - don't use Vulkan. mega slow.
