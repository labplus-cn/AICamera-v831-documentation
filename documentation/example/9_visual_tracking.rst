图像巡线
==============


图像巡线
-----------
例程::

    from mpython import *
    from camera import *
    import time

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    camera.find_line_init()
    while True:
        camera.find_line.recognize()
        if camera.find_line.line_data["rect"] != None:
            print(camera.find_line.line_data["pixels"])
            print(camera.find_line.rotation_angle)
        time.sleep_ms(20)



mPython图形化
-----------
.. figure:: /_static/image/example/visual_tracking/visual_tracking.png
    :align: center
    :width: 1080

