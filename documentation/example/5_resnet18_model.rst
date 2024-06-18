自定义模型功能-图像分类
==============

代码
-----------
例程::

    from mpython import *
    from camera import *
    import time

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    camera.model_restnet18_init(["label1","label2","label3"],'/root/model/resnet18_1000_awnn.param','/root/model/resnet18_1000_awnn.bin',224,224)
    while True:
        camera.restnet18_model.recognize()
        print(camera.restnet18_model.id)
        time.sleep_ms(10)



mPython图形化
-----------
.. figure:: /_static/image/example/model_detect/2.png
    :align: center
    :width: 1080
