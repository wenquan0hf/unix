# Unix-网络通信实用工具 #

如果用户在分布式环境下工作，那么用户就需要与远程用户通信，用户也需要远程方式访问Unix主机。   

如下是一些Unix操作系统中的实用工具，这些工具专用于分布式环境下的用户间的网络通信。本教程列出的如下：

## ping工具 ##

ping 指令会发送一个应答请求到网络中某个主机。该指令主要用于检测远端主机是否可以正常通信。  

ping 指令可以用于如下用途：   

1. 追踪并区分硬件或软件的问题。
1. 确定网络和远端主机的状态。
1. 测试、测量或网络管理。   

## 语法： ##

如下是使用 **ping** 指令的语法：   

    $ping hostname or ip-address


上述指定会持续打印响应信息。用户可以同时按下 CTRL+C 按键来结束信息的打印.

## 例子： ##

下面是检测网络中某主机是否可达的例子：

    $ping google.com
    PING google.com (74.125.67.100) 56(84) bytes of data.
    64 bytes from 74.125.67.100: icmp_seq=1 ttl=54 time=39.4 ms
    64 bytes from 74.125.67.100: icmp_seq=2 ttl=54 time=39.9 ms
    64 bytes from 74.125.67.100: icmp_seq=3 ttl=54 time=39.3 ms
    64 bytes from 74.125.67.100: icmp_seq=4 ttl=54 time=39.1 ms
    64 bytes from 74.125.67.100: icmp_seq=5 ttl=54 time=38.8 ms
    --- google.com ping statistics ---
    22 packets transmitted, 22 received, 0% packet loss, time 21017ms
    rtt min/avg/max/mdev = 38.867/39.334/39.900/0.396 ms
    $  


如果某个主机不可达，那么会显示如下信息：   

    $ping giiiiiigle.com
    ping: unknown host giiiiigle.com
    $  

## FTP工具 ##

ftp就是文件传输协议（File Transter protocol）的简称。使用该工具可以帮助用户在主机间上传或下载文件。

ftp工具拥有自己的UNIX指令，可以完成如下任务：

1. 链接并登陆到远程主机。
1. 浏览目录。
1. 列出目录内容。
1. 上传或下载文件。
1. 按照ascii、ebcdic或binary方式传输文件。

## 语法： ##

如下是使用 **ftp** 指令的语法：

    $ftp hostname or ip-address


上述指令会触发一个输入账号和密码的登陆界面。如果用户输入的账号和密码认证通过，则用户可以访问相应输入账户的根目录，然后就可以执行多种操作。

下面是一些常用操作：

<table>
<tbody>
<tr>
<th>指令</th>
<th>描述</th>

</tr>
<tr>
<td>put filename</td> <td> 从本地往远程服务器上传文件</td> 
</tr>

</tr>
<tr>
<td>get filename</td> <td>从远程服务器往本地下载文件</td> 
</tr>

</tr>
<tr>
<td>mput file list</td> <td>从本地往远程服务器批量上传文件</td> 
</tr>

</tr>
<tr>
<td>mget file list</td> <td>从远程服务器往本地批量下载文件</td> 
</tr>

</tr>
<tr>
<td>prompt off</td> <td>关闭文件提醒,在 mput 与 mget 时不会每操作一个文件就询问一次。</td> 
</tr>

</tr>
<tr>
<td>prompt on</td> <td>开启文件提醒</td> 
</tr>

</tr>
<tr>
<td>dir</td> <td>列出远程服务器上当前目录下的所有文件</td> 
</tr>


</tr>
<tr>
<td>cd dirname</td> <td>切换本地主机上的目录到指定目录下</td> 
</tr>

</tr>
<tr>
<td>lcd dirname</td> <td>切换远程服务器上的目录到指定目录下</td> 
</tr>

</tr>
<tr>
<td>quit</td> <td>注销当前登陆</td> 
</tr>

</tbody>
</table> 


需要注意的是，上传和下载文件时的本地主机目录都是当前目录。如果用户希望上传或下载文件的目录为特定的目录，那么用户需要先将当前目录切换到指定目录后再进行上传或下载操作。  


## 例子： ##

