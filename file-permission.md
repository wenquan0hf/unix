# 文件权限

文件所有权是 UNIX 的一个重要的组成部分，提供了一种安全的方法来存储文件。在 UNIX 中每个文件有以下属性:

- 所有者权限：所有者的权限决定文件的所有者可以对文件执行的操作。
- 组权限：组权限决定了属于该组的成员对他所拥有的文件能够执行的操作。
- 其他人权限：其他人权限表示其他所有人对于该文件能够进行的操作。

## 权限表示符

当使用 **ls -l** 命令的时候，会将与文件相关的各种权限展示出来，如下：

```
$ls -l /home/amrood
-rwxr-xr--  1 amrood   users 1024  Nov 2 00:10  myfile
drwxr-xr--- 1 amrood   users 1024  Nov 2 00:10  mydir
```

输出的第一列表示的是与文件或者目录相关的访问模式或者权限。

权限被分为三组，组中的每个位置代表一个特定的权限，这个顺序是：读(r)、写(w)和执行(x):

- 前三个字符 (2-4) 表示文件的所有者的权限。例如 `-rwxr-xr--` 代表，文件的所有者拥有读 (r)、写 (w) 和执行 (x) 的权限。
- 第二组的三个字符 (5-7) 包含了该文件所属组的权限。例如 `-rwxr-xr--` 表示了所属组拥有读 (r) 和执行 (x) 的权限，但没有写权限。
- 最后一组三个字符 (8-10) 代表其他人的权限。例如 `-rwxr-xr--` 代表其他人只有读 (r) 的权限。

## 文件访问模式

文件的权限是 UNIX 系统安全性的第一道防线。UNIX 权限的基本组成部分是**读，写，执行**权限，如下所述:

1. **读：**分配对文件的内容进行读取和查看文件的权限。
2. **写：**分配对文件的内容进行修改或者删除的权限。
3. **执行：**允许用户将该文件作为一个程序进行执行的权限。

## 目录访问模式

目录访问模式采用和其他文件用相同的方式组织。但是有一些差异，还是需要提到:

1. **读：**访问目录意味着用户可以读取目录下的内容。用户可以查看目录内的文件名。
2. **写：**这个权限意味着用户可以在目录下面删除或者新建文件。
3. **执行：**执行一个目录并没有真正的意义，因此将它当作可以遍历目录的权限。

用户为了执行 ls 或者 cd 命令就必须先访问了 **bin** 目录。

## 改变权限

改变文件或目录的权限，您可以使用 chmod(change mode)命令。有两种方法可以使用 chmod：符号模式和绝对模式。

## 符号模式中使用 chmod

对于初学者来说使用符号模式是最简单的来修改文件或目录的权限方法。可以用下表中的符号来添加、删除或指定你想要设置的权限。

<table>
<tr>
<th style="width:25%">Chmod 操作符</th><th style="width:45%">描述</th>
</tr>
<tr><td><b>+</b></td><td>给文件或者目录添加指定的权限。</td></tr>
<tr><td><b>-</b></td><td>删除文件或者目录的权限。</td></tr>
<tr><td><b>=</b></td><td>设置指定的权限。</td></tr>
</table>

如下是以 testfile 文件为示例。对 testfile 文件运行 `ls -l` 就会像下面一样显示文件的权限：

```
$ls -l testfile
-rwxrwxr--  1 amrood   users 1024  Nov 2 00:10  testfile
```

接下来将前面表格中的 chmod 命令都对 testfile 运行一下，下面的是在 `ls -l` 运行之后，你可以看到文件权限的改变：

```
$chmod o+wx testfile
$ls -l testfile
-rwxrwxrwx  1 amrood   users 1024  Nov 2 00:10  testfile
$chmod u-x testfile
$ls -l testfile
-rw-rwxrwx  1 amrood   users 1024  Nov 2 00:10  testfile
$chmod g=rx testfile
$ls -l testfile
-rw-r-xrwx  1 amrood   users 1024  Nov 2 00:10  testfile
```

下面将展示如何将上面的命令组合成一行：

```
$chmod o+wx,u-x,g=rx testfile
$ls -l testfile
-rw-r-xrwx  1 amrood   users 1024  Nov 2 00:10  testfile
```
## chmod 命令中使用绝对权限

用chmod命令修改权限的第二种方法，是使用一个数字来指定文件的一些列权限。

每个权限被分配了一个数值，如下表所示， 并且给每个权限集的总和提供了一个数值。

