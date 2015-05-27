applyParameter
==============

描述
    测试一个策略的不同参数设置。给定一个由setParameterDistribution 函数生成的参数分布对象，生成参数集，并对指定策略检验每个参数集。

用法
::

    applyParameter(strategy, portfolios, parameterPool, parameterConstrains, method, sampleSize)

参数
    :strategy: 一个要加入参数的“strategy”类型对象
    :portfolios: 要应用的投资组合
    :parameterPool: 一个由setParameterDistribution 函数创建的参数分布对象，它包括所有参数合法值和分布/权重
    :parameterConstrains: setParameterConstraint 函数创建的指定每个参数间约束的对象
    :method: 取字符串“expand”或“random”，指定如何生成参数样本。“expand”将作参数集的所有可能组合
    :sampleSize: 用于当method==’random’时，指定多少参数集来生成和运行检验

说明
    在返回的对象中：$eachRun 包含以每个参数集运行检验的细节。$paramTable 是所有的参数样本，以表格方式用于打印输出。$paramConstrainTable 是应用于参数的约束，以表格方式用于打印输出。$parameterDistribution 是作为函数形参7传递的参数分布。$parameterConstrains 是应用于参数的约束，作为函数形参传递。
