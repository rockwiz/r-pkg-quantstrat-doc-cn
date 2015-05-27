applyIndicators
===============

描述
    将策略中指标应用到任意市场数据。

用法
::

    applyIndicators(strategy, mktdata, parameters=NULL, ...)

参数
    :strategy: 一个要加入指标的“strategy”类型对象
    :mktdata: 一个包含市场数据的xts对象。根据指标不同，可能需要是OHLCV或BBO格式
    :parameters: 策略解析期间应用的参数的命名列表
    :...: 任何其它要传递的参数
