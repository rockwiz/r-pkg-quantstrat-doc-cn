ruleOrderProc
=============

描述
    处理时刻_t_的开放订单，生成交易或新订单。ruleOrderProc函数是quantstrat 缺省的高效填充模拟器。该函数目标是足够应对大多数策略的
    回溯检验，但在实盘使用时需要被替换。它提供获取订单薄和判定何时订单变成交易的接口。

用法
::

    ruleOrderProc(portfolio, symbol, mktdata, timespan=NULL, ordertype= NULL, ..., slippageFUN=NULL)

参数
    :portfolio: 与订单薄相关联的投资组合的文本名字
    :symbol: 用来查找订单的证券标识符，任何关联价格对象的名字（xts价格，通常是OHLC）必须与此匹配
    :mktdata: 一个包含市场数据的xts对象。根据指标不同，可能需要是OHLCV 或BBO格式，缺省为NULL
    :timespan: xts 风格字符型timespan是查找发现要处理订单的期间
    :ordertype: NULL、“market”、“limit”、“stoplimit” 或“stoptrailing”之一，缺省为NULL
    :...: 任何其它要传递的参数
    :slippageFUN: 缺省为 NULL，尚未实现

说明
    为回溯检验和与blotter 中交易记录保持兼容，该函数不允许使你当前头寸穿越零值的交易。这种情况下，实现收益的记账规则比我们希望支持的复杂。许多经纪商出于同样的理由，也会中断、修改或分拆这样的交易。如果你做一个“止损反转”系统，先止损（出清），然后再反转（发起一个新头寸）。

    要连接到真实的交易基础设施，需要修改或替换该函数。在实盘模式下，需要用一个定制函数取代addOrder 函数连到你的市场基础设施。这种情况下，你也许需要在你策略中增加一些额外的代码，或重载函数以检查头寸。

    注意，该函数缺省在applyRules 过程订单槽口（’orders’ slot）中调用。如果你定义了另外的订单处理规则，它将替换该函数。如果要你的定制订单规则和ruleOrderProc 都被调用，需要显式地增加一条规则在你定制的订单处理函数之前或之后调用ruleOrderProc。

    我们想在这里通过slippageFUN 为滑价（slippage）建模。感谢任何代码贡献、建议和需求。
