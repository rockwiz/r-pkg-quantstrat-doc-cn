sigCrossover
============

描述
    这将生成一个穿越信号，它是比较信号sigComparison 的降维版本。

用法
::

    sigCrossover(label, data = mktdata, columns, relationship=c("gt", "lt", "eq", "gte", "lte"))

参数
    :label: 应用到输出的文本标签
    :data: 用于穿越的数据
    :columns: 用于第一列相对第二列穿越的命名列
    :relationship: c("gt","lt","eq","gte","lte")或其它合理的替代

说明
    它将对由relationship 指定的方向上有一个穿越（crossover）的期间返回TRUE，否则返回NA。

    如果需要所有信息，用comparison代替。
