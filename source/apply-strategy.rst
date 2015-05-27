applyStrategy
=============

描述
    将策略应用到任意市场数据。如果mktdata 是NULL，缺省地，mktdata 变量将通过调用一个get（getSymbols??, not yet）为每个证券填充？

用法
::

    applyStrategy(strategy, portfolios, mktdata=NULL, parameters=NULL, ..., verbose=TRUE)

参数
    :strategy: 一个要加入指标的“strategy”类型对象
    :portfolios: 一个要应用策略的投资组合列表
    :mktdata: 一个包含市场数据的xts对象。根据指标不同，可能需要是OHLCV 或BBO格式。缺省为NULL
    :parameters: 策略解析期间用到的参数的命名列表，缺省为NULL
    :...: 任何其它要传递的参数
    :verbose: 如果为TRUE，返回输出列表
