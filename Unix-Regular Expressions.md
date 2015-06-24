## Unix-正则表达式和 SED

正则表达式是一个字符串,可以用来描述几个字符序列。Unix的这些命令中会用到正则表达式,包括 ed、sed、awk、grep,以及 vi。


本教程将教你如何使用正则表达式和 sed。


这里 sed 代表的流编辑器是一个面向流的编辑器，是专门为执行脚本创建的。因此你的所有输入都会被送到 STDOUT 并且它不改变输入文件。

###调用sed：

在我们开始之前,让我们以确保你有/etc/passwd文本文件的本地副本。


如前所述,可以通过一个 pipe 发送数据而调用s ed，如下所示:

    $ cat /etc/passwd | sed
    Usage: sed [OPTION]... {script-other-script} [input-file]...
    
      -n, --quiet, --silent
     suppress automatic printing of pattern space
      -e script, --expression=script
    ...............................

cat 命令转储/etc/passwd 的内容到 sed 是通过 pipe 进入 sed 的模式空间。sed 使用模式空间的内部工作缓冲区来做它的工作。
###sed 的一般语法：

下面是sed的一般语法

    /pattern/action

在这里,pattern 是一个正则表达式,action 则是在下表中给出的命令。当省 pattern  时,如上面我们已经看到的，action 会执行每一行命令。


围绕 pattern 的斜杠字符(/)是不可省略的,因为它们是作为分隔符使用。

<table>
   <tr>
  <td><strong>范围<td><strong>描述</td>
</tr>
<tr>
<td>p<td>输出该行
<tr>
<td>d<td>删除该行</td>
<tr>
<td>s/模式1/模式2/<td>替代第一次出现的模式1和模式2</td>
<tr>

</table>
###用sed 删除所有行:

再次调用 sed ,但这一次使用 sed 的编辑命令删除一行记录，使用字母 d 表示其:

    $ cat /etc/passwd | sed 'd'
    $

除了通过pipe发送一个文件来调用 sed,你可以指导 sed 从文件中读取数据,示例如下。


下面的命令与前面是完全一样的,尝试一下，里面不包括 cat 命令:

    $ sed -e 'd' /etc/passwd
    $

###sed地址:

sed 也可以理解为所谓的地址。地址可以是文件中的一个位置，也可以是一个特殊的编辑命令适用的范围。当 sed 遇到没有地址的情况时,它会对文件中的每一行执行其操作。


下面的命令将一个基本的地址添加到您使用的 sed 命令中:

    $ cat /etc/passwd | sed '1d' |more
    daemon:x:1:1:daemon:/usr/sbin:/bin/sh
    bin:x:2:2:bin:/bin:/bin/sh
    sys:x:3:3:sys:/dev:/bin/sh
    sync:x:4:65534:sync:/bin:/bin/sync
    games:x:5:60:games:/usr/games:/bin/sh
    man:x:6:12:man:/var/cache/man:/bin/sh
    mail:x:8:8:mail:/var/mail:/bin/sh
    news:x:9:9:news:/var/spool/news:/bin/sh
    backup:x:34:34:backup:/var/backups:/bin/sh
    $

注意,数字1添加在删除命令前面。这告诉 sed 在文件的第一行执行编辑命令。在这个例子中,sed将删除/etc/password文件的第一行并打印文件的其他部分。

###sed地址范围:

所以如果你想从文件中删除一行，您可以指定一个地址范围如下:

    $ cat /etc/passwd | sed '1, 5d' |more
    games:x:5:60:games:/usr/games:/bin/sh
    man:x:6:12:man:/var/cache/man:/bin/sh
    mail:x:8:8:mail:/var/mail:/bin/sh
    news:x:9:9:news:/var/spool/news:/bin/sh
    backup:x:34:34:backup:/var/backups:/bin/sh
    $

以上命令应用的范围是1到5行。所以将删除这五行。


尝试以下地址范围:

<table>
   <tr>
  <td><strong>范围<td><strong>描述</td>
</tr>
<tr>
<td>'4,10d'<td>删除第4到10行
<tr>
<td>'10,4d'<td>只删除第10行，因为 sed 不能反方向工作</td>
<tr>
<td>'4,+5d'<td>这将匹配文件中的第4行,删除这一行之后,继续删除下一个五行,然后停止其删除操作并输出其他行
</td>
<tr>
<td>'2,5!d'<td>这将删除除2到5行外的所有其他行。
</td>
<tr>
<td>'1~3d'<td>删除第一行后,跳过接下来的三行,然后删除第四行。sed 继续这种模式直到文件的末尾。
</td>
<tr>
<td>'2~2d'<td>sed 删除第二行,跳过下一行后,删除下面的一行,并重复,直到到达文件的末尾。
</td>
<tr>
<td>'4,10p'<td>输出4到10行之间的内容。</td>
<tr>
<td>'4,d'<td>产生语法错误。</td>
<tr>
<td>',10d'<td>也产生语法错误。</td>
<tr>
</table>


