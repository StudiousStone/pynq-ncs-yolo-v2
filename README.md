# YOLOv2 for PYNQ-Z1 and Intel/Movidius Neural Compute Stick (NCS)

*This project shows how to run tiny yolov2 (20 classes) with PYNQ-Z1 and movidius stick:*
+ A python convertor from yolo to caffe
+ A c/c++ implementation and python wrapper for region layer of yolov2
+ A sample for running yolov2 with movidius stick in images or videos

---

# Updates
+ Refine output bboxes according to letterbox_image in YOLOV2, 01/03/2018, 01/12/2018 (Thanks nathiyaa!)
+ Support multiple sticks, 12/29/2017 (Thanks ichigoi7e!)
+ Process video in the sample, 12/15/2017 (Thanks ichigoi7e!)
+ Fix confident offset issues in nms, 12/12/2017

# How To Use
The following experiments are done on a PYNQ-Z1. You'll also need a Linux PC to compile the graph file with NCSDK.

### Step 1. Install Boost on the PYNQ-Z1
```apt-get install libboost-python-dev```

### Step 2. Clone this repo and compile Python Wrapper
```
git clone https://github.com/fpgadeveloper/pynq-ncs-yolo-v2.git
make
```

### Step 3. Convert Caffe to NCS on development Linux PC
To generate the graph file you will have to install NCSDK on a Linux PC, then clone this repository and run the following command:
```
mvNCCompile ./models/caffemodels/yoloV2Tiny20.prototxt -w ./models/caffemodels/yoloV2Tiny20.caffemodel -s 12
```
There will be a file *graph* generated as converted models for NCS. Just copy this *graph* file to the repo on the PYNQ-Z1.

### Step 4. Run tests
Use the Jupyter notebooks in the notebooks directory of this repo to test YOLOv2 with an image file, a webcam or a HDMI input. You can also run the detection example script by using this command in the terminal:
```	
python3.6 ./detectionExample/Main.py --image ./data/dog.jpg
```
This loads *graph* by default and results will be like this: 
![](/data/yolo_dog.jpg)

# Run Other YoloV2 models
### Convert Yolo to Caffe 
```
Install caffe and config the python environment path.
sh ./models/convertyo.sh
```
Tips:

Please ignore the error message similar as "Region layer is not supported".

The converted caffe models should end with "prototxt" and "caffemodel".

### Update parameters

Please update parameters (biases, object names, etc) in ./src/CRegionLayer.cpp, and parameters (dim, blockwd, targetBlockwd, classe, etc) in ./detectionExample/ObjectWrapper.py.

Please read ./src/CRegionLayer.cpp and ./detectionExample/ObjectWrapper.py for details.

# References
+ [caffe](https://github.com/BVLC/caffe)
+ [yolo](https://github.com/pjreddie/darknet)
+ [caffe-yolo](https://github.com/xingwangsfu/caffe-yolo)
+ [yoloNCS](https://github.com/gudovskiy/yoloNCS)

---

# License
Research Only

# Author
duangenquan@gmail.com
Mods for PYNQ-Z1 and Jupyter notebooks by [Jeff Johnson](http://www.fpgadeveloper.com)
