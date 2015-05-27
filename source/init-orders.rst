initOrders
==========

描述
    该函数依投资组合创建订单容器，即初始化订单容器。

用法
::

    initOrders(portfolio=NULL, symbols=NULL, initDate="1999-12-31", ...)

参数
    :portfolio: 与订单薄相关联的投资组合的文本名字
    :symbols: 一个投资组合所包含的证券的标识符列表，任何关联价格对象的名字（xts价格，通常是OHLC）必须与此匹配
    :initDate: mktdata中给定第一个收盘价之前的日期（ISO8601），用于用一个虚订单来（dummy order）初始化订单薄
    :...: 任何其它要传递的参数

说明
    如果没有提供证券代码列表（缺省状态下），该函数将试图从blotter 的投资组合中提取证券列表。
