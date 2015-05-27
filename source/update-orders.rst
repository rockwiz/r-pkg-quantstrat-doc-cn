updateOrders
============

描述
    更新一个或多个订单。当一个订单被填充，它应该将其状态改为“封闭的”（“closed”）。

用法
::

    updateOrders(portfolio, symbol, timespan, ordertype=NULL, side=NULL, qtysign=NULL, oldstatus="open", newstatus, statustimestamp)

参数
    :portfolio: 与订单薄相关联的投资组合的文本名字
    :symbol: 查找订单的证券标识符。任何关联价格对象的名字（xts价格，通常是OHLC）必须与此匹配
    :timespan: xts 风格字符型timespan是查找发现给定状态（status）和类型（ordertype）订单的期间
    :ordertype: NULL、“market”、“limit”、“stoplimit” 或“stoptrailing”之一，缺省为NULL
    :side: NULL、“long”或“short”之一，缺省为NULL
    :oldstatus: NULL、“open”、“closed”、“canceled”或“replaced”之一，缺省为“open”
    :newstatus: “open”、“closed”、“canceled”或“replaced”之一
    :statustimestamp: 状态更新的时间戳，订单初始化时为空

说明
    当订单被一个新订单更新时，订单状态应改为“replaced’”，以及一个和新订单同样的状态时间（StatusTime）。这在传统由于追踪止损的取消/替换（Cancel/Replace）情况下会发生，或者出现在需要输入一个替换过的订单作为提示的部分填充（partial fill）情况下。

    当一个风险事件或超限事件（over-limit）发生时，典型地，开放订单将被取消（“canceled”）。可能要添加新订单以出清开放头寸（open positions）。许多模型也要在市场收盘时运行一个取消所有开放订单的程序。
