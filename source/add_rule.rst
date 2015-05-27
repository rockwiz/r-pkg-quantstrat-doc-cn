add.rule
========

描述
    向一个策略中添加一个规则，规则将被以一种非常特别的方式处理，因此需要仔细查看。

用法
::

    add.rule(strategy, name, arguments, parameters=NULL, label=NULL, type=c(NULL, "risk", "order", "rebalance", "exit", "enter"), ..., enabled=TRUE, indexnum=NULL, path.dep=TRUE, timespan=NULL, store=FALSE)

参数
    :strategy: 一个要加入规则的“strategy”类型对象
    :name: 规则名称，必须对应一个R函数
    :arguments: 执行时传递给规则函数的缺省参数
    :parameters: 给保存为应用时（apply-time）定义的参数命名的字符串向量，缺省为NULL。仅当需要特殊的名字以避免参数冲突时需要
    :label: 用于指标输出的任意文本标签，NULL缺省地将转换为“<name>. rule’”
    :type: 以下之一：“risk”、“order”、“rebalance”、“exit”、“enter”，参见说明部分
    :...: 任何其它要传递的参数
    :enabled: TRUE/FALSE。该规则在应用该策略时是否可用，缺省为TRUE
    :indexnum: 如果你更新某个特定规则，$rules[type]列表中的索引数要更新
    :path.dep: TRUE/FALSE规则是否为路径依赖，缺省为TRUE，参见说明部分
    :timespan: 一个xts/ISO-8601 风格时间子集，像“T08:00/T15:00”，参见说明部分
    :store: TRUE/FALSE。是否将该策略保存在.strategy环境里，或者返回它。缺省为FALSE

说明
    首先，规则要么是路径依赖（path dependent），要么非路径依赖（non-path-dependent）的。 路径依赖的规则在每次mktdata 传递给applyStrategy形成递增时都将被处理；非路径依赖规则在现实生活中非常少见， 它的应用是在指标和信号发生之后，路径依赖规则处理之前。

    所有的规则都有一个类型，它们可能是以下之一：

        * risk 规则检查并对头寸的风险作出反应，可能暂停执行所有其它规则
        * permanently针对开放订单2在时刻t时的处理规则，总是路径依赖型
        * rebalance 专门在投资组合情况下执行的规则，在单变量策略时不需要
        * exit 确定是否出清一个头寸的规则
        * enter 确定是否建立或增加一个头寸的规则

    这些规则将按其类型以上述顺序执行。每种类型可能与对信号和指标一样定义了多个规则，它们与同样类型的规则之间将根据其索引数顺序执行。

    这些规则的执行顺序被构建，因为路径依赖型规则可能改变已被解析但尚未触发的规则的能力。例如，一个风险（risk）规则可能出清所有头寸，并暂时中止新订单，有效地停止策略进一步执行。另一个例子是一个再平衡（rebalancing）规则函数，它将输入订单来重新平衡投资组合，并暂停其它策略的处理，直到再平衡过程结束。

    timespan参数用基于时间的子集限制规则在一天中的执行时间。有关细节，参见ISO-8601规范和xts文档。注意，它们仅对日内交易有效，并将保持这种方式，禁止除了补丁（测试和文档）之外的相关修改。时间子集也许（很可能）适合普通ISO/xts子集范围，但认为它不支持3。

    name参数应该是表示在applyRules循环中被调用函数的名字的字符串。add.rule函数然后调用match.fun函数，并将实际函数保存在你的策略对象中。这将避免在执行applyRules时通过match.fun来查找，从而也许在处理高频数据获得相当大的速度提升（20%或更多）。

    我们预计规则将是策略的一部分，而本程序包很可能没有合适的模板代码，因为每个策略和环境不一样，尤其在这一方面。我们将提供足够的范例和通用规则以给策略制定者一个起点。

    为了quantstrat能够（大量地）向量化路径依赖规则解析的执行，规则函数假定有一个像ruleSignal一样的函数签名，尤其是sigcol和sigval参数。如果它们是与ruleSignal类似方式的函数，我们可以做些预处理来大大减少循环索引的维数。速度提升的比率是(symbols*total observations)/signal observations，因此它对许多策略非常有意义。
