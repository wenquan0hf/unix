## Unix 使用 Shell 数组

一个 shell 变量只能够容纳一个值。这种类型的变量称为标量变量。

Shell 数组变量可以同时容纳多个值，它支持不同类型的变量。数组提供了一种变量集分组的方法。你可以使用一个数组变量存储所有其他的变量，而不是为每个必需的变量都创建一个新的名字。

Shell 变量中讨论的所有命名规则都将适用于命名数组。

### 定义数组值

一个数组变量和一个标量变量之间的差异可以解释如下。

假如你想描绘不同学生的名字，你需要命名一系列变量名作为一个变量集合。每一个单独的变量是一个标量变量，如下所示：

    NAME01="Zara"
    NAME02="Qadir"
    NAME03="Mahnaz"
    NAME04="Ayan"
    NAME05="Daisy"

我们可以使用一个数组来存储所有上面提到的名字。下面是创建一个数组变量的最简单的方法，将值赋给数组的一个索引。表示如下：

    array_name[index]=value

这里 array_name 是数组的名称，index 是数组中需要赋值的索引项，value 是你想要为这个索引项设置的值。

例如,以下命令:
    
    NAME[0]="Zara"
    NAME[1]="Qadir"
    NAME[2]="Mahnaz"
    NAME[3]="Ayan"
    NAME[4]="Daisy"

如果使用 **ksh** shell，数组初始化的语法如下所示：

    set -A array_name value1 value2 ... valuen

如果使用 **bash** shell，数组初始化的语法如下所示：

    array_name=(value1 ... valuen)

### 访问数组值:

在为数组变量赋值之后，你可以访问它。如下所示：

    ${array_name[index]}

这里 array_name 是数组的名称，index是将要访问的值的索引。下面是一个最简单的例子：

    #!/bin/sh
    
    NAME[0]="Zara"
    NAME[1]="Qadir"
    NAME[2]="Mahnaz"
    NAME[3]="Ayan"
    NAME[4]="Daisy"
    echo "First Index: ${NAME[0]}"
    echo "Second Index: ${NAME[1]}"

这将产生以下结果：

    $./test.sh
    First Index: Zara
    Second Index: Qadir

你可以使用以下方法之一，来访问数组中的所有项目：

    ${array_name[*]}
    ${array_name[@]}

这里 array_name 是你感兴趣的数组的名称。下面是一个最简单的例子：

    #!/bin/sh
    
    NAME[0]="Zara"
    NAME[1]="Qadir"
    NAME[2]="Mahnaz"
    NAME[3]="Ayan"
    NAME[4]="Daisy"
    echo "First Method: ${NAME[*]}"
    echo "Second Method: ${NAME[@]}"

这将产生以下结果：

    $./test.sh
    First Method: Zara Qadir Mahnaz Ayan Daisy
    Second Method: Zara Qadir Mahnaz Ayan Daisy