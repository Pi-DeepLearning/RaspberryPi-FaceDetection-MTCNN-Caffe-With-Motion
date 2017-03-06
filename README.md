# MTCNN with Motion Detection

The Python version of [MTCNN](https://github.com/kpzhang93/MTCNN_face_detection_alignment) running on Raspberry Pi 3 with Love.  
Also a motion detection trigger will help to improve the quality.

### Requirement
0. Raspbian
1. Caffe && PyCaffe: [https://github.com/BVLC/caffe](https://github.com/BVLC/caffe), [My Blog](http://cdn.tiegushi.com/posts/58bce0ec3456de0027004e17)
2. OpenCV && CV2: [My Blog](http://cdn.tiegushi.com/posts/58bce1999deecf00210048b0)  
  If you have good luck, `apt-get install opencv python-opencv` will have it done.
3. Numpy  
  `apt-get install python-numpy`
4. Jupyter(Optional)  
  `pip install jupyter`  
5. WebCam(D-Link DCS-932L)  
  I have it on hand, so have to write a IPCamera class for it.  
  You can simply use a Camera Model of PI (OV5647), it need Camera White Balance and parameter finetune. (PR Welcome)  

### Tell mtcnn where pycaffe is
Edit mtcnn/_init_paths.py, change **caffe_path** to your own. 

### Run

[Demo.ipynb](Demo.ipynb)
