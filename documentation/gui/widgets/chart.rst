图表
======================================================
概述
~~~~~~~~~~~~~~~
图表是可视化数据点的基本对象。它们支持折线图（将点与线连接和/或在其上绘制点）和柱形图。

图表还支持分隔线，2 y轴，刻度线和刻度线文本。

零件和样式
~~~~~~~~~~~~~~~
图表的主要部分称为 LV_CHART_PART_BG ，它使用所有典型的背景属性。文本样式属性确定轴文本的样式，而线属性确定刻度线的样式。填充值在侧面增加了一些空间，因此使序列区域更小。填充也可用于为轴文本和刻度线留出空间。

该系列的背景称为 LV_CHART_PART_SERIES_BG ，它位于主要背景上。在此部分上绘制了分隔线和系列数据。除典型的背景样式属性外，分割线还使用线型属性。填充值指示此零件与轴文本之间的间隔。

LV_CHART_PART_SERIES 可以引用该系列的样式。对于列类型，使用以下属性：

半径：数据点的半径

padding_inner：相同x坐标的列之间的间隔

如果是线型图，则使用以下属性：

线属性来描述线

点的大小半径

bg_opa：线条下方区域的整体不透明度

bg_main_stop：的％bg_opa在顶部以创建一个alpha褪色（0：在顶部透明，255：bg_opa在顶部）

bg_grad_stop：底部bg_opa的百分比以创建alpha渐变（0：底部透明，255：bg_opa顶部）

bg_drag_dir：应该 LV_GRAD_DIR_VER 允许通过bg_main_stop和bg_grad_stop进行Alpha淡入

LV_CHART_PART_CURSOR 引用游标。可以添加任意数量的光标，并且可以通过与行相关的样式属性来设置其外观。创建游标时设置游标的颜色，并用该值覆盖 line_color 样式。

用法
~~~~~~~~~~~~~~~
数据系列
您可以通过 lv_chart_add_series(chart, color) 向图表添加任意数量的系列。它为包含所选颜色的 lv_chart_u series_t 结构分配数据，如果不使用外部数组，如果分配了外部数组，则与该系列关联的任何内部点都将被释放，而序列指向外部数组。

系列类型
存在以下数据显示类型：

LV_CHART_TYPE_NONE - 不显示任何数据。它可以用来隐藏系列。

LV_CHART_TYPE_LINE - 在两点之间画线。

LV_CHART_TYPE_COLUMN - 绘制列。

可以使用 lv_chart_set_type(chart, LV_CHART_TYPE_...) 指定显示类型。可以对类型进行“或”运算（例如 LV_CHART_TYPE_LINE ）。

修改数据
有几个选项可以设置系列数据：

在数组中手动​​设置值，例如 ser1->points[3] = 7 ，然后使用 lv_chart_refresh(chart) 刷新图表。

使用 lv_chart_set_point_id(chart, ser, value, id) ，其中id是您要更新的点的索引。

使用 lv_chart_set_next(chart, ser, value) 。

使用 lv_chart_init_points(chart, ser, value) 将所有点初始化为给定值。

使用 lv_chart_set_points(chart, ser, value_array) 设置数组中的所有点。

使用 LV_CHART_POINT_DEF 作为值可使库跳过该点，列或线段的绘制。

覆盖系列的默认起点
如果希望绘图从默认点（序列的点[0]）之外的其他点开始，则可以使用 lv_chart_set_x_start_point(chart, ser, id) 函数设置替代索引，其中id是要开始的新索引位置从。

设置外部数据源
可以使用以下函数从外部数据源更新图表系列： lv_chart_set_ext_array(chart, ser, array, point_cnt ) ，其中array是lv_coord_t与point_cnt元素的外部数组。注意：更新外部数据源后，应调用 lv_chart_refresh(chart) 来更新图表。

获取当前图表信息
有四个功能可获取有关图表的信息：

