# Unix-什么是Shell脚本 #

shell 是用户访问 unix 操纵系统的接口。它接收用户的输入，然后基于该输入执行程序。程序执行完后，结果会显示在显示器上。

shell 就是运行指令、程序和 shell 脚本的运行环境。就和操作系统可以有很多种类一样，shell 也有很多种。每一种 shell 都有其特定的指令和函数集。  

## Shell 提示符 ##

提示符 $ 被称为命令提示符。当显示命令提示符后，用户就可以键入命令。  

shell 在用户按 Enter 键后，从用户输入设备读入输入信息，它通过查看用户输入的第一个单词，来获知用户想要执行的命令。一个字即使字符不分割组成的字符串，一般是空格和制表符分割字。

下面是在显示器上显示当前日期和时间的 **date** 指令的例子：

    $date
    Thu Jun 25 08:30:19 MST 2009

用户也可以定制自己喜欢的命令提示符，方法是改变环境变量 PS1. 


## Shell 类型 ##

UNIX 系统中有两种主要的Shell：

1. Bourne shell：如果用户使用 bourne shell，默认命令提示符是 $.
1. C shell:如果用户使用 bourne shell，默认命令提示符是 %.

Bourne Shell 也有如下几种子分类：

1. Bourne shell ( sh)
1. Korn shell ( ksh)
1. Bourne Again shell ( bash)
1. POSIX shell ( sh)

C shell不同的类型如下：

1. C shell ( csh)
1. TENEX/TOPS C shell ( tcsh)

最初的 UNIX shell 是 Stephen R. Bourne 在 1970 年代中期写的。当时,他在新泽西的 AT&T 贝尔实验室工作。     

Bourne shell是第一个出现在UNIX系统中的 shell,因此它被称为标准的“shell”。
Bourne shell通常是安装在大多数版本的UNIX中的 /bin/sh 目录。由于这个原因,在不同版本的UNIX上也会选择这种 shell 来编写脚本。
在本教程中,我们将覆盖 Bourne shell 中的大部分概念。  

## Shell 脚本 ##


shell 脚本的主要形式就是一系列的命令，这些命令会顺序执行。良好风格的 shell 会有相应的注释。  

shell 脚本有条件语句（A 大于 B）、循环语句、读取文件和存储数据、读取变量且存储数据，当然，shell 脚本也包括函数。  

Shell 脚本和函数都是翻译型语言，所以他们并不会被编译。  

在后面的部分，我们会尝试写一些脚本。他们是一些写有命令的简单文本文件。

## 脚本例子: ##


假设我们创建一个名为 test.sh 的脚本。注意所有脚本的后缀名都必须为 **.sh**. 假设之前，用户已经往里面添加了一些命令，下面就是要启动这个脚本。例子如下：

    #!/bin/sh

这个命令告诉系统，后面的是 bourne shell.*它应念成 shebang，因为 # 被称为  hash，！称为 bang.*

为了创建包含这些指令的脚本，用户需要先键入 shebang 行，然后键入指令：

    #!/bin/bash
    pwd
    ls


## Shell 注释 ##


可以像下面一样来为脚本添加注释：

    #!/bin/bash
    
    # Author : Zara Ali
    # Copyright (c) Tutorialspoint.com
    # Script follows here:
    pwd
    ls

现在用户已经保存了上述内容，然后就可以执行了：

    $chmod +x test.sh

执行脚本方式如下：

    $./test.sh

这会输出如下结果：

    /home/amrood
    index.htm  unix-basic_utilities.htm  unix-directories.htm  
    test.shunix-communication.htmunix-environment.htm

**注意：**如果想要执行当前目录下的脚本，需要使用如下方式 **./program_name**

**扩展的 Shell 脚本：**

Shell脚本有几个构造告诉Shell环境做什么和什么时候去做。当然,大多数脚本比上面复杂得多。

毕竟，shell 是一种真正的编程语言,它可以有变量,控制结构等等。无论多么复杂的脚本,它仍然只是一个顺序执行的命令列表。

以下脚本使用 **read** 命令从键盘输入并分配给变量 PERSON
,最后打印 STDOUT。

    #!/bin/sh
    
    # Author : Zara Ali
    # Copyright (c) Tutorialspoint.com
    # Script follows here:
    
    echo "What is your name?"
    read PERSON
    echo "Hello, $PERSON"


下面是运行该脚本的例子：

    $./test.sh
    What is your name?
    Zara Ali
    Hello, Zara Ali
    $
