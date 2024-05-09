开关(lv_switch)
======================================================
概述
~~~~~~~~~~~~~~~
开关可用于打开/关闭某物。它看起来像一个小滑块。


零件和样式
~~~~~~~~~~~~~~~
开关使用以下部分

LV_SWITCH_PART_BG : 主要部分

LV_SWITCH_PART_INDIC : 指标（虚拟部分）

LV_SWITCH_PART_KNOB : 旋钮（虚拟部分）

零件和样式与 滑杆(lv_slider) 情况相同。

用法
~~~~~~~~~~~~~~~
变更状态
-------------
可以通过单击或通过下面的函数更改开关的状态：

lv_switch_on(switch, LV_ANIM_ON/OFF) 开

lv_switch_off(switch, LV_ANIM_ON/OFF) 关

lv_switch_toggle(switch, LV_ANOM_ON/OFF) 切换开关的位置

动画时间
-------------
切换开关状态时的动画时间可以使用 lv_switch_set_anim_time(switch, anim_time) 进行调整。

事件
~~~~~~~~~~~~~~~
除了 通用事件 ，开关还支持以下 特殊事件 ：

LV_EVENT_VALUE_CHANGED 在开关更改状态时发送。

了解有关 事件 的更多内容。

按键处理
~~~~~~~~~~~~~~~
开关可处理以下按键：

LV_KEY_UP, LV_KEY_RIGHT 打开滑块

LV_KEY_DOWN, LV_KEY_LEFT 关闭滑块

了解有关 按键 的更多内容。

范例
~~~~~~~~~~~~~~~
简单开关::

    from gui_lib import *
    import time

    scr = lv.scr_act()

    def switch1_event_cb(evt):
        pass

    switch1 = lv.Switch(scr)
    switch1.set_event_cb(switch1_event_cb)
    switch1.off(lv.ANIM.ON)
    while True:
        time.sleep(1)