## Unix 特殊变量

之前的教程就在命名变量时，使用某些非字符数值作为字符变量名提出警告。这是因为这些字符用于作为特殊的 Unix 变量的名称。这些变量是预留给特定功能的。

例如，$ 字符代表进程的 ID 码，或当前 shell 的 PID：

    $echo $$

以上命令将输出当前 shell 的 PID：

    29949

下面的表列出了一些特殊变量，可以在你的 shell 脚本中使用它们：
<table>
<tr>
<th>变量</th>
<th>描述</th>
</tr>
<tr>
<td>$0</td>
<td>当前脚本的文件名。</td>
</tr>
<tr>
<td>$n</td>
<td>这些变量对应于调用一个脚本时的参数。n 是一个十进制正整数，对应于特定参数的位置(第一个参数是 $1，第二个参数是 $2 等等)。</td>
</tr>
<tr>
<td>$#</td>
<td>提供给脚本的参数数量。</td>
</tr>
<tr>
<td>$*</td>
<td>所有的参数都表示两个引用。如果一个脚本接收了两个参数，即 $* 相当于 $1$2。</td>
</tr>
<tr>
<td>$@</td>
<td>所有的参数都是两个单独地引用。如果一个脚本接收了两个参数，即 $@ 相当于 $1$2。</td>
</tr>
<tr>
<td>$?</td>
<td>执行最后一个命令的退出态。</td>
</tr>
<tr>
<td>$$</td>
<td>当前 shell 的进程号。对于 shell 脚本，即他们正在执行的进程的 ID。</td>
</tr>
<tr>
<td>$!</td>
<td>最后一个后台命令的进程号。</td>
</tr>
</table>

### 命令行参数:

命令行参数 $1，$2，$3，……$9 是位置参数，$0 指向实际的命令，程序，shell 脚本或函数。$1，$2，$3，……$9 作为命令的参数。

以下脚本使用与命令行相关的各种特殊变量：

    #!/bin/sh
    
    echo "File Name: $0"
    echo "First Parameter : $1"
    echo "Second Parameter : $2"
    echo "Quoted Values: $@"
    echo "Quoted Values: $*"
    echo "Total Number of Parameters : $#"

这是一个运行上述脚本的示例：

    $./test.sh Zara Ali
    File Name : ./test.sh
    First Parameter : Zara
    Second Parameter : Ali
    Quoted Values: Zara Ali
    Quoted Values: Zara Ali
    Total Number of Parameters : 2

### 特殊参数 $* 和 $@：

存在一些特殊参数，使用它们可以访问所有的命令行参数。除非他们包含在双引号 "" 中，否则$* 和 $@ 运行是相同的。

这两个参数都指定所有的命令行参数，但 "$*" 特殊参数将整个列表作为一个参数，各个值之间用空格隔开。而 "$@" 特殊参数将整个列表分隔成单独的参数。

我们可以编写如下所示的shell脚本，使用 $*或 $@ 特殊参数来处理数量未知的命令行参数：

    #!/bin/sh
    
    for TOKEN in $*
    do
       echo $TOKEN
    done

作为示例，运行上述脚本:

    $./test.sh Zara Ali 10 Years Old
    Zara
    Ali
    10
    Years
    Old

**注意**：这里 do……done 是一种循环，我们将在后续教程中介绍它。

### 退出态:

**$?** 变量代表前面的命令的退出态。

退出态是每个命令在其完成后返回的数值。一般来说，大多数命令如果它们成功地执行，将 0 作为退出态返回，如果它们执行失败，则将 1 作为退出态返回。

一些命令由于一些特定的原因，会返回额外的退出状态。例如，一些命令为了区分不同类型的错误，将根据特定类型的失败原因返回各种不同的退出态值。

下面是一个成功命令的例子:

    $./test.sh Zara Ali
    File Name : ./test.sh
    First Parameter : Zara
    Second Parameter : Ali
    Quoted Values: Zara Ali
    Quoted Values: Zara Ali
    Total Number of Parameters : 2
    $echo $?
    0
    $
