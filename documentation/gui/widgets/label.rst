标签
======================================================
概述
~~~~~~~~~~~~~~~
标签是用于显示文本的基本对象类型。

零件和样式
~~~~~~~~~~~~~~~
标签只有一个主要部分，称为 LV_LABEL_PART_MAIN 。它使用所有典型的背景属性和文本属性。填充值可用于使文本的区域在相关方向上变小。

用法
~~~~~~~~~~~~~~~
设定文字
可以在运行时使用 lv_label_set_text(label, "New text") 在标签上设置文本。它将动态分配一个缓冲区，并将提供的字符串复制到该缓冲区中。因此，在该函数返回后，无需将传递给 lv_label_set_text 的文本保留在范围内。

使用 lv_label_set_text_fmt(label, "Value: %d", 15) ，可以使用printf格式设置文本。

标签能够显示来自0终止的静态字符缓冲区的文本。为此，请使用 lv_label_set_static_text(label, "Text") 。在这种情况下，文本不会存储在动态内存中，而是直接使用给定的缓冲区。这意味着数组不能是在函数退出时超出范围的局部变量。 常数字符串可以安全地与 lv_label_set_static_text 一起使用（除非与 LV_LABEL_LONG_DOT 一起使用，因为它可以就地修改缓冲区），因为它们存储在ROM存储器中，该存储器始终可以访问。

也可以使用原始数组作为标签文本。数组不必以 \0 终止。在这种情况下，文本将与 lv_label_set_text 一样保存到动态存储器中。要设置原始字符数组，请使用 lv_label_set_array_text(label, char_array, size) 函数。

越线
------------------
换行符由标签对象自动处理。可以使用 \n 换行。例如： "line1\nline2\n\nline4"

长模式
------------------
默认情况下，标签对象的宽度会自动扩展为文本大小。否则，可以根据几种长模式策略来操纵文本：

LV_LABEL_LONG_EXPAND - 将对象大小扩展为文本大小（默认）

LV_LABEL_LONG_BREAK - 保持对象宽度，断开（换行）过长的线条并扩大对象高度

LV_LABEL_LONG_DOT - 保持对象大小，打断文本并在最后一行写点（使用 lv_label_set_static_text 时不支持）

LV_LABEL_LONG_SROLL - 保持大小并来回滚动标签

LV_LABEL_LONG_SROLL_CIRC - 保持大小并循环滚动标签

LV_LABEL_LONG_CROP - 保持大小并裁剪文本

可以使用 lv_label_set_long_mode(label, LV_LABEL_LONG_...) 指定长模式

重要的是要注意，当创建标签并设置其文本时，标签的大小已扩展为文本大小。除了默认的 LV_LABEL_LONG_EXPAND ，长模式 lv_obj_set_width/height/size() 无效。

因此，需要更改长模式，首先设置新的长模式，然后使用 lv_obj_set_width/height/size() 设置大小。

另一个重要的注意事项是 LV_LABEL_LONG_DOT 在原地操纵文本缓冲区，以便添加/删除点。当使用 lv_label_set_text 或`` lv_label_set_array_text`` 时，将分配一个单独的缓冲区，并且该实现细节不会被注意。 lv_label_set_static_text 并非如此！如果打算使用 LV_LABEL_LONG_DOT ，则传递给 lv_label_set_static_text 的缓冲区必须可写。

文字对齐
----------------
文本的行可以使用 lv_label_set_align(label, LV_LABEL_ALIGN_LEFT/RIGHT/CENTER) 左右对齐。请注意，它将仅对齐线，而不对齐标签对象本身。

标签本身不支持垂直对齐；应该将标签放在更大的容器中，然后将整个标签对象对齐。

文字重新着色
----------------
在文本中，可以使用命令来重新着色部分文本。例如： "Write a #ff0000 red# word" 。可以通过 lv_label_set_recolor() 函数分别为每个标签启用此功能。

请注意，重新着色只能在一行中进行。因此， \n 不应在重新着色的文本中使用，或者用 LV_LABEL_LONG_BREAK 换行，否则，新行中的文本将不会重新着色。

很长的文字
----------------
Lvgl通过保存一些额外的数据（~12个字节）来加快绘图速度，可以有效地处理很长的字符（> 40k 个字符）。要启用此功能，请在lv_conf.h中设置 LV_LABEL_LONG_TXT_HINT   1

符号
------------------
标签可以在字母旁边显示符号（或单独显示）。阅读 字体(font) 部分以了解有关符号的更多信息。

事件
~~~~~~~~~~~~~~~
仅 通用事件 是按对象类型发送的。

了解有关 事件 的更多内容。

按键
~~~~~~~~~~~~~~~
对象类型不处理任何键。

了解有关 按键 的更多内容。

范例
~~~~~~~~~~~~~~~
文本显示::

    from gui_lib import *
    import time

    scr = lv.scr_act()

    label1 = lv.Label(scr)
    label1.set_recolor(True)
    label1.set_text("你好世界")
    label1.set_long_mode(lv.LABEL_LONG.EXPAND)
    while True:
        time.sleep(1)
