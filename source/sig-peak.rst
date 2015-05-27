sigPeak
=======

描述
    峰/底信号函数。该函数检验看mktdata或指标列观测值在任一方向上是否低于（高于）创建一个局部顶峰（谷底）。

用法
::

    sigPeak(label, data, column, direction = c("peak", "bottom"))

参数
    :label: 应用到输出的文本标签
    :data: 用于比较的数据
    :column: 用于比较的命名列
    :direction: “peak”或“bottom”之一
