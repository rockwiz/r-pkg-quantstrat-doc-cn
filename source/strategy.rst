strategy
========

描述
    “strategy”类型对象构造器。

用法
::

    strategy(name, ..., assets = NULL, constraints = NULL, store = FALSE)

参数
    :name: 策略名称字符串
    :...: 任何其它要传入的参数
    :assets: 应用策略的可选资产列表，正常情况下应该在portfolio 中定义，而不是在这里
    :constraints: 匹配资产的可选组合约束对象
    :store: TRUE/FALSE。是否将该策略保存在.strategy环境里，或者返回它。缺省为FALSE
