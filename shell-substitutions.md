##UNIX- Shell 替代

###什么是替代？

当它遇到包含一个或多个特殊字符的表达式时 shell 执行替代。

###例：

以下是一个例子，在这个例子中，变量被其真实值所替代。同时，“\n” 被替换为换行符：

    #!/bin/sh
    
    a=10
    echo -e "Value of a is $a \n"

这会产生以下结果。在这里 **-e** 选项可以解释反斜杠转义。

    Value of a is 10

下面是没有 -e 选项的结果：

    Value of a is 10\n

这里有以下转义序列可用于 echo 命令：

<table>
	<tr><th>Escape</th><th>Description</th></tr>
	<tr><td><strong>\\</strong></td><td>反斜杠</td></tr>
	<tr><td><strong>\a</strong></td><td>警报(BEL)</td></tr>
	<tr><td><strong>\b</strong></td><td>退格键</td></tr>
	<tr><td><strong>\c</strong></td><td>抑制换行</td></tr>
	<tr><td><strong>\f</strong></td><td>换页</td></tr>
	<tr><td><strong>\n</strong></td><td>换行</td></tr>
	<tr><td><strong>\r</strong></td><td>回车</td></tr>
	<tr><td><strong>\t</strong></td><td>水平制表符</td></tr>
	<tr><td><strong>\v</strong></td><td>垂直制表符</td></tr>
</table>

默认情况下，你可以使用 -E 选项来禁用反斜线转义解释。

你你可以使用 -n 选项来禁用换行的插入。

命令替换：

命令替换是一种机制，通过它 shell 执行给定的命令，然后在命令行替代他们的输出。

###语法：

当给出如下命令时命令替换就会被执行：

    `command`

当执行命令替换确保你使用反引号，而不是单引号字符。

###例：

命令替换一般是用来分配一个命令的输出变量。下面的示例演示命令替换：

    #!/bin/sh
    
    DATE=`date`
    echo "Date is $DATE"
    
    USERS=`who | wc -l`
    echo "Logged in user are $USERS"
    
    UP=`date ; uptime`
    echo "Uptime is $UP"

这会产生以下结果：

    Date is Thu Jul  2 03:59:57 MST 2009
    Logged in user are 1
    Uptime is Thu Jul  2 03:59:57 MST 2009
    03:59:57 up 20 days, 14:03,  1 user,  load avg: 0.13, 0.07, 0.15

###变量代换：

变量代换使 shell 程序员操纵基于状态变量的值。

下面的表中是所有可能的替换：

<table>
	<tr><th>Form</th><th>Description</th></tr>
	<tr><td><strong>${var}</strong></td><td>替代 <i>var</i> 的值</td></tr>
	<tr><td><strong>${var:-word}</strong></td><td>如果 <i>var</i> 为空或者没有赋值，<i>word</i> 替代 <b>var</b>。<i>var</i> 的值不改变。</td></tr>
	<tr><td><strong>${var:=word}</strong></td><td>如果 <i>var</i> 为空或者没有赋值， <i>var</i> 赋值为 <b>word</b> 的值。</td></tr>
	<tr><td><strong>${var:?message}</strong></td><td>如果 <i>var</i> 为空或者没有赋值，<i>message</i> 被编译为标准错误。这可以检测变量是否被正确赋值。</td></tr>
	<tr><td><strong>${var:+word}</strong></td><td>如果 <i>var</i> 被赋值，<i>word</i> 将替代 var。<i>var</i> 的值不改变。</td></tr></td></tr>
</table>

###例：

以下是例子用来说明上述替代的各种状态：
    
    #!/bin/sh
    
    echo ${var:-"Variable is not set"}
    echo "1 - Value of var is ${var}"
    
    echo ${var:="Variable is not set"}
    echo "2 - Value of var is ${var}"
    
    unset var
    echo ${var:+"This is default value"}
    echo "3 - Value of var is $var"
    
    var="Prefix"
    echo ${var:+"This is default value"}
    echo "4 - Value of var is $var"
    
    echo ${var:?"Print this message"}
    echo "5 - Value of var is ${var}"
    
这会产生以下结果：

    Variable is not set
    1 - Value of var is
    Variable is not set
    2 - Value of var is Variable is not set
    
    3 - Value of var is
    This is default value
    4 - Value of var is Prefix
    Prefix
    5 - Value of var is Prefix
