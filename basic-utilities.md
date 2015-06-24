##Unix 基本使用-打印，发送邮件##

到现在为止你肯定对 Unix 系统已经有了一些大概的理解和一些命令的基本使用方式。本教程将介绍一些非常基本的但重要的 Unix 实用工具。

###打印文件：###

在UNIX系统中，您打印一个文件之前，您可能想要重新格式化它调整它的边距，高亮显示一些单词等等。大多数文件也可以打印而不用重新格式化，但未经处理的打印可能不那么好看。

Unix 系统的许多版本中都包含了两个强大的文本格式化命令，nroff 和 troff。他们不包含在本教程中，但是你可以在在网上查到很多关于讲解这两个命令的使用方式的资料。

### pr 命令：###

**pr** 命令可以对终端显示屏上或者打印机上显示的文件进行小幅度的格式化。例如，如果在你的文件中有一长串名字，你可以将它格式化成两列或者多列在屏幕上显示。

如下是 **pr** 命令的语法示例：

```
pr option(s) filename(s)
```

**pr** 命令仅仅只是格式化显示在屏幕上或者打印的副本文件，它不会修改源文件。如下的列表显示一些 pr 命令中可选的参数：
<table class="src">
<tr>
<th style="width:25%">操作</th><th>描述</th>
</tr>
<tr><td><b>-k</b></td><td>产生 k 列的输出</td></tr>
<tr><td><b>-d</b></td><td> 将输出用两个空格隔开(并不是所有的 pr 版本适用)。</td></tr>
<tr><td><b>-h "header"</b></td><td>将下一个项目作为头部信息。</td></tr>
<tr><td><b>-t</b></td><td>去掉打印中的头部和上/下边距。</td></tr>
<tr><td><b>-l PAGE_LENGTH</b></td><td>设置一页存放的数据行数为 PAGE_LENGTH(66)。默认的文本行数为 56 行。</td></tr>
<tr><td><b>-o MARGIN</b></td><td>设置每行之间的间隔为 MARGIN(0) 个空格。</td></tr>
<tr><td><b>-w PAGE_WIDTH</b></td><td>设置页一行的字符个数为 PAGE_WIDTG(72) 个字符。这个参数仅仅对多文本列输出可用。</td></tr>
</table>

在使用 **pr** 命令之前，如下是查看 food 文件的内容：

```
$cat food
Sweet Tooth
Bangkok Wok
Mandalay
Afghani Cuisine
Isle of Java
Big Apple Deli
Sushi and Sashimi
Tio Pepe's Peppers
........
$
```

接着让我们利用 **pr** 命令将输出变成两列，同时头部显示 _Restaruants_:

	$pr -2 -h "Restaurants" food	
	Nov  7  9:58 1997  Restaurants   Page 1

	Sweet Tooth              Isle of Java
	Bangkok Wok              Big Apple Deli
	Mandalay                 Sushi and Sashimi
	Afghani Cuisine          Tio Pepe's Peppers
	........
	$

###lp 和 lpr 命令：###
命令 lp 或 lpr 将文件打印到纸上，而不是在屏幕上显示。一旦你准备使用 pr 命令格式化文本，您可以使用这些命令在任何与你电脑连接的打印机上打印你的文件。

您的系统管理员可能已经建立了一个站点作为默认打印机。为了在默认的打印机上打印一个文件命名 food 的文件，你可以使用 lp 或 lpr 命令，如下示例:

```
$lp food
request id is laserp-525  (1 file)
$
```

lp 命令显示了打印机的 ID，您可以使用它来取消打印作业或检查它的状态。

- 如果您正在使用 lp 命令，您可以使用 -nNum 选项参数设置打印副本的份数。对于 lpr 命令,您也可以使用参数 -Num 起到相同的作用。
- 如果有多个打印机连接到共享网络中，对于 lp 命令你可以使用 -dprinter 参数来选择你想使用的打印机，对于 lpr 命令你可以使用 -Pprinter 参数达到相同的效果。这里 printer 值得是打印机的名称。

###lpstat 和 lpg 命令：###

lpstat 命令显示在打印机队列中的作业:请求的 ID、所有者，文件大小，当打印任务被发送给打印机的时候，请求的状态同样也发送了给打印机。

如果你想看到所有输出请求而不仅仅是你自己的，你可以使用 lpstat -o 命令。请求会按照他们将会被打印的顺序显示出来:

```
$lpstat -o
laserp-573  john  128865  Nov 7  11:27  on laserp
laserp-574  grace  82744  Nov 7  11:28
laserp-575  john   23347  Nov 7  11:35
$
```

lpg 显示的信息与 lpstat -o 显示的稍微有些不同:

```
$lpq
laserp is ready and printing
Rank   Owner      Job  Files                  Total Size
active john       573  report.ps              128865 bytes
1st    grace      574  ch03.ps ch04.ps        82744 bytes
2nd    john       575  standard input         23347 bytes
$
```

在第一行显示打印机状态。如果打印机是禁用或纸用完了，你可以在第一行看到不同的信息。

###cancel 和 lprm 命令：###
**cancel** 命令终止 lp 命令发出的打印请求。**lprm** 命令终止 lpr 发出的打印请求。您可以指定打印机的 ID (由 lp 或 lpq 发出的请求)或名称来终止打印任务。

```
$cancel laserp-575
request "laserp-575" cancelled
$
```

为了取消当前正在打印的任务，可以忽视它的 ID，仅仅输入 cancel 命令和打印机的名称即可：

```
$cancel laserp
request "laserp-573" cancelled
$
```

lprm 命令将取消活动的工作，如果它属于你。否则，你可以使用工作的编号作为该命令的参数，或者使用破折号(-)删除你所有的工作:

```
$lprm 575
dfA575diamond dequeued
cfA575diamond dequeued
$
```

lprm 命令将会告诉你从打印机队列中删除的任务的文件名。

###发送邮件：###

您可以使用 Unix 邮件命令发送和接收邮件。如下是发送电子邮件的语法:

```
$mail [-s subject] [-c cc-addr] [-b bcc-addr] to-addr
```

如下是 mail 命令中重要的参数:

<table class="src">
<tr>
<th style="width:25%">参数</th><th>描述</th>
</tr>
<tr><td><b>-s</b></td><td>在命令行中指定邮件的主题。</td></tr>
<tr><td><b>-c</b></td><td>给列表中的用户发送副本。用户列表是由逗号分开的用户名列表。</td></tr>
<tr><td><b>-b</b></td><td>发送密文副本给列表中的用户。各个列表由逗号分隔开。</td></tr>
</table>


下面是示例发送测试消息到 admin@yahoo.com。

```
$mail -s "Test Message" admin@yahoo.com 
```

接下来该输入你的消息部分，消息输入部分是在行首的 “control-D" 的之后。如果想要结束，你仅仅只需要输入一个点类型(.)，如下：

```
Hi,
This is a test
.
Cc: 
```

你可以发送一个完整的文件通过利用重定向 < 操作符，如下：

```
$mail -s "Report 05/06/07" admin@yahoo.com < demo.txt 
```

为了检查是否有收到邮件，在 Unix 系统中你可以简单的输入如下的命令：

```
$mail
no email
```

