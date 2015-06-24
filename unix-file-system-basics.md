## Unix 文件系统基础知识

文件系统是一个分区或磁盘上的文件的逻辑集合。一个分区是一个信息的容器，如果需要可以跨整个硬盘。

你的硬盘可以有不同的分区，但通常只包含一个文件系统，如一个文件系统涵盖 /file 系统，另一个包含 /home 文件系统。

一个文件系统分区允许不同文件系统的逻辑维护和管理。

Unix 中一切都被认为是一个文件，包括物理设备，如 DVD-ROMs、USB 设备、软盘驱动器等等。

### 目录结构:

Unix 使用文件系统层次结构，就像一棵倒置的树，根目录(/) 是文件系统的底部，所有其他的目录都从那里蔓延。

UNIX 文件系统是文件和目录的集合，具有以下属性：

- 它有一个根目录 (/)，包含其他的文件和目录。
- 使用名字唯一地标识每个文件或目录，这个名字可以是它所在的目录，或者一个独特的标识符，通常被称为一个 inode。
- 按照惯例，根目录的 inode 编号为 2，lost+found目录的 inode 编号为 3。Inode编号 0 和 1 暂不使用。文件的 inode 编号可以通过 ls 命令的 -i 选项指定。
- 它是自包含的。一个文件系统和其他文件系统之间没有依赖关系。

目录有特定的目的，通常存储相同类型的信息以实现更容易定位文件的目的。以下是主要的 Unix 版本上存在的目录：
<table>
<tr>
<th>目录</th>
<th>描述</th>
</tr>
<tr>
<td>/</td>
<td>这是根目录，只包含顶层文件结构所需的目录。</td>
</tr>
<tr>
<td>/bin</td>
<td>这是可执行文件所在的地方。他们提供给所有用户使用。</td>
</tr>
<tr>
<td>/dev</td>
<td>这些是设备驱动程序。</td>
</tr>
<tr>
<td>/etc</td>
<td>上级目录的命令，配置文件，磁盘配置文件，有效的用户列表，组，以太网，主机等各种发送重要信息的地方。</td>
</tr>
<tr>
<td>/lib</td>
<td>包含共享库文件，例如其他内核相关文件。</td>
</tr>
<tr>
<td>/boot</td>
<td>包含系统启动相关的文件。</td>
</tr>
<tr>
<td>/home</td>
<td>包含用户的主目录和其他账户。</td>
</tr>
<tr>
<td>/mnt</td>
<td>用来挂载其他临时文件系统，比如分别针对光盘和软盘的 CD-ROM 驱动器和软盘驱动器。</td>
</tr>
<tr>
<td>/proc</td>
<td>标记为一个包含所有进程的文件，这些进程使用进程编号或其他信息标记。这个文件是一个动态的系统。</td>
</tr>
<tr>
<td>/tmp</td>
<td>包含系统启动期间所有的临时文件。</td>
</tr>
<tr>
<td>/uer</td>
<td>用于各种各样的用途，可以被许多用户使用。包括行政命令、共享文件、库文件等等。</td>
</tr>
<tr>
<td>/var</td>
<td>通常包含变长文件，如日志和打印文件和任何其他类型的文件，该文件包含的数据的量可能是变化的。</td>
</tr>
<tr>
<td>/sbin</td>
<td>包含二进制(可执行的)文件，通常用于系统管理。比如 fdisk 和 ifconfig 功能。</td>
</tr>
<tr>
<td>/kernel</td>
<td>包含内核文件。</td>
</tr>
</table>

### 浏览文件系统：

既然已经了解了文件系统的基本知识，现在就可以开始导航到所需要的文件。以下列出导航到文件系统可以使用的命令：

<table>
<tr>
<th>命令</th>
<th>描述</th>
</tr>
<tr>
<td>cat filename</td>
<td>显示文件名。</td>
</tr>
<tr>
<td>cd dirname</td>
<td>移动到确定的目录。</td>
</tr>
<tr>
<td>cp file1 file2</td>
<td>复制一个文件/目录到指定位置。</td>
</tr>
<tr>
<td>file filename</td>
<td>识别文件类型(二进制、文本等)。</td>
</tr>
<tr>
<td>find filename dir</td>
<td>发现一个文件/目录。</td>
</tr>
<tr>
<td>head filename</td>
<td>显示一个文件的开始。</td>
</tr>
<tr>
<td>less filename</td>
<td>从结束或开始位置浏览一个文件。</td>
</tr>
<tr>
<td>ls dirname</td>
<td>显示指定目录的内容。</td>
</tr>
<tr>
<td>mkdir dirname</td>
<td>创建指定目录。</td>
</tr>
<tr>
<td>more filename</td>
<td>从头到尾浏览一个文件。</td>
</tr>
<tr>
<td>mv file1 file2</td>
<td>移动一个文件/目录的位置或重命名一个文件/目录。</td>
</tr>
<tr>
<td>pwd</td>
<td>显示用户当前所在的目录。</td>
</tr>
<tr>
<td>rm filename</td>
<td>删除一个文件。</td>
</tr>
<tr>
<td>rmdir dirname</td>
<td>删除一个目录。</td>
</tr>
<tr>
<td>tail filename</td>
<td>显示一个文件的结束。</td>
</tr>
<tr>
<td>touch filename</td>
<td>创建一个空白文件或修改现有文件的属性。</td>
</tr>
<tr>
<td>whereis filename</td>
<td>显示一个文件的位置。</td>
</tr>
<tr>
<td>which filename</td>
<td>如果文件在你的路径内，显示它的位置，。</td>
</tr>
</table>

