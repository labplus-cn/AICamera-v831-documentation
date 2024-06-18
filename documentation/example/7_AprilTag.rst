AprilTag识别
==============

代码
-----------
例程::

    from mpython import *
    from camera import *
    import time

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    camera.apriltag_init()
    camera.apriltag.set_tag_families(16)
    while True:
        camera.apriltag.recognize()
        if camera.apriltag.tag_family != None:
            print(camera.apriltag.tag_id)
            print(camera.apriltag.x_tran)
            print(camera.apriltag.x_rol)
            print(camera.apriltag.length)
        time.sleep_ms(20)


mPython图形化
-----------
.. figure:: /_static/image/example/qrcode/AprilTag.png
    :align: center
    :width: 1080

