
applySignals
============

描述
    将策略中的信号应用于任意市场数据。

用法
::

    applySignals(strategy, mktdata, indicators=NULL, parameters=NULL, ...)

参数
    :strategy: 一个要加入信号的“strategy”类型对象
    :mktdata: 一个包含市场数据的xts对象。根据指标不同，可能需要是OHLCV 或BBO格式
    :indicators: 通过指标输出没有包含在mktdata 对象中，它也许单独作为一个xts对象或列表传递
    :parameters: 策略解析期间用到的参数的命名列表
    :...: 任何其它要传递的参数
