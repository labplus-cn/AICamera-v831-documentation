人脸检测
==============

代码
-----------
例程::

    from mpython import *
    from camera import *
    import time

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    camera.face_detect_init()
    while True:
        camera.face_detect.recognize()
        if camera.face_detect.face_num != None:
            print(str('人脸数量：') + str(camera.face_detect.face_num))
            print(str('置信度：') + str(camera.face_detect.max_score))
        time.sleep_ms(20)



mPython图形化示例
-----------
.. figure:: /_static/image/example/face_detect/face_detect.png
    :align: center
    :width: 1080


方法
-----------


.. _CameraV831:

.. class:: CameraV831(tx=Pin.P16, rx=Pin.P15)
   :synopsis: AI摄像头类

.. method::  CameraV831(tx=Pin.P16, rx=Pin.P15)

``tx`` 
串口发送引脚

``rx``
串口接收引脚

例如::
    
    from mpython import *
    from camera import *
    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)