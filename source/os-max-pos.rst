osMaxPos
========

描述
    针对头寸限额和层级大小的订单分割10函数。层级（level）是一种用来划分订单大小的更复杂（专用）技术的简化。很明显，
    返回的最大订单数量（orderqty）是策略规则要求更小的订单规模时的限额或水平。但这是缺省状态下的情况，如果你不想使用层级，可以将它们设为1。

用法
::

    osMaxPos(data, timestamp, orderqty, ordertype, orderside, portfolio, symbol, ruletype, ...)

参数
    :data: 一个包含市场数据的xts对象。根据规则不同，可能需要是OHLCV或BBO格式，也许包括指标和信号信息
    :timestamp: 可强制转换成POSIXct的时间戳，它将是订单要被插入的时间
    :orderqty: 期望订单的数值型数量，由osFUN 修改
    :ordertype: “market”、“limit”、“stoplimit”或“stoptrailing”之一
    :orderside: “long”或“short”之一
    :portfolio: 要下订单的投资组合的文本名字
    :symbol: 下订单的证券标识符。任何关联价格对象的名字（xts价格，通常是OHLC）必须与此匹配
    :ruletype: “risk”、“order”、“rebalance”、“exit”、“enter”之一，参见add.rule
    :...: 任何其它要传递的参数

说明
    在风险规则中，orderqty=’all’将返回一个出清当前头寸的订单大小。

备注
    TODO 将通过连结side和pos退出为非风险退出订单把orderqty=’all’集成进osMaxPos

参考
    addPosLimit、getPosLimit
