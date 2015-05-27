getParameterTable
=================

描述
    从一个strategy 对象中提取参数结构。用户设定参数的分布时不需要该函数。用户可用此函数提取策略中用到的参数，并在他们创建参数分布时作为提示（reminder/ cheatsheet）。

用法
::

    getParameterTable(strategy)

参数
    :strategy: 策略的名字

说明
    在返回的对象中：$paramNameList 是策略中用到的参数列表，作为表格易于打印和查看。$strategyName 是策略本身的名字。$structure是详细的参数结构，可被忽略。
