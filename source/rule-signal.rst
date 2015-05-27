ruleSignal
==========

描述
    信号发生时生成交易订单的缺省规则。pricemethod是以下之一：

    * “market”、“opside”或“maker”，在你买入时将用卖出价（“ask”），卖出时，则用买入价（“bid”）。跨过订单条目（order entry）时的市价以试图设定一个积极价格（aggressive price）来达成交易。
    * “passive”、“work” 或“join”，在你买入时将结合买入价（“bid”），卖出时，则结合卖出价（“ask”）。消极（passively）工作以当时市价来制造流动性，而不跨过订单条目时的市价。
    * “maker”将创建一对订单分别处于买卖两边为造市（market making）活动建模。然后这将创建一个Order.Set，并用阈值为时刻t设定价格。

用法
::

    ruleSignal(data=mktdata, timestamp, sigcol, sigval, orderqty=0, ordertype, orderside=NULL, threshold=NULL, tmult=FALSE, replace=TRUE, delay=1e-04, osFUN="osNoOp", pricemethod=c("market", "opside", "maker"), portfolio, symbol, ..., ruletype, TxnFees=0, prefer=NULL, sethold=FALSE)

参数
    :data: 一个包含市场数据的xts对象。根据规则不同，可能需要是OHLCV 或BBO格式，也许包括指标和信号信息
    :timestamp: 可强制转换成POSIXct的时间戳，它将是订单要被插入的时间
    :sigcol: 检查信号的列名字
    :sigval: 匹配的信号值
    :orderqty: 期望订单的数值型数量，或“all”，由osFUN 修改
    :ordertype: NULL、“market”、“limit”、“stoplimit”、“stoptrailing”或“iceberg”之一
    :orderside: “long”或“short”之一，缺省为NULL，参见说明部分
    :threshold: 应用于追踪止损订单的数值型或函数阈值，缺省为NULL，参见说明部分
    :tmult: 如果为TRUE，阈值为一个价格的百分比乘数因子，而非一个加到价格上或从价格中减去的标量。阈值在订单输入时将会被动态转换为标量
    :replace: TRUE/FALSE，是否替换其它任何有关此投资组合证券的开放订单，缺省为TRUE
    :delay: 将订单插入到订单薄时，多少延迟加到时间戳，以秒计
    :osFUN: 函数或用于分割订单12的函数的文本描述符，缺省为osNoOp
    :pricemethod: 确定订单价格如何计算，参见说明部分
    :portfolio: 要下订单的投资组合的文本名字
    :symbol: 下订单的证券标识符。任何关联价格对象的名字（xts价格，通常是OHLC）必须与此匹配
    :...: 任何其它要传递的参数
    :ruletype: “risk”、“order”、“rebalance”、“exit”、“entry”之一，参见add.rule
    :TxnFees: 数值型费用（通常为负数）或计算TxnFees 的函数的名字（处理过程随后开始，不在此函数中）
    :prefer: price method for getPrice
    :sethold: 布尔值，暂时中止条目规则处理，缺省为FALSE

说明
    如果阈值不是数值型或为NULL，它应该是一个字符串描述能计算阈值的函数。理想情况下，这将是一个提前计算的非路径依赖指标上的列查找。

    如果orderside为NULL，该函数将试图从当前头寸（如果有）、订单数量和订单类型计算订单方向（side）。

参考
    osNoOp , add.rule
