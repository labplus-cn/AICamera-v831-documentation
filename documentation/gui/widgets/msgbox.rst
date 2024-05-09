消息框(lv_msgbox)
======================================================

概述
~~~~~~~~~~~~~~~
消息框充当弹出窗口。它们由背景容器，标签和按钮的 按钮矩阵(lv_imgbtn) 构建而成。

文本将自动分成多行（具有 LV_LABEL_LONG_MODE_BREAK ），高度将自动设置为包含文本和按钮（ LV_FIT_TIGHT 垂直放置）


零件和样式
~~~~~~~~~~~~~~~
消息框的主要部分称为 LV_MSGBOX_PART_MAIN ，它使用所有典型的背景样式属性。使用填充会增加侧面的空间。pad_inner将在文本和按钮之间添加空格。标签样式属性会影响文本样式。

按钮部分与 按钮矩阵(lv_imgbtn) 的情况相同：

LV_MSGBOX_PART_BTN_BG 按钮的背景

LV_MSGBOX_PART_BTN 按钮

用法
~~~~~~~~~~~~~~~
设置文本
要设置文本，请使用 lv_msgbox_set_text(msgbox, "My text") 函数。不仅将保存文本指针，而且文本也可以位于局部变量中。

添加按钮
要添加按钮，请使用 lv_msgbox_add_btns(msgbox, btn_str) 函数。需要指定按钮的文本，例如 const char * btn_str[] = {"Apply", "Close", ""} 。有关更多信息，请访问Button矩阵文档。

仅当首次调用 lv_msgbox_add_btns() 时，才会创建 按钮矩阵(lv_imgbtn)。

自动关闭
使用 lv_msgbox_start_auto_close(mbox, delay) 可以在动画 延迟(delay) 了几毫秒后自动关闭消息框。 lv_mbox_stop_auto_close(mbox) 函数停止启动的自动关闭。

关闭动画的持续时间可以通过 lv_mbox_set_anim_time(mbox, anim_time) 设置。

事件
~~~~~~~~~~~~~~~
除了 通用事件 ，复选框还支持以下 特殊事件 ：

LV_EVENT_VALUE_CHANGED 单击按钮时发送。事件数据设置为单击按钮的ID。

消息框具有一个默认的事件回调，当单击按钮时，该事件回调将自行关闭。

了解有关 事件 的更多内容。

按键处理
~~~~~~~~~~~~~~~
消息框可处理以下按键：

LV_KEY_RIGHT/DOWN 选择下一个按钮

LV_KEY_LEFT/TOP 选择上一个按钮

LV_KEY_ENTER 单击选定的按钮

了解有关 按键 的更多内容。

范例
~~~~~~~~~~~~~~~
简单消息框::

