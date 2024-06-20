二维码识别
==============

代码
-----------
例程::

    from mpython import *
    from camera import *
    import time

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    camera.qrcode_init()
    camera.qrcode.add_qrcode(1)
    while True:
        camera.qrcode.recognize()
        if camera.qrcode.id != None:
            print(camera.qrcode.id)
            print(camera.qrcode.info)
        time.sleep_ms(20)



mPython图形化示例
-----------
.. figure:: /_static/image/example/qrcode/qrcode.png
    :align: center
    :width: 1080




