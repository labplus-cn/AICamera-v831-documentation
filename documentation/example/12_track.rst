寻找色块
===================

例程::

    from mpython import *
    from camera import *
    import time

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    camera.track_init()
    camera.track_set_up([[0, 80, 15, 127, 15, 127], [0, 80, -70, -10, 0, 30]],100)
    while True:
        camera.track.recognize()
        if camera.track.x != None:
            print(camera.track.x)
            print(camera.track.cx)
            print(camera.track.pixels)
        print('===')
        time.sleep_ms(20)




mPython图形化示例
----------------
.. figure:: /_static/image/example/track/track_color.png
    :align: center
    :width: 1080