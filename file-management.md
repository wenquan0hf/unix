# 文件管理

在 UNIX 中的所有数据被都组织成文件。所有文件被都组织成目录。这些目录被组织成一个称为文件系统的树状结构。

当您使用 UNIX 时，你将花费大部分时间用一种方式或另一种方式去处理文件。本教程将教你如何创建和删除文件，复制和重命名它们，创建链接到它们等。

在 UNIX 中有三种基本类型的文件:

1. **普通文件:** 一个普通的文件是系统上包含数据、 文本或程序指令的文件。在本教程中，你将使用普通文件。

2. **目录:** 目录存储特殊和普通文件。 UNIX 目录对于熟悉 Windows 或者 Mac OS 的用户，相当于文件夹。

3. **特殊文件:** 一些特殊的文件提供访问硬件，例如硬盘、 CD - ROM 驱动器、 调制解调器和以太网适配器。其他特殊文件类似于别名或快捷方式，使您能够访问单个文件使用不同的名称。

## 文件列表

为了列出存储在当前目录中的文件和目录。使用下面的命令:

```
    $ls
```

这里是上述命令的示例输出:

```
    $ls
    
    binhosts  lib res.03
    ch07   hw1pub test_results
    ch07.bak   hw2res.01  users
    docs   hw3res.02  work
```

命令 **ls** 支持 **-l** 选项，将帮助您获得有关列出的文件的详细信息:

```
    $ls -l
    total 1962188
    
    drwxrwxr-x  2 amrood amrood  4096 Dec 25 09:59 uml
    -rw-rw-r--  1 amrood amrood  5341 Dec 25 08:38 uml.jpg
    drwxr-xr-x  2 amrood amrood  4096 Feb 15  2006 univ
    drwxr-xr-x  2 root   root4096 Dec  9  2007 urlspedia
    -rw-r--r--  1 root   root  276480 Dec  9  2007 urlspedia.tar
    drwxr-xr-x  8 root   root4096 Nov 25  2007 usr
    drwxr-xr-x  2200300  4096 Nov 25  2007 webthumb-1.01
    -rwxr-xr-x  1 root   root3192 Nov 25  2007 webthumb.php
    -rw-rw-r--  1 amrood amrood 20480 Nov 25  2007 webthumb.tar
    -rw-rw-r--  1 amrood amrood  5654 Aug  9  2007 yourfile.mid
    -rw-rw-r--  1 amrood amrood166255 Aug  9  2007 yourfile.swf
    drwxr-xr-x 11 amrood amrood  4096 May 29  2007 zlib-1.2.3
    $
```

这里是有关所有列出的列信息:

1. 第一列: 表示文件类型，给出了该文件的权限。后面是所有类型的文件的说明。

2. 第二列: 表示文件或目录所采取的内存块的数目。

3. 第三列: 表示该文件的所有者。这是创建此文件的 UNIX 用户。

4. 第四列: 表示用户组。每个 UNIX 用户会有一个相关联的组。

5. 第五列: 表示文件大小以字节为单位。

6. 第六列: 表示此文件被创建或最后一次修改的日期和时间。

7. 第七列: 表示文件或目录的名称。

在 `ls -l` 清单示例中，每个文件的行开头为 `d` ，`-` ，或 `l`。这些字符指示列出的文件的类型。

<table>
<tr>
<th align="left">前缀</th>
<th align="left">描述</th>
</tr>
<tr>
<td><strong> - </strong></td>
<td>常规的文件，如 ASCII 文本文件，二进制可执行文件，或硬链接。</td>
</tr>
<tr>
<td><strong> b </strong></td>
<td>特殊块文件。块输入输出设备文件如物理硬盘驱动器。</td>
</tr>
<tr>
<td><strong> c </strong></td>
<td>字符特殊文件。原始的输入/输出设备文件如物理硬盘驱动器。</td>
</tr>
<tr>
<td><strong> d </strong></td>
<td>包含其他文件和目录列表的目录文件。</td>
</tr>
<tr>
<td><strong> l </strong></td>
<td>符号链接文件。链接到任何一个普通的文件。</td>
</tr>
<tr>
<td><strong> p </strong></td>
<td>命名的管道。进程间通信机制。</td>
</tr>
<tr>
<td><strong> s </strong></td>
<td>用于进程间通信的套接字。</td>
</tr>
</table>

## 元字符

元字符在 UNIX 中具有特殊的意义。例如 `*` 和 `？` 是元字符。我们使用 `*`
 匹配 0 或多个字符，问号 `？` 与单个字符匹配。

举个例子:

```
    $ls ch*.doc
```

显示名称以 ch 开头，并以 .doc 结束的所有文件:

```
    ch01-1.doc   ch010.doc  ch02.docch03-2.doc 
    ch04-1.doc   ch040.doc  ch05.docch06-2.doc
    ch01-2.doc ch02-1.doc c
```

在这里 * 作为元字符可以和任何字符相匹配。如果你只是想要显示以 .doc 结尾的所有文件，你可以使用以下命令:

```
    $ls *.doc
```

## 隐藏文件

隐藏文件，是第一个字符是圆点或句点字符 `(.)` 的文件。 UNIX 程序  ( 包括 shell ) 大多数使用这些文件来存储配置信息。