<table>
<tr>
<th>数值</th><th style="width:75%">权限八进制表示</th><th>参照</th>
</tr>
<tr><td><b>0</b></td><td>没有权限</td><td>---</td></tr>
<tr><td><b>1</b></td><td>可执行的权限</td><td>--x</td></tr>
<tr><td><b>2</b></td><td>写权限</td><td>-w-</td></tr>
<tr><td><b>3</b></td><td>执行和写权限: 1 (执行) + 2 (写) = 3</td><td>-wx</td></tr>
<tr><td><b>4</b></td><td>读取权限</td><td>r--</td></tr>
<tr><td><b>5</b></td><td>读取和执行权限: 4 (读取) + 1 (执行) = 5</td><td>r-x</td></tr>
<tr><td><b>6</b></td><td>读取和写权限: 4 (读) + 2 (写) = 6</td><td>rw-</td></tr>
<tr><td><b>7</b></td><td>所有权限: 4 (读) + 2 (写) + 1 (执行) = 7</td><td>rwx</td></tr>
</table>

如下是针对 testfile 文件的示例。运行 ls -l 命令会显示与该文件相关的权限如下：

```
$ls -l testfile
-rwxrwxr--  1 amrood   users 1024  Nov 2 00:10  testfile
```

对 testfile 运行上面表格中每个 chmod 示例命令，如下是在 ls -l 之后的，你可以从下面命令中看出权限的改变情况：

```
$ chmod 755 testfile
$ls -l testfile
-rwxr-xr-x  1 amrood   users 1024  Nov 2 00:10  testfile
$chmod 743 testfile
$ls -l testfile
-rwxr---wx  1 amrood   users 1024  Nov 2 00:10  testfile
$chmod 043 testfile
$ls -l testfile
----r---wx  1 amrood   users 1024  Nov 2 00:10  testfile
```

## 改变所有者和所属组

在 UNIX 上创建一个帐户时，系统会给每个用户分配一个所有者 ID 和组 ID。所有上面提到的权限也会基于所有者和组进行分配。

如下的两个命令可以改变一个文件的所有者和组：

1. chown：chown 表示的是 “change owner”，并且它是被用来改变一个文件的所有者。
2. chgrp：chgrp 表示的是 “change group”，并且它是被用来一个文件所属的组。

## 改变所有者关系

chown 命令用来改变一个文件的所有者，它的基本语法如下：

```
$ chown user filelist
```

上面命令中的 user 既可以是系统中的用户名，也可以是系统中用户的 id(uid)。
示例：

```
$ chown amrood testfile
$
```

改变 testfile 文件的所有者为 amrood 用户。

**注意：**超级用户，root 用户，拥有不受限制的权限，能够更改所有文件的所有者，但是普通用户只能修改他们所拥有的文件的所有者。

## 改变组关系

chgrp 命令被用来修改文件所属的组。基本语法如下：

```
$ chgrp group filelist
```

上面命令中的 group 既可以是系统中存在的组的名称，也可以是系统中存在的组的 ID(GID)。

示例：

```
$ chgrp special testfile
$
```

改变给定的文件的组为 special 组。

## SUID 和 SGID 文件权限

通常执行一个命令时，为了完成该任务它必须拥有某些特殊的权限。

举一个例子，当你使用 **passwd** 命令改变了你的密码后，您的新密码存储在文件 `/etc/shadow` 中。

作为一个普通用户，出于安全原因你没有读或写访问这个文件的权限，但是当你改变你的密码时，你需要拥有对这个文件写权限。这意味着 **passwd** 程序必须给你额外的权限，以便您可以编写文件 `/etc/shadow`，也就是需要额外的权限。

通过设置用户 ID(SUID)和组 ID(SGID) 位可以给程序额外的权限。

当您执行一个启用了 SUID 的程序，你继承了程序所有者的权限。启动改程序的用户就可以不用设置 SUID 直接运行该程序。

这对于 SGID 同样是适用的。通常程序是按组的权限进行执行，除非你的组改变了该程序所属组的拥有者。

如果 SUID 和 SGID 权限是可用的，它们将会以小写的 “s” 出现。SUID 的 “s” 位通常位于权限中所有者执行权限的旁边。如下：

```
$ ls -l /usr/bin/passwd
-r-sr-xr-x  1   root   bin  19031 Feb 7 13:47  /usr/bin/passwd*
$
```

上面的显示了 SUID 被设置了并且该命令被 root 用户所拥有。在使用大写字母 S 而不是小写字母表示执行位没有设置。 

如果对一个目录设置了防删除位(sticky bit)，那么只有你是如下任意一种用户时你才可以删除该文件：

- 该目录的拥有者
- 被删除文件的拥有者
- 超级用户，root 用户

你可以使用如下的方式设置任何目录的 SUID 和 SGID 位。 

```
$ chmod ug+s dirname
$ ls -l
drwsr-sr-x 2 root root  4096 Jun 19 06:45 dirname
$
``` 
