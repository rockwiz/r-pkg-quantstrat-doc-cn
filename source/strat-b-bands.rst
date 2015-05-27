stratBBands
===========

描述
    实现布林带策略的策略对象。

用法
::

    data('stratBBands')

说明
    1. 指标

        该策略仅使用一个指标，由TTR函数BBands 组成。指标参数包含MA期数和波带标准差大小。

        如果从头开始构建，指标应由以下组成：

        (1) 一个由MA类型（简单、指数、卡尔曼等）和需要平滑的MA期数决定的移动平均；
        (2) 上轨线，上轨线经典地由移动平均线加上标准差构成，或者可替代地由其它主要根据波带振幅，典型是中点或移动平均指标的标准差数，参数化的函数生成；
        (3) 下轨线，下轨线传统的构造为上轨线的对称和相反位置，但也可能不同的函数或参数与上轨线不同的函数构成。

    2. 信号

        经典的布林带策略依赖上、下轨线和中轨线的穿越事件（信号）

        (1) Cl.gt.UpperBand类型sigCrossover，如果收盘价高于上轨线的值。
        (2) Cl.lt.LowerBand类型sigCrossover，如果收盘价低于下轨线的值。
        (3) Cross.mid类型 sigCrossover，在任何点，如果价格穿过中轨线。

    3. 规则

        该策略中，每个信号都有一个对应的进入或退出规则。

    4. 进入

        (1) 进入型ruleSignal，当出现Cl.gt.UpperBand 信号，以市价输入一个卖出订单。
        (2) 进入型ruleSignal，当出现Cl.lt.LowerBand 信号，以市价输入一个买入订单。

    5. 退出

        退出型ruleSignal，当出现Cross.mid 信号，以市价出清所有开放头寸（open position）。

    6. 备注

        该策略可通过以下方式得到改善：

        (1) 采样追踪进入或退出订单
        (2) 使用一个与SMA不同的平滑机制
        (3) 额外的止损规则

参考
    | http://www.investopedia.com/articles/trading/07/bollinger.asp
    | http://www.mysmp.com/technical-analysis/bollinger-bands.html
    | http://trading-strategies.netfirms.com/trading/bollingerbandtactics.htm

    关于布林带的原理和使用，请参阅拙作《K线图形态和常用技术指标使用手册》（P183）
