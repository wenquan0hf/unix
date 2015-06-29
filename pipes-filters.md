# 管道和过滤器

你可以连接两个命令在一起，这样一个程序的输出就可以作为下一个程序的输入。两个或两个以上的命令以这种方式连接形成一个管道。

为了形成管道，在同一行中利用一个竖线`(|)`将两个命令隔开。

如果一个程序将另一个程序的输出作为输入数据，接着对输入的数据执行一些操作，并将结果写入标准输出，它就称为一个过滤器。

## grep 命令

grep 程序用固定的模式搜索一个文件或多个文件。它的语法是:

```
$grep pattern file(s)
```

“grep” 这个名字来源于 ed(UNIX 行编辑器)命令，`g/re/p` 这意味着“利用正则表达式进行全局搜索并打印所有包含它的行。”

正则表达式是一些纯文本 (例如，一个词) 和 `/` 或特殊字符，它被用于模式匹配。

最简单的 grep 使用就是匹配由一个词组成的模式。它可可以管道中使用，因此只有那些输入行中包含一个给定的字符串，才会被发送到标准输出。如果你不指定 grep 读取的文件名，它读取标准输入，这也是所有过滤程序工作的方式:

```
$ls -l | grep "Aug"
-rw-rw-rw-   1 john  doc     11008 Aug  6 14:10 ch02
-rw-rw-rw-   1 john  doc      8515 Aug  6 15:30 ch07
-rw-rw-r--   1 john  doc      2488 Aug 15 10:51 intro
-rw-rw-r--   1 carol doc      1605 Aug 23 07:35 macros
$
```

如下是各种可选的参数，你可以在 grep 命令中进行使用：

<table>
<tr>
<th style="width25%">参数</th><th>描述</th>
</tr>
<tr><td><b>-v</b></td><td>打印所有没有匹配的行。</td></tr>
<tr><td><b>-n</b></td><td>打印所有成功匹配的行和行号。</td></tr>
<tr><td><b>-l</b></td><td>打印匹配的文件名和匹配的行("l"来自字母 letter)。</td></tr>
<tr><td><b>-c</b></td><td>仅仅打印成功匹配到行的个数。</td></tr>
<tr><td><b>-i</b></td><td>同时匹配大小写。</td></tr>
</table>

接下来，让我们使用一个正则表达式,它让 grep 命令找到包含 “carol” 字母的行，紧随其后的可以是零个或多个字母，正则表达式中表示方法是 “.*”)，之后接着是 “Aug” 字符。

如下是使用 -i 参数，表示对字母大小写不敏感：

```
$ls -l | grep -i "carol.*aug"
-rw-rw-r--   1 carol doc      1605 Aug 23 07:35 macros
$
```

## sort 命令

sort 命令是按字母顺序或者数字顺序对行文本进行排序。下面的示例是对 food 文件中的文本进行排序:

```
$sort food
Afghani Cuisine
Bangkok Wok
Big Apple Deli
Isle of Java
Mandalay
Sushi and Sashimi
Sweet Tooth
Tio Pepe's Peppers
$
```

**sort** 命令默认是按字母顺序进行排序。有很多可选参数，可以控制排序：

<table>
<th style="width:25%">参数</th><th>描述</th>
</tr>
<tr><td><b>-n</b></td><td>数值顺序进行排序 (例如: 10 将会被排到 2 之后)，忽略空格和 tab 符。</td></tr>
<tr><td><b>-r</b></td><td>将排序的顺序反转。</td></tr>
<tr><td><b>-f</b></td><td>将大小写排在一起。</td></tr>
<tr><td><b>+x</b></td><td>排序的时候忽略第一个 x 字段。</td></tr>
</table>

两个或者两个以上的命令就可以形成管道。拿前面提到的 **grep** 命令为例，我们可以按照文件的大小进一步对 August 文件进行排序。

如下管道包含了 **ls，grep，和 sort** 命令：

```
$ls -l | grep "Aug" | sort +4n
-rw-rw-r--  1 carol doc      1605 Aug 23 07:35 macros
-rw-rw-r--  1 john  doc      2488 Aug 15 10:51 intro
-rw-rw-rw-  1 john  doc      8515 Aug  6 15:30 ch07
-rw-rw-rw-  1 john  doc     11008 Aug  6 14:10 ch02
$
```

上面的管道将会按照文件的大小对 August 目录下的文件进行排序，并将它们打印到终端屏幕。排序参数 `+4n` 会跳过 4 个字段(由空格分隔的字段)，接着在按照数值顺序对行进行排序。

## pg 和 more 命令介绍

过长的输出通常会在您的屏幕上被压缩，但是如果你通过使用 more 或 pg 命令作为过滤器，知道屏幕显示满了文本之后才会停止。

假设你有一个很长的目录列表。为了让它容易阅读,我们就要对它进行排序，通过使用 **more** 命令对管道的输出进行处理:

```
$ls -l | grep "Aug" | sort +4n | more
-rw-rw-r--  1 carol doc      1605 Aug 23 07:35 macros
-rw-rw-r--  1 john  doc      2488 Aug 15 10:51 intro
-rw-rw-rw-  1 john  doc      8515 Aug  6 15:30 ch07
-rw-rw-r--  1 john  doc     14827 Aug  9 12:40 ch03
	.
	.
	.
-rw-rw-rw-  1 john  doc     16867 Aug  6 15:56 ch05
--More--(74%)
```

屏幕将会充满文本数据，这些文本是按照文件大小顺序的。在屏幕的底端是一个 **more** 命令，你可以敲入命令让屏幕滚动显示更多的数据。

当屏幕上显示完成的时候，你接着可以使用在讨论部分说的任何关于 more 程序的命令。
