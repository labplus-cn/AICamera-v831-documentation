下拉列表
======================================================
概述
下拉列表允许用户从列表中选择一个值。

下拉列表默认情况下处于关闭状态，并显示单个值或预定义的文本。激活后（通过单击下拉列表），将创建一个列表，用户可以从中选择一个选项。当用户选择新值时，该列表将被删除。


小部件和样式
~~~~~~~~~~~~~~~
调用下拉列表的主要部分， LV_DROPDOWN_PART_MAIN 它是一个简单的 lv_obj 对象。它使用所有典型的背景属性。按下，聚焦，编辑等阶梯也照常应用。

单击主对象时创建的列表是Page。它的背景部分可以被引用， LV_DROPDOWN_PART_LIST 并为矩形本身使用所有典型的背景属性，并为选项使用文本属性。要调整选项之间的间距，请使用text_line_space样式属性。填充值可用于在边缘上留出一些空间。

页面的可滚动部分被隐藏，其样式始终为空（透明，无填充）。

滚动条可以被引用 LV_DROPDOWN_PART_SCRLBAR 并使用所有典型的背景属性。

可以 LV_DROPDOWN_PART_SELECTED 使用所有典型的背景属性引用并使用所选的选项。它将以其默认状态在所选选项上绘制一个矩形，并在按下状态下在被按下的选项上绘制一个矩形。

用法
~~~~~~~~~~~~~~~
设定选项
选项作为带有 lv_dropdown_set_options(dropdown, options) 的字符串传递到下拉列表。选项应用 \n 分隔。例如： "First\nSecond\nThird" 。该字符串将保存在下拉列表中，因此也可以保存在本地变量中。

lv_dropdown_add_option(dropdown, "New option", pos) 函数向 pos 索引插入一个新选项。

为了节省内存，还可以使用 lv_dropdown_set_static_options(dropdown, options) 从静态（常量）字符串设置选项。在这种情况下，当存在下拉列表且不能使用 lv_dropdown_add_option 时，options字符串应处于活动状态

可以使用 lv_dropdown_set_selected(dropdown, id) 手动选择一个选项，其中id是选项的索引。

获取选择的选项
使用获取当前选择的选项 lv_dropdown_get_selected(dropdown) 。它将返回所选选项的索引。 lv_dropdown_get_selected_str(dropdown, buf, buf_size) 将所选选项的名称复制到 buf 。

方向
~~~~~~~~~~~~~~~
该列表可以在任何一侧创建。默认值 LV_DROPDOWN_DOWN 可以通过功能进行修改。 lv_dropdown_set_dir(dropdown, LV_DROPDOWN_DIR_LEFT/RIGHT/UP/DOWN)

如果列表垂直于屏幕之外，它将与边缘对齐。

符号
~~~~~~~~~~~~~~~
可以使用 lv_dropdown_set_symbol(dropdown, LV_SYMBOL_...) 将符号（通常是箭头）添加到下拉列表中

如果下拉列表的方向为 LV_DROPDOWN_DIR_LEFT ，则该符号将显示在左侧，否则显示在右侧。

最大高度
可以通过 lv_dropdown_set_max_height(dropdown, height) 设置下拉列表的最大高度。默认情况下，它设置为3/4垂直分辨率。

显示所选
主要部分可以显示所选选项或静态文本。可以使用 lv_dropdown_set_show_selected(sropdown, true/false) 进行控制。

可以使用 lv_dropdown_set_text(dropdown, "Text") 设置静态文本。仅保存文本指针。

如果也不想突出显示所选选项，则可以将自定义透明样式用于 LV_DROPDOWN_PART_SELECTED 。

动画时间
下拉列表的打开/关闭动画时间由 lv_dropdown_set_anim_time(ddlist, anim_time) 调整。动画时间为零表示没有动画。

手动打开/关闭
要手动打开或关闭下拉列表，可以使用 lv_dropdown_open/close(dropdown, LV_ANIM_ON/OFF) 功能。

事件
~~~~~~~~~~~~~~~
除了 通用事件 外，下拉列表还发送以下 特殊事件 ：

LV_EVENT_VALUE_CHANGED - 选择新选项时发送。

了解有关 事件 的更多信息。

按键
~~~~~~~~~~~~~~~
以下按键由按钮处理：

LV_KEY_RIGHT/DOWN - 选择下一个选项。

LV_KEY_LEFT/UP - 选择上一个选项。

LY_KEY_ENTER - 应用选定的选项（发送LV_EVENT_VALUE_CHANGED事件并关闭下拉列表）。

进一步了解 按键 。

范例
~~~~~~~~~~~~~~~
简单的下拉列表::

    from gui_lib import *
    import time

    scr = lv.scr_act()

    def dropdown1_event_cb(evt):
        pass


    dropdown1 = lv.Dropdown(scr)
    dropdown1.set_event_cb(dropdown1_event_cb)
    dropdown1.set_options("选项1\n选项2\n选项3")
    dropdown1.add_option("新选项", -1)
    dropdown1.set_selected(0)
    while True:
        time.sleep(1)
