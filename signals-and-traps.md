# UNIX 信号和 Traps #

信号是发送给程序的软件中断，表明已发生的重要事件。这些事件的范围可以是从用户请求到非法内存访问错误。这些信号，如中断信号，表明用户要求程序做一些非一般流程控制下的事情。

以下是一些你可能会遇到的并且需要在程序中使用的常见信号：

<table>
<tr>
<th align="left">信号名</th>
<th align="left">信号值</th>
<th align="left">描述</th>
</tr>
   <tr>
      <td>SIGHUP</td>
      <td>1</td>
      <td>控制终端意外终止或者是控制进程结束时发出</td>
   </tr>
   <tr>
      <td>SIGINT</td>
      <td>2</td>
      <td>用户发送一个中断信号时发出（Ctrl+C）。</td>
   </tr>
   <tr>
      <td>SIGQUIT</td>
      <td>3</td>
      <td>用户发送一个退出信号时发出（Ctrl+D）。</td>
   </tr>
   <tr>
      <td>SIGFPE</td>
      <td>8</td>
      <td>当非法的数学操作执行时发出。</td>
   </tr>
   <tr>
      <td>SIGKILL</td>
      <td>9</td>
      <td>一个进程获取到此信号，它必须立即退出，并且不能进行任何清除操作。</td>
   </tr>
   <tr>
      <td>SIGALRM</td>
      <td>14</td>
      <td>时钟信号（用于定时器）</td>
   </tr>
   <tr>
      <td>SIGTERM</td>
      <td>15</td>
      <td>软件终止信号（kill 命令缺省产生此信号）。</td>
   </tr>
</table>

## 信号列表： ##

有一个简单的方法可以列出你的系统所支持的所有信号。仅仅用命令 **kill -l** 就可以显示系统所有支持的信号：


	$ kill -l
	 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL
	 5) SIGTRAP      6) SIGABRT      7) SIGBUS       8) SIGFPE
	 9) SIGKILL     10) SIGUSR1     11) SIGSEGV     12) SIGUSR2
	13) SIGPIPE     14) SIGALRM     15) SIGTERM     16) SIGSTKFLT
	17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
	21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU
	25) SIGXFSZ     26) SIGVTALRM   27) SIGPROF     28) SIGWINCH
	29) SIGIO       30) SIGPWR      31) SIGSYS      34) SIGRTMIN
	35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3  38) SIGRTMIN+4
	39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
	43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12
	47) SIGRTMIN+13 48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14
	51) SIGRTMAX-13 52) SIGRTMAX-12 53) SIGRTMAX-11 54) SIGRTMAX-10
	55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7  58) SIGRTMAX-6
	59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
	63) SIGRTMAX-1  64) SIGRTMAX


 Solaris, HP-UX 和 Linux 之间实际的信号列表会有所不同。 

## 默认动作： ##

每一个信号都有一个与之相随的默认动作。一个信号的默认动作是当脚本或程序接收到一个信号时，它的执行表现。

这些可能的默认动作是：

- 终止进程。

- 忽略信号。

- 内核映像转储。当收到信号时，此动作将创建一个称为 core 的文件，其包含进程的内存映像。

- 停止进程。

- 继续停止的进程。

## 发送信号： ##

有几种向程序或者脚本传递信号的方法。其中用户最常见的是在正在运行的脚本的时候，按下 Ctrl+C 或者 INTERRUPT 键。

当你按下 Ctrl+C 键，信号 SIGINT 被发送到脚本中，根据之前定义的默认动作，脚本将会被终止。

另外一种常见的传送信号的方法是使用 kill 命令，其语法如下所示：

    $ kill -signal pid

这里的 **signal** 要么是信号值，要么是信号名称。 **pid** 是信号要发送到的进程的 ID。 
例如：

    $ kill -1 1001

发送 HUP 信号（即意外终止信号）到运行进程 ID 为 1001 的程序。 用下面的命令来发送一个 kill 信号到同样的进程：

    $ kill -9 1001

这条命令会杀死运行进程 ID 为 1001 的程序。

## 捕获信号： ##

当一个 shell 程序正在执行的过程中，你在终端按下了 Ctrl+C 或 Break 键，通常情况下，程序会立即终止，并且你的命令提示返回。但这可能并不总是你所期望的。例如，这可能会留下一堆未清理的临时文件。

捕获这些信号是很容易的，捕获命令（trap）的语法如下：

    $ trap commands signals


这里的 commands 可以是任何有效的 UNIX 命令，甚至可以是一个用户定义的函数。
signals 可以是一个你想捕获的任何数量信号的列表。

在 shell 脚本中，trap 有三种常见的用途：


1. 清除临时文件
2. 忽略信号

## 清除临时文件 ##
作为 trap 命令的一个例子，下面的命令展示了，如果有人试图从终端中止程序时，你如何先删除一些文件，然后退出：

    $ trap "rm -f $WORKDIR/work1$$ $WORKDIR/dataout$$; exit" 2

如果程序收到了信号值为 2 的信号，trap 命令将会被执行。从 shell 程序上执行 trap 的这一点开始，work1$$ 和 dataout$$ 这两个文件会自动被删除。

所以如果用户中断程序的运行，这个 trap 将会被执行，你可以确保这两个文件将被清理掉。**rm** 后面的这个 **exit** 命令，它的存在是必要的。如果没有它，程序会在它中断点（也就是信号接收的时刻）继续执行。

信号值 1 是由挂断产生的：要么是有人故意挂断终端或者是终端被意外断开。

在这种情况下，把信号值 1 增加到信号列表中，你可以通过这样修改上面的 trap 命令，从而删除那两个指定的文件：

    $ trap "rm $WORKDIR/work1$$ $WORKDIR/dataout$$; exit" 1 2


现在，如果终端被挂起或者是 Ctrl+C 被按下，这些文件将被删除。

指定的 trap 命令如果包含多个命令，那么它们必须括在引号中。还要注意，当 trap 命令执行时，shell  会扫描一遍命令行，当接收到信号列表的其中一个信号时，也会再执行一次扫描。

所以在上面的例子中，当 trap 命令执行后，WORKDIR 和 $$ 的值将会被替换。如果你想要这种替换仅仅发生在信号值 1 或者 2 接收到的时候，你可以用单引号把多个命令引起来：
    
    $ trap 'rm $WORKDIR/work1$$ $WORKDIR/dataout$$; exit' 1 2

## 忽略信号： ##

如果 trap 命令的 command 字段是空的，那么当接收到指定的信号后，信号将被忽略。例如下面的一个命令：

    $ trap '' 2


指定的中断信号将被忽略。当执行某些可能不想被打断的操作时，你可能会想忽略掉些特定的信号。按如下所示，你可以指定要忽略的多个信号：

    $ trap '' 1 2 3 15


注意，如果要一个信号被忽略掉，那么第一个参数必须是指定的空，它不等同于如下的命令，下面的命令有自己单独的意义：

    $ trap  2

如果你忽略了一个信号，那么你所有的子 shell 也会忽略此信号。然而，如果你指定了接收一个信号所采取的动作，那么所有的子 shell 接收到此信号后会采取相同动作。

## 重置 Traps： ##

当你改变了信号接收后的默认动作，你可以通过一个简单的省略第一个参数的 trap 命令将默认动作重置回来。

那么命令

    $ trap 1 2

将信号 1 和 2 接收后采取的动作重置为其原有的默认动作。