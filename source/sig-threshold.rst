sigThreshold
============

描述
    生成一个阈值信号。许多策略，包括RSI或MACD风格的，在指标高于或低于某个设定阈值时做出交易决策。该函数基于这样一个阈值生成合适的信号。

用法
::

    sigThreshold(label, data=mktdata, column, threshold=0, relationship=c("gt", "lt", "eq", "gte", "lte"), cross = FALSE)

参数
    :label: 应用到输出的文本标签
    :data: 用于比较的数据
    :column: 用于比较的命名列
    :threshold: 要检验的数值型阈值
    :relationship: c("gt","lt","eq","gte","lte")或其它合理的替代
    :cross: 如果为TRUE，在运行中将只对第一个穿越阈值的观测值返回TRUE
