# 输入/输出重定向

大多数 UNIX 系统命令从你的终端接受输入并将所产生的输出发送回​​到您的终端。一个命令通常从一个叫标准输入的地方读取输入，默认情况下，这恰好是你的终端。同样，一个命令通常将其输出写入到标准输出，默认情况下，这也是你的终端。

## 输出重定向

一个命令的输出通常用于标准输出，也可以很容易地将输出转移到一个文件。这种能力被称为输出重定向：

如果记号 `> file` 添加到任何命令，这些命令通常将其输出写入到标准输出，该命令的输出将被写入文件，而不是你的终端：

检查下面的 **who** 命令，它将命令的完整的输出重定向在用户文件中。

```
    $ who > users
```

请注意，没有输出出现在终端中。这是因为输出已被从默认的标准输出设备（终端）重定向到指定的文件。如果你想检查 *users* 文件，它有完整的内容：

```
    $ cat users
    oko tty01   Sep 12 07:30
    ai  tty15   Sep 12 13:32
    ruthtty21   Sep 12 10:10
    pat tty24   Sep 12 13:07
    steve   tty25   Sep 12 13:03
    $
```

如果命令输出重定向到一个文件，该文件已经包含了一些数据，这些数据将会丢失。考虑这个例子：

```
    $ echo line 1 > users
    $ cat users
    line 1
    $
```

您可以使用 `>>` 运算符将输出添加在现有的文件如下：

```
    $ echo line 2 >> users
    $ cat users
    line 1
    line 2
    $
```

## 输入重定向

正如一个命令的输出可以被重定向到一个文件中，所以一个命令的输入可以从文件重定向。大于号 `>` 被用于输出重定向，小于号 `<`用于重定向一个命令的输入。

通常从标准输入获取输入的命令可以有自己的方式从文件进行输入重定向。例如，为了计算上面 *user* 生成的文件中的行数，你可以执行如下命令：

```
    $ wc -l users
    2 users
    $
```

在这里，它产生的输出为 2 行。你可以通过从 *user* 文件进行 wc 命令的标准输入重定向：

```
    $ wc -l < users
    2
    $
```

请注意，两种形式的 wc 命令产生的输出是有区别的。在第一种情况下，用行数列出该文件的用户的名称，而在第二种情况下，它不是。

在第一种情况下，wc 知道，它是从文件用户读取输入。在第二种情况下，只知道它是从标准输入读取输入，所以它不显示文件名。

## Here 文档

*here document*  被用来将输入重定向到一个交互式 Shell 脚本或程序。

在一个 Shell 脚本中，我们可以运行一个交互式程序，无需用户操作，通过提供互动程序或交互式 Shell 脚本所需的输入。

Here 文档的一般形式是：

```
    command << delimiter
    document
    delimiter
```

这里的 Shell 将 `<<` 操作符解释为读取输入的指令，直到它找到含有指定的分隔符线。然后所有包含行分隔符的输入行被送入命令的标准输入。

分隔符告诉 Shell here 文档已完成。没有它，Shell 不断的读取输入。分隔符必须是一个字符且不包含空格或制表符。

以下是输入命令 **wc -l**  来进行计算行的总数：

```
    $wc -l << EOF
    	This is a simple lookup program 
    	for good (and bad) restaurants
    	in Cape Town.
    EOF
    3
    $
```

可以用 *here document* 编译多行，脚本如下：

```
    #!/bin/sh
    
    cat << EOF
    This is a simple lookup program 
    for good (and bad) restaurants
    in Cape Town.
    EOF	
```

这将产生以下结果：

```
    This is a simple lookup program
    for good (and bad) restaurants
    in Cape Town.
```

下面的脚本用 vi 文本编辑器运行一个会话并且将输入保存文件在 test.txt 中。

```
    #!/bin/sh
    
    filename=test.txt
    vi $filename <<EndOfCommands
    i
    This file was created automatically from
    a shell script
    ^[
    ZZ
    EndOfCommands
```

如果用 vim 作为 vi 来运行这个脚本，那么很可能会看到以下的输出：

```
    $ sh test.sh
    Vim: Warning: Input is not from a terminal
    $
```

运行该脚本后，你应该看到以下内容添加到了文件 test.txt 中：

```
    $ cat test.txt
    This file was created automatically from
    a shell script
    $
```

## 丢弃输出

有时你需要执行命令，但不想在屏幕上显示输出。在这种情况下，你可以通过重定向到文件 `/dev/null` 以丢弃输出:

```
    $ command > /dev/null
```

在这里 command 是要执行的命令的名字。文件 `/dev/null` 是一个自动丢弃其所有的输入的特殊文件。

为了丢弃一个命令的输出和它的错误输出，你可以使用标准重定向来将 STDOUT 重定向到 STDERR ：

```
    $ command > /dev/null 2>&1
```

在这里，2 代表 STDERR ， 1 代表 STDOUT。可以上通过将 STDERR 重定向到 STDERR 来显示一条消息，如下：

```
    $ echo message 1>&2
```

## 重定向命令

以下是可以用来重定向的命令的完整列表：

<table>
	<tr><th>命令</th><th>描述</th></tr>
	<tr><td>pgm > file</td><td>pgm 的输出被重定向到文件</td></tr>
	<tr><td>pgm < file</td><td>pgm 程序从文件度它的输入</td></tr>
	<tr><td>pgm >> file</td><td>pgm 的输出被添加到文件</td></tr>
	<tr><td>n > file</td><td>带有描述符 n 的输出流重定向到文件</td></tr>
	<tr><td>n >> file</td><td>带有描述符 n 的输出流添加到文件</td></tr>
	<tr><td>n >& m</td><td>合并流 n 和 流 m 的输出</td></tr>
	<tr><td>n <& m</td><td>合并流 n 和 流 m 的输入</td></tr>
	<tr><td><< tag </td><td>标准输入从开始行的下一个标记开始。</td></tr>
	<tr><td>|</td><td>从一个程序或进程获取输入,并将其发送到另一个程序或进程。</td></tr>
</table>

需要注意的是文件描述符 0 通常是标准输入（STDIN），1 是标准输出（STDOUT），2 是标准错误输出（STDERR）。