注意:在使用p action的时候,您应该使用- n 选项来避免重复输出。检查以下两个命令的betweek 差异:

    $ cat /etc/passwd | sed -n '1,3p'


上面的命令不加 - n 的情形如下:

    $ cat /etc/passwd | sed '1,3p'

###替换命令:


替换命令,用s表示,将取代你指定的任何其他字符串。


用一个字符串替代另一个,你需要告诉 sed 你第一个字符串的结束位置和想要替换的字符串的开始位置。传统上是由正斜杠(/)将两个字符串分开的。


以下命令将替换第一次出现的root和amrood字符串。


    $ cat /etc/passwd | sed 's/root/amrood/'
    amrood:x:0:0:root user:/root:/bin/sh
    daemon:x:1:1:daemon:/usr/sbin:/bin/sh
    ..........................


非常重要的一点是, sed 替代只在一个命令行的某一字符串第一次出现时才能使用。如果字符串root在一行里面出现不止一次，只有第一个root字符串被替换。


sed去做一个全局替换，需要添加字母g到命令末尾，命令如下:

    $ cat /etc/passwd | sed 's/root/amrood/g'
    amrood:x:0:0:amrood user:/amrood:/bin/sh
    daemon:x:1:1:daemon:/usr/sbin:/bin/sh
    bin:x:2:2:bin:/bin:/bin/sh
    sys:x:3:3:sys:/dev:/bin/sh
    ...........................

###替换标志：

除了g标志外，还有许多其他有用的标志可以使用,而且您每次可以指定多余一个标志。

<table>
   <tr>
  <td><strong>标志<td><strong>描述</td>
</tr>
<tr>
<td>g<td>替换所有可以匹配的字符而不仅仅是第一个
<tr>
<td>NUMBER<td>仅仅替换第NUMBLER个匹配的字符
<tr>
<td>p<td>如果发生了替换，则输出模式空间</td>
<tr>
<td> w FILENAME<td>如果发生了替换，则将结果写到FILENAME
<tr>
<td>I or i<td>以不区分大小写的方式匹配</td>
<tr>
<td>M or m<td>除了拥有特殊正则表达式字符^和$的正常的行为外,这个标志使^匹配换行符后的空字符串,使$匹配换行符前的空字符串。
</td>
<tr>
</table>

###使用一个可替换的字符串分隔符:

你会发现自己不得不对包含斜杠字符的字符串做一个替换。在这种情况下,您可以对 s 后的字符来指定一个不同的分隔符。

    $ cat /etc/passwd | sed 's:/root:/amrood:g'
    amrood:x:0:0:amrood user:/amrood:/bin/sh
    daemon:x:1:1:daemon:/usr/sbin:/bin/sh

在上面的例子中: / 作为定界符使用,而不是斜线/。因为我们试图搜索 /root,而不是简单的 roo t字符串。
###使用空串的执行替换：

使用一个空的替换字符串去删除/etc/passwd文件的root字符串。

    $ cat /etc/passwd | sed 's/root//g'
    :x:0:0::/:/bin/sh
    daemon:x:1:1:daemon:/usr/sbin:/bin/sh

###地址替换：

如果你想只在第10行用字符串sh替换字符串quiet,你可以指定如下:

    $ cat /etc/passwd | sed '10s/sh/quiet/g'
    root:x:0:0:root user:/root:/bin/sh
    daemon:x:1:1:daemon:/usr/sbin:/bin/sh
    bin:x:2:2:bin:/bin:/bin/sh
    sys:x:3:3:sys:/dev:/bin/sh
    sync:x:4:65534:sync:/bin:/bin/sync
    games:x:5:60:games:/usr/games:/bin/sh
    man:x:6:12:man:/var/cache/man:/bin/sh
    mail:x:8:8:mail:/var/mail:/bin/sh
    news:x:9:9:news:/var/spool/news:/bin/sh
    backup:x:34:34:backup:/var/backups:/bin/quiet

