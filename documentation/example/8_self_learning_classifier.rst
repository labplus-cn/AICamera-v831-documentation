自学习分类
==============

训练保存模型
-----------
例程::

    from mpython import *
    from camera import *
    import time

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    ID = ['class1', 'class2', 'class3']
    camera.self_learning_classifier_init(3, 15)
    camera.slc.add_class_img()
    camera.slc.add_sample_img()
    camera.slc.train()
    camera.slc.save_classifier('/root/self_learning_classifier/classes.bin')
    while True:
        camera.slc.predict()
        index = camera.slc.id
        score = camera.slc.max_score
        if index != None and score != None:
            print(ID[index])
        time.sleep_ms(20)



mPython图形化示例
-----------
.. figure:: /_static/image/example/self_learning_classifier/1.png
    :align: center
    :width: 1080




加载使用模型
-----------
例程::

    from mpython import *
    from camera import *
    import time

    index = None
    score = None

    camera = CameraV831(tx=Pin.P16, rx=Pin.P15)
    ID = ['class1', 'class2']
    camera.self_learning_classifier_init(3, 15)
    camera.slc.load_classifier('/root/self_learning_classifier/classes.bin')
    while True:
        camera.slc.predict()
        index = camera.slc.id
        score = camera.slc.max_score
        if index != None:
            print(ID[index])



mPython图形化
-----------
.. figure:: /_static/image/example/self_learning_classifier/2.png
    :align: center
    :width: 1080

