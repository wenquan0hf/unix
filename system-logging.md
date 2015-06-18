# UNIX 系统日志 #

UNIX 系统有一个非常灵活和强大的日志系统，它让你能够记录几乎任何你能想象的东西，然后你可以操作日志来获取你需要的信息。

许多版本的 UNIX 提供了一个名为 *syslog* 的通用日志工具，有信息需要记录的单独程序要将信息发送到 syslog。

Unix *syslog* 是一个主机可配置的，统一的系统日志工具。该系统采用集中式的系统日志进程，其运行程序 /etc/syslogd 或者 /etc/syslog。

系统记录器的操作是相当简单的。程序发送日志条目到 *syslogd*，其将会在配置文件 /etc/syslogd.conf 或 /etc/syslog 中查找，当找到一个匹配后，将日志消息写入到期望的日志文件中。

现有你应该了解的四种基本日志术语：

<table>
<tr>
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
   <tr>
      <td>Facility</td>
      <td>此标识符用来描述提交的日志信息的应用程序或进程。例如邮件，内核和 FTP。</td>
   </tr>
   <tr>
      <td>Priority</td>
      <td>一个显示消息重要性的指示器。syslog 作为准则定义了消息的级别，从调试信息到关键事件。</td>
   <tr>
      <td>Selector</td>
      <td>一个或更多的 facility 和 level 的结合体 。当一个输入事件匹配一个 selector 时，一个 action 会被执行。</td>
   </tr>
   <tr>
      <td>Action</td>
      <td>传入的消息匹配 selector 时会发生的事情。Action 可以将消息写入日志文件，将消息回传到控制台或其他设备，将消息写入到一个登录用户，或将消息发送到另一个日志服务器。</td>
   </tr>
</table>

## Syslog Facilities： ##
下面是 selector 可用的 facility。不是所有的 facility 都存在于所有版本的 UNIX。


<table>
<tr>
<th align="left">Facility</th>
<th align="left">描述</th>
</tr>
   <tr>
      <td>auth</td>
      <td>需要用户名和密码的相关活动（getty，su，login）</td>
   </tr>
   <tr>
      <td>authpriv</td>
      <td>类似于 auth 的认证，但是记录的文件只能被授权的用户读取。</td>
   </tr>
   <tr>
      <td>console</td>
      <td>用于捕获信息，这些信息一般会传向系统控制台。</td>
   </tr>
   <tr>
      <td>cron</td>
      <td>与 cron 系统有关的计划任务信息。</td>
   </tr>
   <tr>
      <td>daemon</td>
      <td>所捕获的所有系统守护进程信息。</td>
   </tr>
   <tr>
      <td>ftp</td>
      <td>ftp 守护进程相关的信息。</td>
   </tr>
   <tr>
      <td>kern</td>
      <td>内核信息。</td>
   </tr>
   <tr>
      <td>local0.local7</td>
      <td>用户自定义使用的本地信息。</td>
   </tr> 
   <tr>
      <td>lpr</td>
      <td>与打印服务系统有关的信息。</td>
   </tr>
   <tr>
      <td>mail</td>
      <td>与邮件系统相关的信息。</td>
   </tr>
   <tr>
      <td>mark</td>
      <td>用于生产日志文件中时间戳的伪事件。</td>
   </tr>
   <tr>
      <td>news</td>
      <td>与网络新闻传输协议( nntp )有关的信息。</td>
   </tr>
   <tr>
      <td>ntp</td>
      <td>与网络时间协议有关的信息。</td>
   </tr>
   <tr>
      <td>user</td>
      <td>普通用户进程产生的信息。</td>
   </tr>
   <tr>
      <td>uucp</td>
      <td>UUCP 子系统生成的信息。</td>
   </tr>
</table>


## Syslog 优先级： ##

syslog 的优先级( Priority )如下表：

<table>
<tr>
<th align="left">Priority</th>
<th align="left">描述</th>
</tr>
   <tr>
      <td>emerg</td>
      <td>紧急情况，如即将发生的系统崩溃，通常会广播到所有用户。</td>
   </tr>
   <tr>
      <td>alert</td>
      <td>需要立即修改的情况，如系统数据库的损坏。</td>
   </tr>
   <tr>
      <td>crit</td>
      <td>关键的情况，如一个硬件的错误。</td>
   </tr>
   <tr>
      <td>err</td>
      <td>普通错误。</td>
   </tr>
   <tr>
      <td>warning</td>
      <td>警告</td>
   </tr>
   <tr>
      <td>notice</td>
      <td>不是一个错误的情况，但是可能需要用特定方式的处理一下。</td>
   </tr>
   <tr>
      <td>info</td>
      <td>报告性的消息。</td>
   </tr>  
   <tr>
      <td>debug</td>
      <td>用于调试程序的消息。</td>
   </tr>
   <tr>
      <td>none</td>
      <td>没有重要级别，通常用于指定非日志的消息。</td>
   </tr>
</table>

