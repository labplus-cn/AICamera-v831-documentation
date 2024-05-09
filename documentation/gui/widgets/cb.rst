复选框
======================================================
概述
~~~~~~~~~~~~~~~
复选框(Checkbox)对象是从 Button 背景构建的，Button 背景还包含Button项目符号和 Label ，以实现经典的复选框。

零件和样式
~~~~~~~~~~~~~~~
该复选框的主要部分称为 LV_CHECKBOX_PART_BG 。它是“项目符号”及其旁边的文本的容器。背景使用所有典型的背景样式属性。

项目符号是真正的 基础对象(lv.obj) ，可以用 LV_CHECKBOX_PART_BULLET 引用。项目符号会自动继承背景状态。因此，背景被按下时，项目符号也会进入按下状态。项目符号还使用所有典型的背景样式属性。

标签没有专用部分。因为文本样式属性始终是继承的，所以可以在背景样式中设置其样式。

用法
~~~~~~~~~~~~~~~
文本
可以通过 lv.Checkbox.set_text("New text") 函数修改文本。它将动态分配文本。

要设置静态文本，请使用 lv.Checkbox.set_static_text(txt) 。这样，将仅存储 txt 指针，并且在存在复选框时不应释放该指针。

选中/取消选中
可以通过 lv.Checkbox.set_checked(true/false) 手动选中/取消选中复选框。设置为 true 将选中该复选框，而设置为 false 将取消选中该复选框。

禁用复选框
要禁用复选框，调用 lv.Checkbox.set_disabled(true) .

获取/设置复选框状态
可以使用 lv.Checkbox.get_state() 函数获取Checkbox的当前状态，该函数返回当前状态。可以使用 lv.Checkbox.set_state(state) 设置复选框的当前状态。
枚举 lv.btn_state_t 定义的可用状态为：

lv.BTN_STATE.RELEASED

lv.BTN_STATE.PRESSED

lv.BTN_STATE.DISABLED

lv.BTN_STATE.CHECKED_RELEASED

lv.BTN_STATE.CHECKED_PRESSED

lv.BTN_STATE.CHECKED_DISABLED

事件
~~~~~~~~~~~~~~~
除了 通用事件 ，复选框还支持以下 特殊事件 ：

lv.EVENT.VALUE_CHANGED - 切换复选框时发送。

请注意，与通用输入设备相关的事件（如LV_EVENT_PRESSED）也以非活动状态发送。需要使用lv.Cb.is_inactive() 检查状态，以忽略非活动复选框中的事件。

了解有关 事件 的更多内容。

按键
~~~~~~~~~~~~~~~
复选框可处理以下按键：

LV_KEY_RIGHT/UP - 如果启用了切换，则进入切换状态

LV_KEY_LEFT/DOWN - 如果启用了切换，则进入非切换状态

请注意，与往常一样，LV_K​​EY_ENTER的状态会转换为LV_EVENT_PRESSED / PRESSING / RELEASED等。

了解有关 按键 的更多内容。

范例
~~~~~~~~~~~~~~~
简单复选框::

    from gui_lib import *
    import time

    scr = lv.scr_act()

    def checkbox1_event_cb(evt):
        pass


    checkbox1 = lv.Checkbox(scr)
    checkbox1.set_event_cb(checkbox1_event_cb)
    checkbox1.set_text("新复选框")
    checkbox1.move_foreground()
    checkbox1.set_checked(True)
    print(checkbox1.is_checked())
    while True:
        time.sleep(1)