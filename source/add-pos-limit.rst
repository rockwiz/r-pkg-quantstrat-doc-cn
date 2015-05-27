addPosLimit
===========

描述
    在时间戳上添加头寸或层级界限。层级（level）是一种用来划分订单大小的更复杂（专用）技术的简化。很明显，返回的最大订单数量（orderqty）是策略规则要求更小的订单规模时的限额或水平。但这是缺省状态下的情况，如果你不想使用层级，可以将它们设为1。

用法
::

    addPosLimit(portfolio, symbol, timestamp, maxpos, longlevels=1, minpos=-maxpos, shortlevels=longlevels)

参数
    :portfolio: 要下订单的投资组合的文本名字
    :symbol: 下订单的证券标识符。任何关联价格对象的名字（xts价格，通常是OHLC）必须与此匹配
    :timestamp: 可强制转换成POSIXct的时间戳，它将是订单要被插入的时间
    :maxpos: 数值型的证券最大头寸
    :longlevels: 数值型的层级数
    :minpos: 数值型的最小头寸，缺省为-minpos （允许用负数表示空头）
    :shortlevels: 数值型空头层级数，缺省为longlevels

参考
    osMaxPos getPosLimit
