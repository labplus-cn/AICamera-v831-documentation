滑杆(lv_slider)
======================================================
概述
~~~~~~~~~~~~~~~
滑杆对象看起来像是带有旋钮的 进度条(lv_bar) 。可以拖动该旋钮以设置一个值。滑块也可以是垂直或水平的。


零件和样式
~~~~~~~~~~~~~~~
滑块的主要部分称为 LV_SLIDER_PART_BG ，它使用典型的背景样式属性。

LV_SLIDER_PART_INDIC 是一个虚拟部件，它也使用所有典型的背景属性。默认情况下，指标的最大大小与背景的大小相同，但在 LV_SLIDER_PART_BG 中设置正填充值将使指标变小。 （负值会使它变大） 如果在指示器上使用了值样式属性，则将根据指示器的当前大小来计算对齐方式。例如，中心对齐值始终显示在指示器的中间，无论其当前大小如何。

LV_SLIDER_PART_KNOB 是一个虚拟部件，使用所有典型的背景属性来描述旋钮。与指示器类似，值文本也与旋钮的当前位置和大小对齐。默认情况下，旋钮是正方形（具有半径），其边长等于滑块的较小边。 可以使用填充值使旋钮变大。填充值也可以是不对称的。

用法
~~~~~~~~~~~~~~~
值和范围
--------------
要设置初始值，请使用 lv_slider_set_value(slider, new_value, LV_ANIM_ON/OFF) 。 lv_slider_set_anim_time(slider, anim_time) 设置动画时间（以毫秒为单位）。

要指定范围（最小，最大值），可以使用 lv_slider_set_range(slider, min , max) 。

对称范围
--------------
除普通类型外，滑块还可以配置为两种其他类型：

LV_SLIDER_TYPE_NORMAL 普通型

LV_SLIDER_TYPE_SYMMETRICAL 将指标对称地绘制为零（从零开始，从左到右）

LV_SLIDER_TYPE_RANGE 允许为左（起始）值使用附加旋钮。 （可与 lv_slider_set/get_left_value() 一起使用）

可以使用 lv_slider_set_type(slider, LV_SLIDER_TYPE_...) 更改类型

仅旋钮模式
--------------
通常，可以通过拖动旋钮或单击滑块来调整滑块。在后一种情况下，旋钮移动到所单击的点，并且滑块值相应地变化。在某些情况下，希望将滑块设置为仅在拖动旋钮时做出反应。

通过调用 lv_obj_set_adv_hittest(slider, true); 启用此功能。

事件
~~~~~~~~~~~~~~~
除了 通用事件 ，滑杆还支持以下 特殊事件 ：

LV_EVENT_VALUE_CHANGED 在使用键拖动或更改滑块时发送。拖动滑块时（仅当释放时）连续发送事件。使用lv_slider_is_dragged确定滑块是被拖动还是刚刚释放。

了解有关 事件 的更多内容。

按键处理
~~~~~~~~~~~~~~~
滑杆可处理以下按键：

LV_KEY_UP, LV_KEY_RIGHT 将滑块的值增加1

LV_KEY_DOWN, LV_KEY_LEFT 将滑块的值减1

了解有关 按键 的更多内容。

范例
~~~~~~~~~~~~~~~
自定义样式的滑块::

    from gui_lib import *
    import time

    scr = lv.scr_act()

    def slider1_event_cb(evt):
        pass


    slider1 = lv.Slider(scr)
    slider1.set_event_cb(slider1_event_cb)
    slider1.set_type(lv.SLIDER_TYPE.NORMAL)
    slider1.set_range(0, 100)
    slider1.set_left_value(0, lv.ANIM.ON)
    slider1.set_value(0, lv.ANIM.ON)
    slider1.set_value(50, lv.ANIM.ON)
    time.sleep(2)
    slider1.set_left_value(50, lv.ANIM.ON)
    while True:
        time.sleep(1)