同样的,做一个地址范围替换,你可以做如下操作:

    $ cat /etc/passwd | sed '1,5s/sh/quiet/g'
    root:x:0:0:root user:/root:/bin/quiet
    daemon:x:1:1:daemon:/usr/sbin:/bin/quiet
    bin:x:2:2:bin:/bin:/bin/quiet
    sys:x:3:3:sys:/dev:/bin/quiet
    sync:x:4:65534:sync:/bin:/bin/sync
    games:x:5:60:games:/usr/games:/bin/sh
    man:x:6:12:man:/var/cache/man:/bin/sh
    mail:x:8:8:mail:/var/mail:/bin/sh
    news:x:9:9:news:/var/spool/news:/bin/sh
    backup:x:34:34:backup:/var/backups:/bin/sh

正如你从输出所看到的，前五行里面的字符串 sh 都改为了 quiet ,但是其他行里面的 sh都丝毫没有改变。
###匹配命令:

你可以使用 p 参数和 - n 参数输出所有匹配的行，如下所示:

    $ cat testing | sed -n '/root/p'
    root:x:0:0:root user:/root:/bin/sh
    [root@ip-72-167-112-17 amrood]# vi testing
    root:x:0:0:root user:/root:/bin/sh
    daemon:x:1:1:daemon:/usr/sbin:/bin/sh
    bin:x:2:2:bin:/bin:/bin/sh
    sys:x:3:3:sys:/dev:/bin/sh
    sync:x:4:65534:sync:/bin:/bin/sync
    games:x:5:60:games:/usr/games:/bin/sh
    man:x:6:12:man:/var/cache/man:/bin/sh
    mail:x:8:8:mail:/var/mail:/bin/sh
    news:x:9:9:news:/var/spool/news:/bin/sh
    backup:x:34:34:backup:/var/backups:/bin/sh


###使用正则表达式：
在进行模式匹配时,您可以使用正则表达式，它提供了更多的灵活性。
检查下面的例子中以daemon开始的行然后删除:

    $ cat testing | sed '/^daemon/d'
    root:x:0:0:root user:/root:/bin/sh
    bin:x:2:2:bin:/bin:/bin/sh
    sys:x:3:3:sys:/dev:/bin/sh
    sync:x:4:65534:sync:/bin:/bin/sync
    games:x:5:60:games:/usr/games:/bin/sh
    man:x:6:12:man:/var/cache/man:/bin/sh
    mail:x:8:8:mail:/var/mail:/bin/sh
    news:x:9:9:news:/var/spool/news:/bin/sh
    backup:x:34:34:backup:/var/backups:/bin/sh

下面是将删除以 sh 结尾的所有行的例子：

    $ cat testing | sed '/sh$/d'
    sync:x:4:65534:sync:/bin:/bin/sync

下表列出了四个在正则表达式里面非常有用的特殊字符。

<table>
   <tr>
  <td><strong>字符<td><strong>描述</td>
</tr>
<tr>
<td>^<td>匹配一行的起始</td>
<tr>
<td>$<td>匹配一行的结尾</td>
<tr>
<td>.<td>匹配任何的单个字符</td>
<tr>
<td>*<td>匹配零个或多个以前出现的字符</td>
<tr>
<td>[chars]<td>为了匹配任何字符串的字符。您可以使用-字符来表示字符的范围。
</td>
<tr> 
</table>

###匹配字符:


来看看在其他的表达式里面如何演示元字符的使用。例如下面的模式:


<table>
   <tr>
  <td><strong>表达式<td><strong>描述</td>
</tr>
<tr>
<td>/a.c/<td>匹配包含字符串如a+c，a-c，abc, match, 还有 a3c</td>
<tr>
<td>/a*c/<td>匹配相同的字符串还有字符串比如ace，yacc，以及arctic</td>
<tr>
<td>/[tT]he/<td>匹配字符The和the</td>
<tr>
<td>/^$/<td>匹配空白行</td>
<tr>
<td>/^.*$/<td>不管任何情况，都匹配一整行</td>
<tr> 
<td>/ */<td>匹配一个或多个空格</td>
<tr>
<td>/^$/<td>匹配空行</td>
<tr> 
</table>


下表给出了一些常用的字符:

<table>
   <tr>
  <td><strong>集<td><strong>描述</td>
</tr>
<tr>
<td>[a-z]<td>匹配一个小写字母</td>
<tr>
<td>[A-Z]<td>匹配一个大写字母</td>
<tr>
<td>[a-zA-Z]<td>匹配一个字母</td>
<tr>
<td>[0-9]<td>匹配数字</td>
<tr>
<td>[a-zA-Z0-9]<td>匹配单个字母或数字</td>
<tr> 
</table>




###字符类关键词:


通常来说，一些特殊的关键字对regexp来说也是适用的,尤其是GNU实用程序会使用regexp。对 sed正则表达式来说这些都是非常有用的，因为这样既简化了表达式又增强了可读性。


