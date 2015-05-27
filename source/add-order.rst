addOrder
========

描述
    向一个指令册中添加订单。quantstrat 中包含的指令函数要建立在回溯检验和实盘两方面都接近实际交易环境的模型，理解这一点很主要。许多回溯检验系统包含“立即执行”的假设，在quantstrat 中，我们选择不这样做，因为真正的量化交易系统没有“立即执行”。它们作出决策（规则），然后输入指令（函数在回溯检验时的职责），在这过程中，接收触发信号和规则的数据与指令（订单）达到市场的时间之间会有一些延迟，然后，如果市场价格与流动性匹配，那些订单才可能成为交易。

用法
::

    addOrder(portfolio, symbol, timestamp, qty, price, ordertype, side, threshold=NULL, status="open", statustimestamp="", delay=1e-05, tmult=FALSE, replace=TRUE, return=FALSE, ..., TxnFees=0)

参数
    :portfolio: 与订单薄关联的投资组合的文本名字
    :symbol: 查找订单的证券标识符。任何关联价格对象的名字（xts价格，通常是OHLC）必须与此匹配
    :timestamp: 可强制转换成POSIXct的时间戳，它将是在此之前搜索订单的时间
    :qty: 订单的数值型数量
    :price: 数值型价格，订单以此值插入
    :ordertype: “market”、“limit”、“stoplimit”、“stoptrailing”或“iceberg”之一
    :side: “long”或“short”之一
    :threshold: 应用于追踪止损订单的数值型阈值，缺省为NULL
    :status: “open”、“closed”、“canceled”或“replaced”之一，缺省为“open”
    :statustimestamp: 状态更新的时间戳，订单初始化时为空
    :delay: 将订单插入到订单薄时，多少延迟加到时间戳，以秒计
    :tmult: 如果为TRUE，阈值为一个价格的百分比乘数因子，而非一个加到价格上或从价格中减去的标量。阈值在订单输入时将会被动态转换为标量
    :replace: TRUE/FALSE，是否替换其它任何有关此投资组合证券的开放订单，缺省为TRUE
    :return: 如果为TRUE，返回组成订单的行，缺省为FALSE（将其赋值到环境中）
    :...: 任何其它要传递的参数
    :TxnFees: 数值型费用（通常为负数）或计算TxnFees 的函数的名字（处理过程随后开始，不在此函数中）

说明
    缺省状态下，该函数将定位并替换具有相同类型和方向的任何针对请求的投资组合/证券的“开放”订单（“open” orders）。这等价于有时被称为二择一委托5的订单。如果你不希望函数以这种方式工作，设定replace=FALSE 。

    我们建立了两种止损单（stop order）模型，足够应对大多数止损类型。

    最简单的类型是限价止损单（stoplimit order），它是一种在指定价位进入或退出头寸的限价指令。也可以给限价止损加上阈值乘数（threshold multiplier），它允许将阈值设定为当前价格的倍数。例如，要将限价止损设为当前价格加上10%，你可以将阈值乘数设为1.10。阈值乘数（或标量）在指令条目上将被转换成一个价格。

    一旦进入订单薄，普通“限价”单和“止损限价”单在功能上没有什么不同，但是两者的区别在报告何时止损被触发比较有用。

    我们也为追踪止损单（stoptrailing order）建立了模型，它用于建模动态限价进入或退出。如果你在追踪止损单上设定tmult=TRUE，阈值的大小将被设为乘数因子乘以价格与订单薄当前价格之差。在这种方式下，a 10 change in size from the current price as the price changes6。它在订单条目上被有效地转换成一个标量。随着该功能在未来可能变化，我们相信在阈值方面这样做比从当前市场价格扩大或缩小阈值距离更留有余地，并将产生较少的意外影响和可读性更好的行为。

    “stop”和“iceberg”是利用订单阈值的仅有类型。在限价止损（stoplimit）或追踪止损（stoptrailing）单上的标量阈值（scalar thresholds）tmult=FALSE将被加到当前市场价格以设定限制价位。换句话说，标量阈值是订单输入时当前价格正或负的差额。对追踪止损单而言，订单可能会（通过cancel/replace）频繁移动。

    一些市场和经纪商认可触发市价单（market order）的止损条件。当止损触发时，市价单将在当时价位（then-prevailing price）上被执行。我们没有给这类订单建模。

    我们也增加了“iceberg”订单类型。这种类型应该最经常与delay和osMaxPos配对使用。冰山单（iceberg order）在初始输入时被当做带有可选阈值（它应用于初始订单条目，所以应小心）的限价单对待。现在，它们将输入一张新订单，其价位是价格+任何之前冰山单执行时的阈值。如果没有用osMaxPos或等同的订单规模函数（order sizing function）限制总的头寸规模，该过程可能会无限进行下去。为之前交易确认和输入新订单到订单薄之间发生的延迟建模也是可取的。

    如果要从回溯检验（backtesting）模式转移到实盘（production）模式，该函数（以及相联系的函数ruleOrderProc）需要替换成可以工作在你的执行环境中的函数。

    从根本上说，执行环境必须一个真实的交易环境的三个接口：

    1. 一个市场数据接口，提供更新后的市场数据，通常以时间循环的方式存取
    2. 一个订单接口，发送订单到市场，或取消（或更新）到市场的订单
    3. 一个填充（fill）接口，当订单被加载（filled）后，报告交易细节

    转换到真实的交易环境也很可能需要applyStrategy的一个新版本来提供事件循环接口并与mktdata相互作用。
