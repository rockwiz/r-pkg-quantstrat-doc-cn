getPosLimit
===========

描述
    获取某个时间戳上的头寸和层级限额。

用法
::

    add.indicator(strategy, name, arguments, parameters=NULL, label=NULL, ..., enabled=TRUE, indexnum=NULL, store=FALSE)

参数
    :portfolio: 要下订单的投资组合的文本名字
    :symbol: 下订单的证券标识符。任何关联价格对象的名字（xts价格，通常是OHLC）必须与此匹配
    :timestamp: 可强制转换成POSIXct的时间戳，它将是订单要被插入的时间