例如,字符a到z以及字符A到Z构成了这样一个用关键字[[:alpha:]]表示的类。

使用字母表的字符类关键词,这个命令输出/etc/syslog.conf文件里面以字母表的字母开始的行:


    $ cat /etc/syslog.conf | sed -n '/^[[:alpha:]]/p'
    authpriv.* /var/log/secure
    mail.* -/var/log/maillog
    cron.* /var/log/cron
    uucp,news.crit /var/log/spooler
    local7.*   /var/log/boot.log


下表是 GNU sed 的可用的字符类关键词的一个完整的列表。

<table>
   <tr>
  <td><strong>字符类<td><strong>描述</td>
</tr>
<tr>
<td>[[:alnum:]]<td>字母(a - z A-Z 0 - 9)</td>
<tr>
<td>[[:alpha:]]<td>字母(a - z A-Z)</td>
<tr>
<td>[[:blank:]]<td>空白字符(空格或制表键)</td>
<tr>
<td>[[:cntrl:]]<td>控制字符</td>
<tr>
<td>[[:digit:]]<td>数字[0 - 9]</td>
<tr> 
<td>[[:graph:]]<td>任何可见字符(不包括空格)</td>
<tr>
<td>[[:lower:]]<td>小写字母的[a -ž]</td>
<tr> 
<td>[[:print:]]<td>可打印字符(无控字符)</td>
<tr> 
<td>[[:punct:]]<td>标点字符</td>
<tr>
<td>[[:space:]]<td>空白</td>
<tr> 
<td>[[:upper:]]<td>大写字母的[A -Z]</td>
<tr>
<td>[[:xdigit:]]<td>十六进制数字[0 - 9 a - f A-F]</td>
<tr> 
</table>



###&引用:


sed 元字符 & 代表被匹配的 pattern 的内容。例如,假设您有一个名为phone.txt.的文件，里面都电话号码,如下所示:

    5555551212
    
    5555551213
    
    5555551214
    
    6665551215
    
    6665551216
    
    7775551217


你想让前三个数字被括号括起来以更容易阅读。要做到这一点,您可以使用 & 替换字符,如下所示:

    $ sed - e ' s / ^[[数位:]][[数位:]][[数位:]](&)/ g phone.txt
    
    
    (555)5551212
    
    (555)5551213
    
    (555)5551214
    
    (666)5551215
    
    (666)5551216
    
    (777)5551217


先匹配3位数字,然后使用&取代那些括号括起来的数字。


###使用多个sed命令:


您可以在一个 sed 命令下使用多个 sed 命令，如下:


    $ sed -e 'command1' -e 'command2' ... -e 'commandN' files

这里commandN 到 command1 都是我们之前讨论的 sed 类型命令。这些命令应用于每个文件列表的行。


以相同的机制,我们可以以下面的方式写上面的电话号码:

    $ sed - e ' s / ^[[数位:]]\ \ { 3 } /(&)/ g \
    
                             - e ' s /)[[数位:]]\ \ { 3 } / & - / g phone.txt
    
    (555)555 - 1212
    
    (555)555 - 1213
    
    (555)555 - 1214
    
    (666)555 - 1215
    
    (666)555 - 1216
    
    (777)555 - 1217


注意:在上面的例子中,不是重复字符类关键字[[:digit:]] 三次,而是代之以\{3\},这意味着前三次正则表达式相匹配。


###引用:


&元字符是有用的,但更有用的功能是能够在正则表达式中定义特定区域,通过定义正则表达式的特定的一部分,您可以引用字符引用这部分。


反向引用时,你必须首先定义一个区域,然后回顾这个区域。定义一个区域是在你感兴趣的区域插入\和括号。你周围的第一区域被通过\ 1引用,第二个地区用 \ 2引用,等等。


假设 phone.txt 有以下文本:

    (555)555 - 1212
    
    (555)555 - 1213
    
    (555)555 - 1214
    
    (666)555 - 1215
    
    (666)555 - 1216
    
    (777)555 - 1217


现在试试下面的命令:

    $ cat phone.txt | sed 's/\(.*)\)\(.*-\)\(.*$\)/Area \
       code: \1 Second: \2 Third: \3/'
    Area code: (555) Second: 555- Third: 1212
    Area code: (555) Second: 555- Third: 1213
    Area code: (555) Second: 555- Third: 1214
    Area code: (666) Second: 555- Third: 1215
    Area code: (666) Second: 555- Third: 1216
    Area code: (777) Second: 555- Third: 1217
    

注意:在上面的例子中每个括号内的正则表达式将引用\ 1,\ 2等等。

