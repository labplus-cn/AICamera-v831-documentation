二维码识别
==============

代码
-----------
例程::

    from mpython import *
    from camera import *
    import time

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    camera.mnist_init()
    while True:
        camera.mnist.recognize()
        if camera.mnist.id != None:
            print(camera.mnist.id)
            print(camera.mnist.max_score)
        time.sleep_ms(20)


mPython图形化
-----------
.. figure:: /_static/image/example/mnist/mnist.png
    :align: center
    :width: 1080




