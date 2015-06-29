# 循环控制

到目前为止你已经学习过创建循环以及用循环来完成不同的任务。有时候你需要停止循环或跳出循环迭代。

在本教程中你将学到以下语句用于控制 Shell 循环：

- **break** 语句
- **continue** 语句

## 无限循环

所有循环都有一个有限的生命周期。当条件为假或真时它们将跳出循环，这取决于这个循环。

一个循环可能会由于未匹配到适合得条件而无限执行。一个永远执行没有终止的循环会执行无数次。因此，这种循环被称为无限循环。

### 例子

这是一个使用 while 循环显示数字 0 到 9 的简单的例子：

```
    #!/bin/sh
    
    a=10
    
    while [ $a -ge 10 ]
    do
       echo $a
       a=`expr $a + 1`
    done
```

这个循环将永远持续下去，因为 a 总是大于或等于 10，它永远不会小于 10。所以这正是无限循环的一个恰当的例子。

## break 语句

所有在 break 语句之前得语句执行结束后执行 break 语句，**break** 语句用于跳出整个循环。然后执行循环体后面的代码。然后在循环结束后运行接下来的代码。

### 语法

以下 **break** 语句将用于跳出一个循环：

```
    break
```
break 语句也可以使用这种格式来退出嵌套循环式：

```
    break n
```

在这里 **n** 指定封闭循环执行的次数然后退出循环。

### 例子

这里是一个简单的例子，用来说明只要 a 变成 5 循环将终止：

```
    #!/bin/sh

    a=0
    
    while [ $a -lt 10 ]
    do
       echo $a
       if [ $a -eq 5 ]
       then
      break
       fi
       a=`expr $a + 1`
    done
```

这会产生以下结果：

```
    0
    1
    2
    3
    4
    5
```

这里是一个简单的嵌套 for 循环的例子。如果 var1 等于 var2 以及 var2 等于 0 ，则这个脚本将跳出这个双重循环：

```
    #!/bin/sh
    
    for var1 in 1 2 3
    do
       for var2 in 0 5
       do
      if [ $var1 -eq 2 -a $var2 -eq 0 ]
      then
     break 2
      else
     echo "$var1 $var2"
      fi
       done
    done
```

这会产生以下结果。在内循环中，有一个 break 命令，其参数为 2。这表明，你应该打破外循环和内循环才能满足条件。

```
    1 0
    1 5
```

## continue 语句

**continue** 语句类似于 break 命令，二者不同之处在于，continue 语句用语结束当前循环，能引起当前循环的迭代的退出，而不是整个循环。

这个语句在当程序发生了错误，但你想执行下一次循环的时候是非常有用的。

### 语法

```
    continue
```

正如 break 语句，一个整型参数可以传递给 continue 命令以从嵌套循环中跳过命令。

```
    continue n
```

在这里 n 指定封闭循环执行的次数然后进入下一次循环。

### 例子

下面是使用 continue 语句的循环，它返回 continue 语句并且开始处理下一个语句：

```
    #!/bin/sh
    
    NUMS="1 2 3 4 5 6 7"
    
    for NUM in $NUMS
    do
       Q=`expr $NUM % 2`
       if [ $Q -eq 0 ]
       then
      echo "Number is an even number!!"
      continue
       fi
       echo "Found odd number"
    done
```

这会产生以下结果：

```
    Found odd number
    Number is an even number!!
    Found odd number
    Number is an even number!!
    Found odd number
    Number is an even number!!
    Found odd number
```