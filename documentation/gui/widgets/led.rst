LED
======================================================
LED是矩形（或圆形）对象。它的亮度可以调节。亮度降低时，LED的颜色会变暗。


零件和样式
~~~~~~~~~~~~~~~
LED只有一个主要部分，称为 LV_LED_PART_MAIN ，它使用所有典型的背景样式属性。

用法
~~~~~~~~~~~~~~~
亮度
可以使用 lv.Led.set_bright(bright) 设置它们的亮度。亮度应介于0（最暗）和255（最亮）之间。

切换
~~~~~~~~~~~~~~~
使用 lv.Led.on() 和 lv.Led.off() 将亮度设置为预定义的ON或OFF值。 lv.Led.toggle() 在ON和OFF状态之间切换。

事件
~~~~~~~~~~~~~~~
仅支持 通用事件

了解有关 事件 的更多内容。

按键处理
~~~~~~~~~~~~~~~
对象类型不处理任何键。

了解有关 按键 的更多内容。

范例
~~~~~~~~~~~~~~~
LED灯闪烁::

    from gui_lib import *
    import time

    scr = lv.scr_act()

    led1 = lv.Led(scr)
    led1.set_pos(100, 100)
    led1.set_bright(0)
    led1.on()
    while True:
        time.sleep(1)
        led1.toggle()