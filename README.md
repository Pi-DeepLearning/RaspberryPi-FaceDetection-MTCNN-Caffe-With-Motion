# MTCNN with Motion Detection On Raspberry Pi 3

The Python version of [MTCNN](https://github.com/kpzhang93/MTCNN_face_detection_alignment) running on Raspberry Pi 3 with Love.  
Also a motion detection trigger will help to improve the quality.

### Requirement
Installation of dependencies:
```shell
  sudo apt-get update && sudo apt-get upgrade
  sudo apt-get install -y gfortran cython
  sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler git
  sudo apt-get install --no-install-recommends libboost-all-dev
  sudo apt-get install -y python-dev libgflags-dev libgoogle-glog-dev liblmdb-dev libatlas-base-dev python-skimage
  sudo pip install pyzmq jsonschema pillow numpy scipy ipython jupyter pyyaml
```  
0. Raspbian
1. Caffe && PyCaffe: [https://github.com/BVLC/caffe](https://github.com/BVLC/caffe), [My Blog](http://cdn.tiegushi.com/posts/58bce0ec3456de0027004e17)

Install caffe:
```shell
  git clone https://github.com/BVLC/caffe
  cd caffe
  cp Makefile.config.example Makefile.config
  sudo nano Makefile.config
```
  Modify next lines, instead of these
```shell  
  #CPU_ONLY := 1
  /usr/lib/python2.7/dist-packages/numpy/core/include
  INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include
  LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib
```  
  with:
```shell  
  CPU_ONLY := 1
  /usr/local/lib/python2.7/dist-packages/numpy/core/include
  INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/
  LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/arm-linux-gnueabihf/hdf5/serial/
```

```shell
  make all
  make test
  make runtest
  make pycaffe
  
  ./scripts/download_model_binary.py models/bvlc_googlenet
  sudo nano ~/.bashrc
  export PYTHONPATH=/home/pi/deepdream/caffe/python:$PYTHONPATH // Add at the end of file
```
Protobuf installation:
```shell
  cd ~/caffe
  cd python
  python setup.py build
  python setup.py google_test
  sudo python setup.py install
```
2. OpenCV && CV2: [My Blog](http://cdn.tiegushi.com/posts/58bce1999deecf00210048b0)  
  If you have good luck, `sudo apt-get install opencv python-opencv` will have it done.
  or search installation guide from google.
 
4. WebCam(D-Link DCS-932L)  
  I have it on hand, so have to write a IPCamera class for it.  
  You can simply use a Camera Model of PI (OV5647), it need Camera White Balance and parameter finetune. (PR Welcome) 
  
  if you use PiNor Cam module or other nonUSB cam, you may need do following changes:
  ```shell
    sudo modprobe bcm2835-v4l2
  ```  
    code:
      ret, frame = ipCam.read()
      _, cnts, _ = cv2.findContours(thresh.copy(), cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_SIMPLE)
    
  
### Tell mtcnn where pycaffe is
Edit mtcnn/_init_paths.py, change **caffe_path** to your own. 

### Run

[Demo.ipynb](Demo.ipynb)

