# 环境

UNIX 中一个重要的概念是环境，它是由环境变量所定义。一些环境变量是由系统设置，有一些是由用户设置的，还有一些是被 Shell，或任何会加载另一个程序的程序所设置。

一个变量是由一个字符组成的串，并且我们会给它赋值。给变量赋的值可以是一个数字，文本，文件名，设备或任何其他类型的数据。

例如，首先，我们设置一个名称为 TEST 的变量，然后我们使用 echo 命令查看它的值:

```
$TEST="Unix Programming"
$echo $TEST
Unix Programming
```

注意，设置环境变量不使用 `$` 符号，但在访问他们的时候，我们使用 `$` 符号作为前缀。这些变量保存它们的值，直到我们退出 shell。

当你登录到系统，shell 经过初始化阶段，在该阶段会设置各种环境变量。这通常会涉及到两步的处理过程，shell 会读取以下文件:

- `/etc/profile`
- profile

处理流程如下:

1. shell 程序检查 **/etc/profile** 文件是否存在。
2. 如果该文件存在，shell 程序会读取该文件。否则，就会跳过该文件。同时也不会显示任何错误信息。
3. shell 程序检查 **.profile** 文件是否在你的根目录下面存在。您的根目录就是你在登录之后进入的目录。
4. 如果该文件存在，shell 程序就会读取它。否则，shell 程序跳过它，不会显示任何错误信息。

一旦这两个文件读取完成，shell 显示一个等待输入命令:

```
	$
```

这是提示,在它后面你可以输入命令来执行。

**注意：**Shell 初始化的详细过程通常利用的是 **Bourne** Shell，但是其他的一些文件处理是利用 **bash** 和 **ksh** shell 程序。

## .profile 文件

**/etc/profile** 文件是由 UNIX 的系统管理员维护的，并且该文件中包含了 Shell 初始化的信息，这个信息可以被任何系统中的任何用户查看。

如果你有对 **.profile** 文件操作的权限，那么你就可以在这个文件中添加你想要的尽可能多的定制 Shell 信息。

- 你使用的终止符的类型
- 命令存在的一系列文件的列表
- 一些列的变量设置你的终端显示的效果

你可以在你的根目录下面查看 **.profile** 文件。利用 **vi** 编辑器打开它，查看其中设置的所有环境变量。

## 设置终结符的类型

通常您所使用的终端的类型由 **login** 或 **getty** 程序自动配置。有时，自动配置过程会推测你的终端类型是不对的。

如果您的终端设置错误，命令的输出可能看起来很奇怪，或者你可能无法与 Shell 正常交互。

确保这不是这种情况，大多数用户的终端最少相同的特性如下:

```
$TERM=vt 100
$
```

## 设置 PATH 变量

当你在命令提示符下输入任何命令，Shell 只有确定了命令所在的目录才能执行命令。

Shell 是在环境变量 PATH 中寻找命令所在的目录。通常，它设置如下:

```
$PATH=/bin:/usr/bin
$
```

这里的每一个由冒号，：，分开的实体是目录。如果你请求 Shell 执行一个命令，但是它不能在 PATH 环境变量中找到任何命令所在的路径,这时会出现一个类似如下的消息:

```
$hello
hello: not found
$
```

还有类似于 PS1 和 PS2 这样的变量，将会在下一节说明。

## PS1 和 PS2 变量

shell 显示给你的命令提示符存储在变量 PS1 中。你可以改变这个变量成任何你想要的字符。只要你改变它，它就会从你改变后开始起作用。

例如，如果你输入如下的命令:

```
$PS1='=>'
=>
=>
=>
```

你的提示输入符将会变成 =>。设置 PS1 的值，让它显示工作目录，输入如下的命令:

```
=>PS1="[\u@\h \w]\$"
[root@ip-72-167-112-17 /var/www/tutorialspoint/unix]$
[root@ip-72-167-112-17 /var/www/tutorialspoint/unix]$
```

该命令的结果是,显示用户的用户名、机器名称(主机名)，和工作目录。

有相当多的转义序列，可以用作 PS1 的参数，尽量让自己只关注最关键的部分,不要让下面的信息对你造成过多的压力。

