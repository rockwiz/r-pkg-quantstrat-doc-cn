add.indicator
=============
描述
    向一个策略中添加一个指标。指标是典型的标准技术分析或统计分析输出，如移动平均、布林带或定价模型。

用法
::

    add.indicator(strategy, name, arguments, parameters=NULL, label= NULL, ..., enabled=TRUE, indexnum=NULL, store=FALSE)

参数
    :strategy: 一个要加入指标的“strategy”类型对象
    :name: 指标名称，必须对应一个R函数
    :arguments: 执行时传递给指标函数的缺省参数
    :parameters: 给保存为应用时（apply-time）定义的参数命名的字符串向量，缺省为NULL。仅当需要特殊的名字以避免参数冲突时需要
    :label: 用于指标输出的任意文本标签，NULL缺省地将转换为“<name>.ind”
    :...: 任何其它要传递的参数
    :enabled: TRUE/FALSE。该指标在应用该策略时是否可用，缺省为TRUE
    :indexnum: 如果你更新某个特定指标，$indicators 列表中的索引数要更新
    :store: TRUE/FALSE。是否将该策略保存在.strategy环境里，或者返回它。缺省为FALSE

说明
    指标总是路径无关的（path-independent），在可能的情况下应该从向量化函数（vectorized functions）中构建。

    指标先于信号和规则应用，指标的输出可作为构建信号或触发规则的输入。

    形参（arguments）和实参（parameters）都是命名列表，描述要传递给指标函数的参数。形参用于定义传递给在指标名字中命名的函数的任何非缺省参数。例如，给移动平均函数的x形参可定义为x=quote(Cl(mktdata))

    如果你看demo脚本，你会注意到我们在建立指标、信号或规则时常常使用quote(mktdata)，这通过quote()告诉R延迟解析，并采用一个特殊变量mktdata 。

    mktdata典型是通过在全局环境中查找价格或收益的时间序列内在地创建给quantstrat 。mktdata 也许包含你在quatstrat 之外操作的其它数据，尽管在可能的情况下，应该用quantstrat 包含所有该策略的逻辑以便维护和更改。

    quote() 的使用告诉R，在函数随后被解析之前不要解析quote中的内容。到代码被解析的时候，mktdata将被填入正确的价格信息，这些价格信息基于任何你要对其进行策略评估的投资组合的内容。

    实参（parameters）是另一个命名列表，通常不需要。如果有多个指标、信号或规则函数，它们共有相同的形参名字，但是在应用时（apply-time）需要传递不同的参数值 ，你需要给它们唯一名以便延后解析能在应用时帮你把它们都甄别出来。

    我们将在演示（demo）脚本中加入命名实参的例子。

参考
    quote
