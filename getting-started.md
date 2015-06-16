# 什么是 Unix ? #

UNIX 操作系统是一系列的程序，将计算机和用户联系在一起。

分配系统资源和协调计算机内部的所有详细信息的计算机程序被称为操作系统或内核。

用户通过一个称为 shell 的程序内核进行通信。 shell 是一个命令行解释器; 它将用户输入的命令进行转换，并将它们转换为一种可以使内核理解的语言。

- Unix 最初是 1969 年由一批在贝尔实验室的人员开发出来的，包括 Ken Thompson, Dennis Ritchie, Douglas McIlroy, 和 Joe Ossanna。

- 在市场上有各种 Unix 变体。例如 Solaris Unix, AIX, HP Unix and BSD 是一些例子。 Linux 也是受欢迎的免费的 Unix。

- 许多人可以同时使用 UNIX 计算机;因此 UNIX 被称为多用户系统。

- 用户也可以在同一时间运行多个程序;因此 UNIX 被称为多任务处理。

# Unix 体系结构: #

这里是一个 UNIX 系统基本框图:

![](http://www.tutorialspoint.com/images/unix_architecture.jpg)

总结所有版本的 UNIX 的主要概念包含以下四个基本要素:

- **内核：**内核是操作系统的核心。它与硬件和大多数任务像内存管理任务调度和文件管理交互。

- **Shell：**shell 是用于处理您的请求的实用程序。当您在您的终端键入命令时，shell 将命令解释并调用你想要的程序。Shell 使用标准语法的所有命令。C Shell, Bourne Shell 和 Korn Shell 是最著名的 shell ，适用于大多数 Unix 变体。

- **命令和实用程序：**有各种各样的命令和实用程序可供您使用。**cp**, **mv**, **cat** 和 **grep** 等是命令和实用程序的几个例子。 有超过 250 标准命令，再加上通过第三方软件提供的其他命令。所有的命令都跟着各种可选的选项。

- **文件和目录：**在 UNIX 中的所有数据被都组织到文件中。所有文件被都组织到目录中。这些目录被组织成一个称为文件系统的树状结构。

# 系统启动: #

如果你有一台电脑安装了 UNIX 操作系统，然后你只需要打开其电源，使其运行。

只要你打开电源，系统开始启动，最后它会提示您登录到系统，登录到系统和使用它为您日复一日的活动。

# 登陆 Unix: #

当你第一次连接到 UNIX 系统时，你通常会看到如下提示:

    login:

# 登录: #

1. 准备好您的用户名 ( 用户标识 ) 及密码。如果你还没有这些，请联系您的系统管理员。

2. 在登录提示符下，键入您的用户名，然后按 ENTER 键。您的用户 id 是区分大小写，因此请确保您键入的 id 是系统管理员分配的。

3. 在密码提示符下，键入您的密码，然后按 ENTER 键。您的密码也是区分大小写的。

4. 如果您提供正确的用户 id 和密码，你将被允许进入系统。此时屏幕上回显的信息如下图所示。

<!-- lz -->

    login : amrood
    amrood's password:
    Last login: Sun Jun 14 09:32:32 2009 from 62.61.164.73
    $
    

系统会为您提供 (有时称为 $ 提示) 一个命令提示符，你可以在下面键入你所有的命令。例如若要检查日历您需要键入 **cal** 命令，如下所示:

    $ cal
     June 2009
    Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6
     7  8  9 10 11 12 13
    14 15 16 17 18 19 20
    21 22 23 24 25 26 27
    28 29 30
    
    $

# 修改密码 :#

所有 Unix 系统都需要密码以确保您的文件和数据的安全性，这个约束可以保证您的文件免受黑客破坏。这里是更改密码的步骤:

1. 开始时，在命令提示符处键入 **passwd** 如下所示。

2. 请输入您的旧密码即您目前使用的密码。

3. 输入你的新密码。总是保持您的密码足够复杂，没有人能猜出它。但前提是保证你记得住。

4. 您将需要再次键入该密码验证的密码。

<!-- lz -->

    $ passwd
    Changing password for amrood
    (current) Unix password:******
    New UNIX password:*******
    Retype new UNIX password:*******
    passwd: all authentication tokens updated  successfully
    
    $

**注意 :** 我用星 (*) 的位置是告诉您那是您输入当前密码和新密码的位置，当您键入字符时这些字符不会直接显示出来，而是以 * 号代替。

# 列出目录和文件: #

在 UNIX 中的所有数据被都组织到文件。所有文件被都组织成目录。这些目录被组织成一个称为文件系统的树状结构。

您可以使用 **ls** 命令列出所有的文件或目录在目录中。以下是使用 **ls** 命令与 **-l** 选项的示例。

    $ ls -l
    total 19621
    drwxrwxr-x  2 amrood amrood  4096 Dec 25 09:59 uml
    -rw-rw-r--  1 amrood amrood  5341 Dec 25 08:38 uml.jpg
    drwxr-xr-x  2 amrood amrood  4096 Feb 15  2006 univ
    drwxr-xr-x  2 root   root4096 Dec  9  2007 urlspedia
    -rw-r--r--  1 root   root  276480 Dec  9  2007 urlspedia.tar
    drwxr-xr-x  8 root   root4096 Nov 25  2007 usr
    -rwxr-xr-x  1 root   root3192 Nov 25  2007 webthumb.php
    -rw-rw-r--  1 amrood amrood 20480 Nov 25  2007 webthumb.tar
    -rw-rw-r--  1 amrood amrood  5654 Aug  9  2007 yourfile.mid
    -rw-rw-r--  1 amrood amrood166255 Aug  9  2007 yourfile.swf
    
    $

以 **d......** 开头的在这里表示目录。例如 uml, univ 和 urlspedia 是目录，其余的为文件。

# 你是谁 ？ #

当您登录到系统时，你可能愿意知道: **我是谁**?

最简单的方法来找出"你是谁"是输入 **whoami** 命令:

    $ whoami
     amrood
    
    $

在你的系统上试一试。此命令将列出与当前的登录名关联的帐户名称。你可以试试 **who am i** 命令以此来获取有关自己的信息。

# 已登录的是谁 ?#

有时你可能想知道谁同时登录到计算机。

这里有三个命令可以用来获取你此信息，基于你想要了解其他用户的程度: **users**，**who**，和 **w**。

    $ users
     amrood bablu qadir
    
    $ who
    amrood ttyp0 Oct 8 14:10 (limbo)
    bablu  ttyp2 Oct 4 09:08 (calliope)
    qadir  ttyp4 Oct 8 12:09 (dent)
    
    $

尝试在您的系统上的 **w** 命令来检查输出。这将列出一些更多的与记录在系统中的用户相关联的信息。

# 登出： #

当您完成您的会话时，您需要登出您的系统，确保没有其他人伪装成您访问您的文件。

# 登出方法：#

1. 只需在命令提示符下，键入 **logout** 命令然后系统将清理一切和断开连接

# 系统关机：#

最一致的方法来关闭 Unix 系统是正确通过命令行使用以下命令之一:

<table>
<tr>
<th align="left">命令</th>
<th align="left">描述</th>
</tr>
<tr>
<td><strong>halt</strong> </td>
<td>立即使系统关机。</td>
</tr>
<tr>
<td><strong> init 0 </strong></td>
<td>在关机之前使用预定义的脚本来同步和清理你的系统。</td>
</tr>
<tr>
<td><strong> init 6 </strong></td>
<td>在系统完全关闭后重新启动系统，然后将它完全备份</td>
</tr>
<tr>
<td><strong> poweroff </strong></td>
<td>通过断电自动关闭系统。</td>
</tr>
<tr>
<td><strong> reboot </strong></td>
<td>重新启动</td>
</tr>
<tr>
<td><strong> shutdown </strong></td>
<td>关机</td>
</tr>
</table>

你通常需要超级用户或根 (在 Unix 系统上最有特权的帐户) 来关闭系统，但在一些独立或个人拥有的 Unix 机器上，管理员用户甚至常规用户都可以这样做。