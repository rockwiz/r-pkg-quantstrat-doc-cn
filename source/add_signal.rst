add.signal
==========

描述
    向一个策略中添加一个信号。

用法
::

    add.signal(strategy, name, arguments, parameters=NULL, label=NULL, ..., enabled=TRUE, indexnum=NULL, store=FALSE)

参数
    :strategy: 一个要加入信号的“strategy”类型对象
    :name: 信号名称，必须对应一个R函数
    :arguments: 执行时传递给信号函数的缺省参数
    :parameters: 给保存为应用时（apply-time）定义的参数命名的字符串向量，缺省为NULL。仅当需要特殊的名字以避免参数冲突时需要
    :label: 用于指标输出的任意文本标签，NULL缺省地将转换为“<name>.sig”
    :...: 任何其它要传递的参数
    :enabled: TRUE/FALSE。该信号在应用该策略时是否可用，缺省为TRUE
    :indexnum: 如果你更新某个特定信号，$signals 列表中的索引数要更新
    :store: TRUE/FALSE。是否将该策略保存在.strategy环境里，或者返回它。缺省为FALSE
