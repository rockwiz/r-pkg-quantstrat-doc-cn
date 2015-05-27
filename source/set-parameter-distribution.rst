setParameterDistribution
========================

描述
    用于设定一个策略参数分布的函数。

用法
::

    setParameterDistribution(paramDist=NULL, type=NULL, indexnum=0, distribution=NULL, weight, label, psindex=NULL)

参数
    :paramDist: 存储参数列表的对象的名字
    :type: indicator/signal/enter/exit/order之一
    :indexnum: 告知同类中的序列（如果type是signal，indexnum=2意味策略中的第二个信号）
    :distribution: 参数的分布，可以是任何返回一个向量的函数（例如，1:10 或 sample(1:20,6)）
    :weight: 分布中每个值的权重，缺省值将是等权重
    :psindex: 指定参数分布对象中的索引，用于改变/替换对象中的参数分布