下面是一些关于ftp操作的例子：

    $ftp amrood.com
    Connected to amrood.com.
    220 amrood.com FTP server (Ver 4.9 Thu Sep 2 20:35:07 CDT 2009)
    Name (amrood.com:amrood): amrood
    331 Password required for amrood.
    Password:
    230 User amrood logged in.
    ftp> dir
    200 PORT command successful.
    150 Opening data connection for /bin/ls.
    total 1464
    drwxr-sr-x   3 amrood   group   1024 Mar 11 20:04 Mail
    drwxr-sr-x   2 amrood   group   1536 Mar  3 18:07 Misc
    drwxr-sr-x   5 amrood   group512 Dec  7 10:59 OldStuff
    drwxr-sr-x   2 amrood   group   1024 Mar 11 15:24 bin
    drwxr-sr-x   5 amrood   group   3072 Mar 13 16:10 mpl
    -rw-r--r--   1 amrood   group 209671 Mar 15 10:57 myfile.out
    drwxr-sr-x   3 amrood   group512 Jan  5 13:32 public
    drwxr-sr-x   3 amrood   group512 Feb 10 10:17 pvm3
    226 Transfer complete.
    ftp> cd mpl
    250 CWD command successful.
    ftp> dir
    200 PORT command successful.
    150 Opening data connection for /bin/ls.
    total 7320
    -rw-r--r--   1 amrood   group   1630 Aug  8 1994  dboard.f
    -rw-r-----   1 amrood   group   4340 Jul 17 1994  vttest.c
    -rwxr-xr-x   1 amrood   group 525574 Feb 15 11:52 wave_shift
    -rw-r--r--   1 amrood   group   1648 Aug  5 1994  wide.list
    -rwxr-xr-x   1 amrood   group   4019 Feb 14 16:26 fix.c
    226 Transfer complete.
    ftp> get wave_shift
    200 PORT command successful.
    150 Opening data connection for wave_shift (525574 bytes).
    226 Transfer complete.
    528454 bytes received in 1.296 seconds (398.1 Kbytes/s)
    ftp> quit
    221 Goodbye.
    $


## telnet工具 ##


用户在工作经常会遇到这样的需求：用户需要连接到远程Unix主机且需要在远程主机上进行操作。Telnet 就是一个允许用户对远程服务器进行连接、登陆且可以进行远程操作的工具。

一旦用户使用 telnet 工具登陆到了远程服务器上，那么用户就可以像在本地主机操作那样操作远程服务器来执行任务。下面是 telnet 对话的一个例子：

    C:>telnet amrood.com
    Trying...
    Connected to amrood.com.
    Escape character is '^]'.
    
    login: amrood
    amrood's Password: 
    *****************************************************
    *   *
    *   *
    *WELCOME TO AMROOD.COM  *
    *   *
    *   *
    *****************************************************
    
    Last unsuccessful login: Fri Mar  3 12:01:09 IST 2009
    Last login: Wed Mar  8 18:33:27 IST 2009 on pts/10
    
       {  do your work }
    
    $ logout
    Connection closed.
    C:>    



## finger 工具 ##


finger 指令用于显示指定主机上有关用户的信息。这里的主机可以是本地主机，也可以是远程服务器。   

由于安全原因，finger 也能在其他系统中使用。   

下面是使用 finger 指令的简单语法。

检测本地主机中登陆用户的信息的例子如下：

    $ finger
    Login Name   Tty  Idle  Login Time   Office amrood   pts/0  Jun 25 08:03 (62.61.164.115)   


获取本地主机上指定有效用户的信息的例子如下：

    $ finger amrood
    Login: amrood   Name: (null)
    Directory: /home/amrood Shell: /bin/bash
    On since Thu Jun 25 08:03 (MST) on pts/0 from 62.61.164.115
    No mail.
    No Plan.   


检测远程服务器中所有登陆用户的信息的例子如下：
    
     $ finger @avtar.com
    Login Name   Tty  Idle  Login Time   Office
    amrood   pts/0  Jun 25 08:03 (62.61.164.115)   



获取远程服务器上的指定有效用户信息的例子如下：   


    $ finger amrood@avtar.com
    Login: amrood   Name: (null)
    Directory: /home/amrood Shell: /bin/bash
    On since Thu Jun 25 08:03 (MST) on pts/0 from 62.61.164.115
    No mail.
    No Plan.

 
