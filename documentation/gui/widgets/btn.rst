按钮
======================================================
概述
~~~~~~~~~~~~~~~
按钮是简单的矩形对象。它们源自容器，因此也可以提供布局和配合。此外，可以启用它以在单击时自动进入检查状态。


零件和样式
~~~~~~~~~~~~~~~
这些按钮仅具有一种主要样式，称为 lv.Btn.PART_MAIN ，并且可以使用以下组中的所有属性：

背景(background)

边界(border)

边框(outline)

阴影(shadow)

数值(value)

模式(pattern)

过渡(transitions)

启用布局或适合时，它还将使用padding属性。

用法
~~~~~~~~~~~~~~~
为了简化按钮的使用，可以使用 lv.Btn.get_state() 来获取按钮的状态。它返回以下值之一：

lv.BTN_STATE.RELEASED 松开

lv.BTN_STATE.PRESSED 被点击

lv.BTN_STATE.CHECKED_RELEASED 点击后松开

lv.BTN_STATE.CHECKED_PRESSED 重复点击

lv.BTN_STATE.DISABLED 禁用

lv.BTN_STATE.CHECKED_DISABLED

使用 lv.Btn.set_state(lv.BTN_STATE. ...) 可以手动更改按钮状态。

.. 如果需要状态的更精确描述（例如，重点突出），则可以使用常规 lv.obj_get_state(btn) 。

可检查
~~~~~~~~~~~~~~~
可以使用 lv.Btn.set_checkable(btn, true) 将按钮配置为切换按钮。在这种情况下，单击时，按钮将自动进入 lv.STATE_CHECKED 状态，或再次单击时返回到lv.STATE_CHECKED状态。

布局和适配
~~~~~~~~~~~~~~~
与容器类似，按钮也具有布局和适合属性。

lv.Btn.set_layout(lv.LAYOUT. ...) 设置布局。默认值为 lv.LAYOUT_CENTER 。因此，如果添加标签，则标签将自动与中间对齐，并且无法通过 lv.Obj.set_pos() 移动。您可以使用 lv.Btn.set_layout(lv.LAYOUT.OFF) 禁用布局。

lv.Btn.set_fit/fit2/fit4(lv.FIT.MAX/NONE/PARENT/TIGHT) 允许根据子代，父代和适合类型自动设置按钮的宽度和/或高度。

事件
~~~~~~~~~~~~~~~
除了 通用事件 外，按钮还发送以下特殊事件：

lv.EVENT_VALUE_CHANGED-切换按钮时发送。

了解有关 事件 的更多信息。

按键
~~~~~~~~~~~~~~~
以下按键由按钮处理：

lv.KEY_RIGHT/UP-如果启用了切换，则进入切换状态。

lv.KEY_LEFT/DOWN-如果启用了切换，则进入非切换状态。

请注意， lv.K​​EY_ENTER 的状态已转换为 lv.EVENT_PRESSED/PRESSING/RELEASED 等。

进一步了解 按键 。

范例
~~~~~~~~~~~~~~~
简单的按钮::

    from gui_lib import *
    import time

    scr = lv.scr_act()

    def btn1_event_cb(evt):
        if evt == lv.EVENT.CLICKED:
            try: threading.Thread(target=btn1_clicked, args=(), daemon=True).start()
            except: pass
        elif evt == lv.EVENT.PRESSED:
            try: threading.Thread(target=btn1_pressed, args=(), daemon=True).start()
            except: pass
        elif evt == lv.EVENT.PRESSING:
            try: threading.Thread(target=btn1_pressing, args=(), daemon=True).start()
            except: pass
        elif evt == lv.EVENT.LONG_PRESSED:
            try: threading.Thread(target=btn1_long_pressed, args=(), daemon=True).start()
            except: pass
        elif evt == lv.EVENT.RELEASED:
            try: threading.Thread(target=btn1_released, args=(), daemon=True).start()
            except: pass
        elif evt == lv.EVENT.VALUE_CHANGED:
            try: threading.Thread(target=btn1_value_changed, args=(), daemon=True).start()
            except: pass

    def btn1_pressed():
        print("Hello, world")


    btn1 = lv.Btn(scr)
    btn1.set_event_cb(btn1_event_cb)
    btn1.set_fit()
    btn1_label = lv.Label(btn1)
    btn1_label.set_text("按钮")
    btn1.set_pos(60, 50)
    while True:
        time.sleep(1)
