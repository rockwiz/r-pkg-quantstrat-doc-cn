paramConstraint
===============

描述
    生成比较信号。目前，该函数比较两列。很高兴接受可以比较任意列的补丁。基本与signal.R 中Brian 编写的sigComparison 函数相同，只有少量修改。

用法
::

    paramConstraint(label, data = mktdata, columns, relationship=c("gt", "lt", "eq", "gte", "lte"))

参数
    :label: 应用到输出的文本标签
    :data: 用于比较的数据
    :columns: 用于比较的命名列
    :relationship: c("gt","lt","eq","gte","lte","op") 或其它合理的替代

说明
    比较应用到列向量中第一列到第二列。

    关系“op”意指相反（“opposite”）方向。将进行合理尝试来匹配。