facility 和 level 的组合能够让你辨别记录了什么和这些日志信息去哪儿了。

每个程序尽职尽责地向系统记录器发送消息，记录器基于 selector 定义的 level 决定跟踪什么和舍弃什么信息。

当你指定了一个 level，系统会记录这一 level 及更高 level 的一切信息。

## 文件 /etc/syslog.conf： ##

文件 /etc/syslog.conf 用于配置记录消息的位置。一个典型的 syslog.conf 文件看起来应该像这样：


	*.err;kern.debug;auth.notice /dev/console
	daemon,auth.notice           /var/log/messages
	lpr.info                     /var/log/lpr.log
	mail.*                       /var/log/mail.log
	ftp.*                        /var/log/ftp.log
	auth.*                       @prep.ai.mit.edu
	auth.*                       root,amrood
	netinfo.err                  /var/log/netinfo.log
	install.*                    /var/log/install.log
	*.emerg                      *
	*.alert                      |program_name
	mark.*                       /dev/console


文件中的每一行包含两部分：

- 一个消息 selector，其指定了哪种消息用来记录。例如，内核的所有错误信息或所有调试信息。

- 一个 action，其指明了对接收的消息该怎么处理。例如，写入一个文件中或者将消息发送到用户的终端。

下面是上述配置的注意事项：

- 消息 selector 有两部分：facility 和 priority。例如， kern.debug 选择了所有由内核( facility )产生的的调试信息( priority )。

- 消息 selectetor kern.debug 选择了所有 priority 大于 debug 的信息。

- 在任何 facility 和 priority 位置上的星号，表示“所有”的意思。例如， \*.debug 表示所有 facility 的调试信息，而 kern.\* 表示内核所产生的所有信息。

- 你也可以用逗号来指定多个 facility。两个或两个以上的 selectetor 可以用分号组合在一起。

## 日志记录 Action： ##

action 部分指定了下面五个 action 中的其中一个：

1. 将信息记录到一个文件或设备。例如，/var/log/messages lpr.log 或者 /dev/console。
2. 发送一个消息给一个用户。你可以用逗号分开指定多个用户名（例如，root，amrood）。
3. 发送一个消息给所有用户。在这种情况下，action 部分包含了一个星号（例如，\*）。
4. 用管道发送消息到程序。在这种情况下，程序是在 UNIX 管道符号（|）后指定。
5. 将消息发送到另一台主机上的 syslog。在这种情况下，action 部分包含了一个前面有 at 符号的主机名（例如，@tutorialspoint.com）。

## logger 命令： ##

UNIX 提供了 **logger** 命令，这是处理系统日志记录的一个非常有用的命令。**logger** 命令发送日志消息到 syslogd 守护进程，从而驱使系统记录日志。

这意味着我们可以随时用命令行检查 **syslogd** 守护进程及其配置。logger 命令提供了一种在命令行上添加一行条目到系统日志文件中的方法。

该命令的格式是：

    logger [-i] [-f file] [-p priority] [-t tag] [message]...

下面是具体的参数细节：

<table>
<tr>
<th align="left">选项</th>
<th align="left">描述</th>
</tr>
   <tr>
      <td>-f filename</td>
      <td>使用文件 filename 的内容作为消息来记录。</td>
   </tr>
   <tr>
      <td>-i</td>
      <td>日志的每一行都记录进程的 id。</td>
   </tr>
   <tr>
      <td>-p priority</td>
      <td>指定输入消息的优先级 priority（指定的 selector），优先级 priority 可以是数字或者指定为 facility.level 对的格式。默认参数是 user.notice。</td>
   </tr>
   <tr>
      <td>-t tag</td>
      <td>用指定 tag 标记记录到日志中的每一行。</td>
   </tr>  
   <tr>
      <td>message</td>
      <td>字符串参数，它的内容以特定顺序连接在一起，由空格分开。</td>
   </tr>
</table>

## 日志轮换： ##

日志文件有快速增长的特点，并消耗大量的磁盘空间。大多数 UNIX 发行版系统使用了工具（如 newsyslog 或 logrotate）启用日志轮换功能。

这些工具由 cron 守护进程在一个频繁的时间间隔里调用。你可以在 newsyslog 或 logrotate 的手册页中获取更多的细节内容。

## 重要日志文件的位置 ##

所有的系统应用程序创建自己的日志文件在 /var/log 和它的子目录里。下面这里有几个重要的应用，其相应的日志目录：

<table>
<tr>
<th align="left">应用</th>
<th align="left">目录</th>
</tr>
   <tr>
      <td>httpd</td>
      <td>/var/log/httpd</td>
   </tr>
   <tr>
      <td>samba</td>
      <td>/var/log/samba</td>
   </tr>
   <tr>
      <td>cron</td>
      <td>/var/log/</td>
   </tr>
   <tr>
      <td>mail</td>
      <td>/var/log/</td>
   </tr>
   <tr>
      <td>mysql</td>
      <td>/var/log/</td>
   </tr>
</table>