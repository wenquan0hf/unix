# 目录

目录是一个文件，它的作用是存储文件的名称和相关的信息。所有的文件，无论是普通，特殊，或目录都包含在目录中。

UNIX 使用层次结构来组织文件和目录。这种结构通常被称为一个目录树。树上有一个根节点，斜杠字符 `(/)`，所有其他目录包含在它之下。

## 主目录

主目录是当您第一次登录时所在的目录。

您的大部分工作将在主目录及您自定义的子目录中完成。

在任意目录下执行以下命令可以随时切换到主目录：

```
    $cd ~
    $
```

在这里 `~` 表示主目录。如果您想要跳转至任何其他用户的主目录中，可以使用以下命令：

```
    $cd ~username
    $
```

跳转至您最近的目录中可以使用下列命令：

```
    $cd -
    $
```

## 绝对/相对路径名

目录采用分层方式组织，其顶部为根目录 `(/)`。层次结构内的任何文件的位置由其路径描述。

路径由 `/` 来分隔。路径名是绝对的如果它是描述与根的关系，所以绝对路径名的开头总是 `/`。

这些是绝对文件名的一些例子。

```
    /etc/passwd
    /users/sjones/chem/notes
    /dev/rdsk/Os3
```

路径也可以是相对于你当前的工作目录。相对路径永远不会以 `/` 开始。相对于用户 amrood 的主目录，一些路径可能看起来像这样：

```
    chem/notes
    personal/res
```

在任何时候要确定你所在的文件系统层次结构时，请输入命令 **pwd** 打印当前工作目录：

```
    $pwd
    /user0/home/amrood
    
    $
```

## 目录列表

要列出目录中的文件可以使用下面的语法：

```
    $ls dirname
```

以下是示例，列出 `/usr/local` 目录中包含的所有文件：

```
    $ls /usr/local
    
    X11   bin  gimp   jikes   sbin
    ace   doc  includelib share
    atalk etc  info   man ami
```

## 创建目录

通过下面的命令创建目录:

```
    $mkdir dirname
```

在这里，**dirname** 是您想要创建的目录的绝对或相对路径名。例如，命令：

```
    $mkdir mydir
    $
```

在当前目录中创建目录 **mydir**。这里是另一个示例：

```
    $mkdir /tmp/test-dir
    $
```

此命令在 `/tmp` 目录中创建目录 test-dir。命令 **mkdir** 不产生任何输出如果它成功创建请求的目录。

如果你在命令行上给出多个目录，mkdir 创建每个目录。例如：

```
    $mkdir docs pub
    $
```

在当前目录下创建目录 docs 和 pub 。

## 创建父目录

有时当你想要创建一个目录，其父目录可能不存在。在这种情况下，**mkdir** 发出一个错误消息，如下所示：

```
    $mkdir /tmp/amrood/test
    mkdir: Failed to make directory "/tmp/amrood/test"; 
    No such file or directory
    $
```

在这种情况下，您可以指定 **mkdir** 命令的 **-p** 选项。它为您创建所有必要的目录。例如：

```
    $mkdir -p /tmp/amrood/test
    $
```

上面的命令创建所需的父目录。

## 删除目录

可以按如下方式使用 **rmdir** 命令删除目录：

```
    $rmdir dirname
    $
```

**注意:** 删除目录时请确保它是空的，这意味着不应该在这个目录里有任何文件或子目录。

您可以一次创建多个目录如下:

```
    $rmdir dirname1 dirname2 dirname3
    $
```

上面的命令删除目录 dirname1、dirname2 和 dirname2，前提是它们是空的。如果成功删除，rmdir 命令不生成任何输出。

## 更改目录

你可以使用 **cd** 命令来做比更改主目录更多的事：你可以使用它来跳转到任何目录，其参数为一个有效的绝对或相对路径。语法如下所示:

```
    $cd dirname
    $
```

在这里，dirname 是你想要跳转到的目录的名称。例如，命令:

```
    $cd /usr/local/bin
    $
```

更改目录 `/usr/local/bin`。从该目录，您可以使用下面的相对路径跳转到 `/usr/home/amrood` 目录:

```
    $cd ../../home/amrood
    $
```

## 重命名目录

mv ( move ) 命令也可以用于重命名目录。语法如下所示:

```
    $mv olddir newdir
    $
```

您可以重命名目录 **mydir** 为 **yourdir**，如下所示:

```
    $mv mydir yourdir
    $
```

## 目录 . ( 点 ) 和 .. ( 点点 ) 

文件名 `.` ( 点 ) 表示当前的工作目录；和文件名 `..` ( 点点 ) 代表当前工作目录的上一级，通常被称为父目录。

如果我们输入要显示的当前工作目录文件的列表，使用 `-a` 选项列出所有的文件与 `-l` 选项提供长列表，这是结果。

```
    $ls -la
    drwxrwxr-x4teacher   class   2048  Jul 16 17.56 .
    drwxr-xr-x60   root  1536  Jul 13 14:18 ..
    ----------1teacher   class   4210  May 1 08:27 .profile
    -rwxr-xr-x1teacher   class   1948  May 12 13:42 memo
    $
```