<table>
<tr>
<th style="width:25%">转义序列</th><th>描述</th>
</tr>
<tr><td><b>\t</b></td><td>将当前的时间表示成 HH:MM:SS 的形式</td></tr>
<tr><td><b>\d</b></td><td>将当前的日期表示成 周 月 日</td></tr>
<tr><td><b>\n</b></td><td>新的一行。</td></tr>
<tr><td><b>\s</b></td><td>当前的环境变量。</td></tr>
<tr><td><b>\W</b></td><td>工作目录。</td></tr>
<tr><td><b>\w</b></td><td>工作目录的完整路径。</td></tr>
<tr><td><b>\u</b></td><td>当前用户的用户名。</td></tr>
<tr><td><b>\h</b></td><td>当前机器的主机名称。</td></tr>
<tr><td><b>\#</b></td><td>当前命令的编号。每输入一条命令编号加 1。</td></tr>
<tr><td><b>\$</b></td><td>如果有效的 UID 是 0(也就是说，如果你以 root 用户进行登录)，命令提示符会变成 #，否则，提示符是 $。</td></tr>
</table>

你可以通过修改 `.profile` 文件，在每次登录的时候进行上面的那些转换。这样每次登录就会自动的改变 PS1 的值。

当你输入一个不完整的命令是，shell 将再次显示一个命令输入符，等待你再次完成命令并回车。

默认二级提示 >(大于号)，但可以改变通过设置 PS2 变量进行修改：

下面的示例使用默认的二级提示:

```
	$ echo "this is a
	> test"
	this is a
	test
	$
```

下面是一个通过重新定义 PS2 变量自定义输入符的示例:

```
$ PS2="secondary prompt->"
$ echo "this is a
secondary prompt->test"
this is a
test
$
```

## 环境变量

以下是部分重要的环境变量的列表。这些变量将按照上面提到的方式被设置和访问:

<table>
<tr>
<th style="width:25%">变量</th><th>描述</th>
</tr>
<tr><td><b>DISPLAY </b></td><td>包含显示设备的标识符，默认情况下它的值是 X11。</td></tr>
<tr><td><b>HOME</b></td><td>表明当前用户的根目录，默认的参数中会内置 cd 命令。</td></tr>
<tr><td><b>IFS</b></td><td>表明系统内部所使用字段分隔符，它通常用在解析器分割单词中。</td></tr>
<tr><td><b>LANG</b></td><td>LANG 扩展系统默认的语言：LC_ALL 可以用来覆盖这个变量。例如，如果它的值是 pt_BR，那么系统的语言就被设置成(Brazillian)Portuguese 和地区被设置成 Brazil。</td></tr>
<tr><td><b>LD_LIBRARY_PATH</b></td><td>许多 UNIX 系统动态链接器，包含以冒号分隔的目录列表，在执行后，动态连接器构建过程图像过程中，在搜索其他目录之前，先搜索共享对象。</td></tr>
<tr><td><b>PATH</b></td><td>命令的搜索路径。它是由冒号分隔开一系列目录，也就是 shell 寻找命令所在的目录。</td></tr>
<tr><td><b>PWD</b></td><td>当前的工作目录，由 cd 命令设置的。</td></tr>
<tr><td><b>RANDOM</b></td><td>每次被引用的时候就会生成一个 0 到 32,767 范围内的一个随机整数。</td></tr>
<tr><td><b>SHLVL</b></td><td>每次一个 bash 实例被启动这个值就会加 1。这个变量对于决定内置的退出命令是否终止当前会话是很有用的。</td></tr>
<tr><td><b>TERM </b></td><td>显示类型。</td></tr>
<tr><td><b>TZ </b></td><td>时间区域。它能被赋值为 GMT，AST 等。</td></tr>
<tr><td><b>UID</b></td><td>数值类型标识当前用户，它在 shell 启动的时候被初始化。</td></tr>
</table>

如下是几个简单的例子显示几个环境变量：

```
$ echo $HOME
/root
]$ echo $DISPLAY
$ echo $TERM
xterm
$ echo $PATH
/usr/local/bin:/bin:/usr/bin:/home/amrood/bin:/usr/local/bin
$
```