您可以使用 [Manpage Help](http://www.tutorialspoint.com/unix/unix-manpage-help.htm) 查看这里提到每个命令的完整语法。

### df命令:

管理分区空间的第一种方式是 df (磁盘空闲)命令。命令 df -k(磁盘空闲)以千字节的形式显示磁盘空间的使用情况，如下所示：

    $df -k
    Filesystem  1K-blocks  Used   Available Use% Mounted on
    /dev/vzfs10485760   7836644 2649116  75% /
    /devices0 0   0   0% /devices
    $

一些目录，比如 /devices，以千字节形式显示使用为 0，且可用列以及能力都为 0%。这些特殊的(或虚拟的)文件系统，虽然他们驻留在磁盘上，但他们本身不占用磁盘空间。

在所有Unix系统上 df -k 的输出通常都是相同的。它一般包括：

<table>
<tr>
<th>列</th>
<th>描述</th>
</tr>
<tr>
<td>Filesystem</td>
<td>物理文件系统名称。</td>
</tr>
<tr>
<td>kbytes</td>
<td>存储介质上的可用空间总字节。</td>
</tr>
<tr>
<td>used</td>
<td>被文件使用过的空间的总字节。</td>
</tr>
<tr>
<td>avail</td>
<td>可用空间的总字节。</td>
</tr>
<tr>
<td>capacity</td>
<td>被文件使用的空间和总额的比例。</td>
</tr>
<tr>
<td>Mounted on</td>
<td>文件系统正在安装的。</td>
</tr>
</table>

您可以使用 -h (可读的)选项来设置显示，使用易于理解的符号，合适的大小等输出格式。

### du命令:

du (磁盘使用量) 命令使您能够按指定目录来显示一个特定的目录中磁盘空间的使用情况。

如果你想判断一个特定的目录正在使用多少空间，这个命令是很有用的。以下命令将显示被每个目录消耗的块的数量。根据系统的不同，一个块可能需要 512 字节或 1 千字节。

    $du /etc
    10 /etc/cron.d
    126/etc/default
    6  /etc/dfs
    ...
    $

-h 选项使输出更容易理解:

    $du -h /etc
    5k/etc/cron.d
    63k   /etc/default
    3k/etc/dfs
    ...
    $

### 挂载文件系统：

文件系统必须安装以用于系统的正常使用。为了查看您的系统上目前安装(可用)的文件系统，可以使用这个命令：

    $ mount
    /dev/vzfs on / type reiserfs (rw,usrquota,grpquota)
    proc on /proc type proc (rw,nodiratime)
    devpts on /dev/pts type devpts (rw)
    $

Unix协定的 /mnt 目录，就是临时挂载的地方(例如 CD-ROM 驱动器，远程网络驱动器，软盘驱动器)。如果你需要挂载文件系统，您可以使用 mount 命令，语法如下：

    mount -t file_system_type device_to_mount directory_to_mount_to

例如，如果你想挂载 CD-ROM 到目录 /mnt/cdrom，你可以输入：

    $ mount -t iso9660 /dev/cdrom /mnt/cdrom

假设您的 CD-ROM 设备称为 /dev/cdrom，你想挂载到 /mnt/cdrom。可以参考安装手册页获得更具体的信息或类型，在命令行输入 -h 得到帮助信息。

安装之后，您可以使用 cd 命令通过挂载点来浏览可用的新文件系统。

### 卸载文件系统:

通过识别挂载点或设备，从你的系统中卸载(删除)文件系统。使用 **umount** 命令实行。

例如，可以使用以下命令卸载光盘：

    $ umount /dev/cdrom

mount 命令使你能够访问你的文件系统，但在大多数现代Unix系统中，加载函数使这个过程对用户不可见且不需要用户干预。

### 用户和组配额:

提供用户和组配额的机制：单个用户或特定组中的所有用户所使用的空间量可以由管理员定义的值限制。

配额操作有两种限制。如果空间的数量或磁盘块的数量开始超过管理员定义的限制，允许用户采取行动：

- **软限制**：如果用户超过限制的定义，有一个宽限度，允许用户释放一些空间。
- **硬限制**：当达到硬限制使，忽略宽限度，没有进一步的文件或块可以分配。

有许多命令来管理配额:

<table>
<tr>
<th>命令</th>
<th>描述</th>
</tr>
<tr>
<td>quota</td>
<td>显示组中一个用户的磁盘使用情况和限制。</td>
</tr>
<tr>
<td>edquota</td>
<td>这是一个配额编辑器。可以使用这个命令编辑用户或组配额。</td>
</tr>
<tr>
<td>quotacheck</td>
<td>扫描文件系统，为了磁盘使用、制造、检查和修复配额文件</td>
</tr>
<tr>
<td>setquota</td>
<td>这也是一个命令行配额编辑器。</td>
</tr>
<tr>
<td>quotaon</td>
<td>系统宣布应该在一个或多个文件系统上启用磁盘配额。</td>
</tr>
<tr>
<td>quotaoff</td>
<td>系统宣布应该禁用一个或多个文件系统上的磁盘配额。</td>
</tr>
<tr>
<td>repquota</td>
<td>打印指定文件系统的磁盘使用和配额的汇总</td>
</tr>
</table>
您可以使用 [Manpage Help](http://www.tutorialspoint.com/unix/unix-manpage-help.htm) 查看这里提到每个命令的完整语法。