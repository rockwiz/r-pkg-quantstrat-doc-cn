getOrders
=========


描述
    该函数存在为了其它代码能发现开放订单，可能要更新或取消它们。

用法
::

    getOrders(portfolio, symbol, status="open", timespan=NULL, ordertype=NULL, side=NULL, qtysign=NULL, which.i=FALSE)

参数
    :portfolio: 与订单薄相关联的投资组合的文本名字
    :symbol: 查找发现订单的证券标识符。任何关联价格对象的名字（xts价格，通常是OHLC）必须与此匹配
    :status: “open”、“closed”、“canceled”或“replaced”之一，缺省为“open”
    :timespan: xts 风格字符型timespan是查找发现给定状态（status）和类型（ordertype）订单的期间
    :ordertype: NULL、“market”、“limit”、“stoplimit”、“stoptrailing”或“iceberg”之一，缺省为NULL
    :side: NULL、“long”或“short”之一，缺省为NULL
    :which.i: 如果为TRUE，返回行索引数而非匹配标准的订单行，缺省为FALSE

说明
    它作为报告或事后分析工具有些用，但并非总是要输出。应该用symbols 代替symbol ？
