sigFormula
==========

描述
    从一个公式中生成信号。该代码利用一些能将一个R对象（这种情况下是quantstrat内部的mktdata对象）作为环境或利用parent.frame 将其作为框架（“frame’”）对待的基本R功能。这允许简单地通过列名就能定位数据列，而不需要任何大的操作。quantstrat 的大多数情况，这将要么是价格/收益列，要么是指标或之前信号添加的列。该公式将为每行比较返回TRUE/FALSE，作为随后被用于规则执行的时间序列的列。公式将用 eval解析，即便在if语句中。

用法
::

        sigFormula(label, data = mktdata, formula, cross = FALSE)

参数
    :label: 应用到输出的文本标签
    :data: 用于公式的数据
    :formula: 一个逻辑表达式，与常用的if语句相似。典型地引用mktdata 中的列名字
    :cross: 如果为TRUE，运行中将只对第一个匹配公式的观测值返回TRUE

说明
    该代码改编自Vijay Vaidyanthan 在他用来构造任意、公式化和比较的PAST(AAII/SIPRO) 代码中的方法。非常感谢Vijay分享他的专长。
