stratFaber
==========

描述
    法布尔市场时机策略。法布尔（Faber）的文章（2007）提出了一个非常简单的量化市场时机模型。他们以美国1900年以来的数据为样本对该模型进行了检验，之后又对其它20个市场进行了样本外（out-of-sample）检验。

用法
::

    data('stratFaber')

说明
    法布尔的文章探讨了Jeremy Seigel 关于道琼斯指数（DJIA）时机的著作《Stocks for the Long Run》（1994）中提出的200天移动平均策略。他得出结论说，一个简单的市场时机策略相对买入-持有策略提升了绝对收益和风险调整（risk adjusted）收益。将所有交易成本包括进去后，绝对收益有所不足，但仍能获得较好的风险调整收益。Siegel 也检验了纳斯达克（NASDAQ）综合指数1972年以来的情况，发现有更好的绝对收益和风险调整收益。

    这篇文章通过选取10-月SMA，实现了一个200-天SMA的简化版本。对长时期范围，月度数据更易得到，而较小的间隔也会转换成较小的交易成本。

    系统的规则相对简单：

    (1) 当月价格大于10-月SMA，买入
    (2) 当月价格小于10-月SMA ，转成现金
    (3) 所有的进入和退出价格都是信号出现日的收盘价
    (4) 所有时间序列都是包括分红、每月更新的总收益。出于演示（demo）目的，我们只使用价格收益
    (5) 现金收益以90天商业票据估计。杠杠模型的保证金率（margin rates）以经纪商活期贷款利率（call rate）估计。再次，出于演示策略的目的，我们忽略了利息和杠杠（尽管它们可以在框架中建模）
    (6) 没有包含佣金和滑价（尽管它们可以在框架中建模）
    (7) 不含税

    这个简单的策略与众所周知的趋势追随系统在三个方面不同：首先，没有做空。卖出信号时头寸转成现金，而非做一个空头交易；其次，这个头寸保持和交易起始时一样。不假设头寸随趋势发展增加；第三，没有止损点。如果趋势迅速反转，系统将一直等到出现卖出信号时，才卖出头寸。

指标
    该策略仅使用一个指标，由TTR函数SMA 组成。该指标的参数只有一个MA期数。

信号
    法布尔策略依赖两个围绕SMA的穿越事件（信号）：

    (1) Cl.gt.SMA类型sigCrossover，如果收盘价高于SMA值
    (2) Cl.lt.SMA类型sigCrossover，如果收盘价低于SMA值

规则
    该策略中，每个信号都有一个相应的进入和退出规则：

    (1) 进入，当价格向上穿越SMA时用Cl.gt.SMA信号在市场上输入一个买入订单。
    (2) 退出，当价格向下穿越SMA时用Cl.lt.SMA信号在市场上输入一个卖出订单。

备注
    该策略在实际运用时，可通过以下方式改进：

    (1) 采样追踪进入或退出订单
    (2) 使用一个不同于SMA的平滑机制
    (3) 添加止损规则
    (4) 添加其它指标值

参考
    * Faber, Mebane T., "A Quantitative Approach to Tactical Asset Allocation." Journal of Risk Management (Spring 2007).
    * Siegel, Jeremy J. Stocks for the Long Run : The Definitive Guide to Financial Market Returns and Long-Term Investment Strategies (4th ed.). 436 pp. McGraw-Hill. 2007. ISBN 9780071494700. (earlier editions 1994, 1998, 2002)