lv_chart_get_type(chart) 返回当前图表类型。

lv_chart_get_point_count(chart) 返回当前图表点数。

lv_chart_get_x_start_point(ser) 返回指定系列的当前绘图索引。

lv_chart_get_point_id(chart, ser, id) 返回指定系列的特定索引处的数据值。

更新模式
lv_chart_set_next 可以以两种方式运行，具体取决于更新模式：

LV_CHART_UPDATE_MODE_SHIFT - 将旧数据向左移动，然后向右添加新数据。

LV_CHART_UPDATE_MODE_CIRCULAR - 循环添加新数据（如ECG图）。

可以使用 lv_chart_set_update_mode(chart, LV_CHART_UPDATE_MODE_...) 更改更新模式。

浮标个数
可以通过 lv_chart_set_point_count(chart, point_num) 修改系列中的点数。默认值为10。注意：当将外部缓冲区分配给序列时，这也会影响处理的点数。

垂直范围
可以使用 lv_chart_set_range(chart, y_min, y_max) 在y方向上指定最小值和最大值。点的值将按比例缩放。默认范围是：0..100。

分割线
水平和垂直分隔线的数量可以通过 lv_chart_set_div_line_count(chart, hdiv_num, vdiv_ 进行修改。默认设置为3条水平分割线和5条垂直分割线。

刻度线和标签
~~~~~~~~~~~~~~~
刻度和标签可以添加到轴上。

lv_chart_set_x_tick_text(chart, list_of_values, num_tick_marks, LV_CHART_AXIS_...) 设置x轴上的刻度和文本。 list_of_values 是一个字符串，带有 '\n' 终止文本（期望最后一个），其中包含用于刻度的文本。 list_of_values 是一个字符串，带有 '\n' 终止文本（期望最后一个），其中包含用于刻度的文本。例如。 const char * list_of_values = "first\nsec\nthird" 。 list_of_values 可以为 NULL 。 如果设置了 list_of_values ，则 num_tick_marks 告诉两个标签之间的刻度数。如果 list_of_values 为 NULL ，则它指定滴答声的总数。

主刻度线绘制在放置文本的位置，次刻度线绘制在其他位置。 ``lv_chart_set_x_tick_length(chart, major_tick_len, minor_tick_len) `` 设置x轴上刻度线的长度。

y轴也存在相同的功能： lv_chart_set_y_tick_text 和 lv_chart_set_y_tick_length 。

光标
~~~~~~~~~~~~~~~
可以使用 lv_chart_cursor_t * c1 = lv_chart_add_cursor(chart, color, dir); 添加光标。 dir LV_CHART_CURSOR_NONE/RIGHT/UP/LEFT/DOWN 的可能值或它们的OR-ed值，用于指示应在哪个方向上绘制光标。

lv_chart_set_cursor_point(chart, cursor, &point) 设置光标的位置。 point 是指向 lv_poin_t 变量的指针。例如。lv_point_t point = {10, 20}; 。该点相对于图表的序列区域。

lv_coord_t p_index = lv_chart_get_nearest_index_from_coord(chart, x) 告诉哪个点索引最接近X坐标（相对于序列区域）。例如，当单击图表时，它可用于将光标捕捉到一个点。

lv_chart_get_x_from_index(chart, series, id) 和 lv_chart_get_y_from_index(chart, series, id) 告诉给定点的X和Y坐标。将光标放置到给定点很有用。

可以使用 lv_chart_get_series_area(chart, &area) 检索当前系列区域，其中 area 是指向 lv_area_t 变量的指针，用于存储结果。该区域具有绝对坐标。

事件
~~~~~~~~~~~~~~~
仅通用事件是按对象类型发送的。

了解有关 事件 的更多信息。

按键
~~~~~~~~~~~~~~~
对象类型不处理任何键。

进一步了解 按键 。

范例
~~~~~~~~~~~~~~~
折线图