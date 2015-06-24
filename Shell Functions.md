##Unix - Shell 函数

 函数允许你将一个脚本的整体功能分解成更小的逻辑子部分，然后当需要的时候可以被调用来执行它们各自的任务。

使用函数来执行重复性的任务是一个创建代码重用的很好的方式来。代码重用是现代面向对象编程的原则的重要组成部分。

Shell函数类似于其他编程语言中的子程序和函数。

###创建函数：

声明一个函数，只需使用以下语法：

    function_name () { 
       list of commands
    }

函数的名字是 function_name，在脚本的其它地方你可以用函数名调用它。函数名后必须加括号，在其后加花括号，其中包含了一系列的命令。

###例子：

以下是使用函数的简单例子：

    #!/bin/sh
    
    # Define your function here
    Hello () {
       echo "Hello World"
    }
    
    # Invoke your function
    Hello

当你想执行上面的脚本时，它会产生以下结果：

    $./test.sh
    Hello World
    $

###函数的参数传递：

你可以定义一个函数，在调用这些函数的时候可以接受传递的参数。这些参数可以由 $1，$2 等表示。

以下是一个例子，我们传递两个参数 *Zara* 和 *Ali* ，然后我们在函数中捕获和编译这些参数。

    #!/bin/sh
    
    # Define your function here
    Hello () {
       echo "Hello World $1 $2"
    }
    
    # Invoke your function
    Hello Zara Ali

这将产生以下结果：

    $./test.sh
    Hello World Zara Ali
    $

###函数返回值：

如果你从一个函数内部执行一个 exit 命令，不仅能终止函数的执行，而且能够终止调用该函数的 Shell 程序。

如果你只是想终止该函数的执行，有一种方式可以跳出定义的函数。

根据实际情况，你可以使用 **return** 命令从你的函数返回任何值，其语法如下：

    return code

这里的 *code* 可以是你选择的任何东西，但很明显，考虑到将脚本作为一个整体，你应该选择有意义的或有用的东西。

###例子：

下面的函数返回一个值 1：

    #!/bin/sh
    
    # Define your function here
    Hello () {
       echo "Hello World $1 $2"
       return 10
    }
    
    # Invoke your function
    Hello Zara Ali
    
    # Capture value returnd by last command
    ret=$?
    
    echo "Return value is $ret"

这将产生以下结果：

    $./test.sh
    Hello World Zara Ali
    Return value is 10
    $

###嵌套函数：

函数更有趣的功能之一就是他们可以调用本身以及调用其他函数。调用自身的函数被称为递归函数。

下面简单的例子演示了两个函数的嵌套：

    #!/bin/sh
    
    # Calling one function from another
    number_one () {
       echo "This is the first function speaking..."
       number_two
    }
    
    number_two () {
       echo "This is now the second function speaking..."
    }
    
    # Calling function one.
    number_one

这将产生以下结果：

    This is the first function speaking...
    This is now the second function speaking...

###从 Prompt 函数调用：

你可以把常用函数的定义放置到文件 *.profile* 中，这样当你载入的时候可以得到它们并且在 prompt 命令中使用它们。

或者，你可以将多个函数定义在一个文件中，比如 *test.sh*，然后通过键入以下内容当前shell中执行该文件：

    $. test.sh

这样做可以使 *test.sh* 内定义的任何函数被读入，定义到当前 shell ，如下：

    $ number_one
    This is the first function speaking...
    This is now the second function speaking...
    $

要从 shell 删除函数的定义，你可以使用带 .f 选项的 unset 命令。这也是用来删除 shell 中一个变量的定义的命令。

    $unset .f function_name