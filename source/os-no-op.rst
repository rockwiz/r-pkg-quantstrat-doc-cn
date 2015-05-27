osNoOp
======

描述
    缺省函数不执行操作（NoOp），返回orderqty。

用法
::

    osNoOp(timestamp, orderqty, portfolio, symbol, ruletype, ...)

参数
    :timestamp: 可强制转换成POSIXct的时间戳，它将是订单要被插入的时间
    :orderqty: 期望订单的数值型数量，由osFUN 修改
    :portfolio: 要下订单的投资组合的文本名字
    :symbol: 下订单的证券标识符。任何关联价格对象的名字（xts价格，通常是OHLC）必须与此匹配
    :...: 任何其它要传递的参数
    :ruletype: “risk”、“order”、“rebalance”、“exit”、“enter”之一，参见add.rule

说明
    如果orderqty 是“all”，将只工作于一个退出规则类型；否则，orderqty 是零。
