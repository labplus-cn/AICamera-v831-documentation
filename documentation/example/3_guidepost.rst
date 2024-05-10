路标识别
==============


代码
-----------
例程::

    from mpython import *
    from camera import *
    import time

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    camera.guidepost_init()
    while True:
        camera.guidepost.recognize()
        if camera.guidepost.id != None and camera.guidepost.max_score >= 0.5:
            print(camera.guidepost.id)
            print(camera.guidepost.max_score)
        time.sleep_ms(20)




mPython图形化
-----------
.. figure:: /_static/image/example/guidepost/guidepost.png
    :align: center
    :width: 1080