隐藏文件的一些常见的例子包括文件:

- **.profile:** Bourne shell ( sh ) 初始化脚本。
- **.kshrc:** Korn shell ( ksh ) 初始化脚本。
- **.cshrc:** C shell ( csh ) 初始化脚本。
- **.rhosts:** remote shell 配置文件。

若要列出不可见文件，请指定到 `ls -a` 选项:

```
    $ ls -a
    
    . .profile   docs lib test_results
    ...rhostshostspub users
    .emacsbinhw1  res.01  work
    .exrc ch07   hw2  res.02
    .kshrcch07.bak   hw3  res.03
    $
```

- 单个点 **.** : 这个代表当前目录。
- 两个点 **..** : 这个代表父目录。

## 创建文件

您可以使用 **vi** 编辑器来创建任何 UNIX 系统上的普通文件。你只需要给出以下命令:

```
    $ vi filename
```

上面的命令会打开一个给定的文件名的文件。您将需要按键 **i** 来进入编辑模式。一旦您处于编辑模式下你可以在如下图所示文件中写入您的内容:

```
    This is unix file....I created it for the first time.....
    I'm going to save this content in this file.
```

一旦你做完上一步，请执行以下步骤:

- 按键 **esc** 退出编辑模式。
- 一起按两个键 **Shift + ZZ** 完全退出文件。

现在你会有一个已经创建好的叫 **filename** 的文件在当前目录中。

```
    $ vi filename
    $
```

## 编辑文件

您可以使用 **vi** 编辑器编辑现有的文件。我们将在一个单独的教程中详细介绍。但总之，您可以打开现有的文件，如下所示:

```
    $ vi filename
```

一旦文件被打开，您将能在编辑模式下按键 **i** ，然后您可以如您所想的编辑文件。如果您想要在一个文件里左右移动首先您需要按下键 **esc** 退出编辑模式来，然后您可以使用下列键在文件内部移动:

- **l** 键移动到右侧。
- **h** 键移动到左侧。
- **k** 键移动到上面。
- **j** 键移动到下面。

使用上面的键您可以将光标放在任何您想要编辑的地方。一旦您定位好然后您可以使用 **i** 键来在编辑模式下编辑该文件。当您编辑完文件您可以按下 **esc** 键然后按下 **Shift + ZZ** 键来从文件完全的退出。

## 显示文件的内容

你可以使用 **cat** 命令来查看文件的内容。以下是简单的示例来查看上面创建文件的内容:

```
    $ cat filename
    This is unix file....I created it for the first time.....
    I'm going to save this content in this file.
    $
```

你可以通过按如下方式使用 **-b** 选项和 **cat** 命令显示行号:

```
    $ cat -b filename
    1   This is unix file....I created it for the first time.....
    2   I'm going to save this content in this file.
    $
```

## 统计文件中字数

你可以使用 **wc** 命令来获取一个文件中的总的行数，字数和字符数。以下是简单的示例来查看有关上面创建的文件的信息:

```
    $ wc filename
    2  19 103 filename
    $
```

这里是所有四个列的细节:

1. 第一列: 代表文件中的行数。

2. 第二列: 代表文件中的字数。

3. 第三列: 代表文件中的字符数。这是文件的实际大小。

4. 第四列: 代表文件名。

在获取有关这些文件的信息的时候，你可以给多个文件。这里是简单的语法:

```
    $ wc filename1 filename2 filename3
```

## 复制文件

要使用 **cp** 命令文件的副本。该命令的基本语法如下:

```
    $ cp source_file destination_file
```

下面是创建一个已有文件 **filename** 的副本的例子。

```
    $ cp filename copyfile
    $
```

现在你会发现多了一个文件 **copyfile** 在您的当前目录。此文件与原始文件 **filename** 完全相同。

## 删除文件

若要更改文件的名称使用 **mv** 命令。其基本的语法是:

```
    $ mv old_file new_file
```

下面是把现有文件 **filename** 重命名为 **newfile** 的示例:

```
    $ mv filename newfile
    $
```

**mv** 命令将现有文件完全移动到新的文件。所以在这种情况下你只能发现 **newfile** 在你当前的目录中。

## 删除文件

若要删除现有文件使用 **rm** 命令。其基本的语法是:

```
    $ rm filename
```

**警告:** 要删除一个文件可能会很危险，因为它可能包含有用的信息。所以在使用此命令时要小心。这推荐使用 **-i** 选项和 **rm** 命令。

以下是完全删除现有文件 **filename** 的示例:

```
    $ rm filename
    $
```

您可以在一行中删除多个文件，如下所示:

```
    $ rm filename1 filename2 filename3
    $
```

## 标准 UNIX 流

在正常情况下每个 UNIX 程序在它启动时打开的三个流 ( 文件 ):

- **stdin :** 这指作为标准输入，关联文件描述符为 0。它也可以表示为 STDIN 。UNIX 程序默认从 STDIN 中读取。
- **stdout :** 这指作为标准输出，关联文件描述符为 1。它也可以表示为 STDOUT 。UNIX 程序默认从 STDOUT 中读取。
- **stderr :** 这指作为标准错误，关联文件描述符为 2。它也可以表示为 STDERR 。UNIX 程序会将所有的错误信息写入 STDERR。