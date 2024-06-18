自定义模型功能-目标检测
==============

代码
-----------
例程::

    from mpython import *
    from camera import *
    import time

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    camera.model_yolo_init(["label1","label2","label3"],'/root/model/opt_int8.param','/root/model/opt_int8.bin',224,224,[4.069214876033057, 4.0495867768595035, 4.842875874125874, 4.626966783216783, 4.279592803030304, 4.3652935606060606, 5.198702830188679, 4.841686320754717, 4.55390625, 4.179166666666666])
    while True:
        camera.yolo_model.recognize()
        if camera.yolo_model.id != None:
            if camera.yolo_model.max_score >= 0.5:
                print(camera.yolo_model.id)
                print(camera.yolo_model.max_score)
                print('')
        time.sleep_ms(10)


mPython图形化
-----------
.. figure:: /_static/image/example/model_detect/1.png
    :align: center
    :width: 1080
