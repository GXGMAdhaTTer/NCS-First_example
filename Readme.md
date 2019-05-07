# Readme

笔者尝试了live-object-detector案例，但是发现此案例无法成像，于是基于video_object这个案例进行了修改。由于该案例的整体代码过长，笔者将截取关键部分进行说明。以下是修改的过程。

video_object的功能是识别视频中的物体，物体的类型如下。

```python
# labels AKA classes.  The class IDs returned
# are the indices into this list
labels = ('background',
          'aeroplane', 'bicycle', 'bird', 'boat',
          'bottle', 'bus', 'car', 'cat', 'chair',
          'cow', 'diningtable', 'dog', 'horse',
          'motorbike', 'person', 'pottedplant',
          'sheep', 'sofa', 'train', 'tvmonitor')
```

修改的主要思路是将video_object读取视频的过程替换为读取摄像机内容。考虑到这是一个对视频进行逐帧分析的过程，因此笔者开始寻找video_object中处理每一帧的代码片段。

首先，找到了读取视频内容的关键语句。

`cap = cv2.VideoCapture(input_video_file)`

在此处进行替换。

`camera = cv2.VideoCapture(0)`

寻找`cap`行为后，发现了读取`cap`每一帧的函数`read()`。

`ret, display_image = cap.read()`

在此处进行替换。

`ret, display_image = camera.read()`

在进行两步替换，顺便注释掉冗余代码后，video_object顺利改成了live_object。

# 编译环境
python3.5.3
已配置ncsdk和opencv。
自行 git clone https://github.com/movidius/ncsdk.git

#训练模型
采用的是caffe的MobileNet-SSD模型，自行训练参考https://github.com/chuanqi305/MobileNet-SSD
