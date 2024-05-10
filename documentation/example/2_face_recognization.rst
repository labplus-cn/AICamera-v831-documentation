人脸识别
==============

代码
-----------
例程::

    from mpython import *
    from camera import *
    import time

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    camera.face_recognize_init(2, 80)
    camera.fcr.add_face()
    while True:
        camera.fcr.recognize()
        if camera.fcr.id != None:
            print(camera.fcr.id)
            print(camera.fcr.max_score)
        time.sleep_ms(20)




mPython图形化
-----------
.. figure:: /_static/image/example/face_recognization/face_recognization.png
    :align: center
    :width: 1080