## Unix 用户管理

在 Unix 系统中，有三种类型的账户：

1. **root 帐户**：这也被称为超级用户，这类用户对系统拥有完整的和不受约束的控制权。超级用户可以运行任何命令，而不受任何限制。这类用户应该承担作为一个系统管理员的任务。
1. **系统账户**：系统账户是为操作系统特定组件的需要提供的，例如邮件账户和 sshd 账户。这些账户通常是为了满足系统上一些特定的功能的需要而设定的，对它们进行的任何修改都可能会对系统造成负面影响。
1. **用户帐号**：用户帐户提供交互式访问系统的用户和用户组。通常给普通用户分配这些账户，通常附带有对关键系统文件和目录有限的访问权限。

Unix 支持组帐号（Group Account）的概念，在逻辑上是许多账户的群组。每个帐户都可能是任何组账号的一部分。Unix 组在处理文件权限和流程管理中发挥了重要的作用。

### 管理用户和组：

下面列出三个主要的用户管理文件：

1. **/etc/passwd**：此文件保存用户帐户和密码信息。这个文件包含了 Unix 系统上大多数的账户信息。
1. **/etc/shadow**：此文件包含相应帐户的加密密码。不是所有的系统都支持这个文件。
1. **/etc/group**：此文件包含每个帐户的组信息。
1. **/etc/gshadow**：此文件包含安全组帐号信息。

使用 **cat** 命令检查上述所有文件。

大多数 Unix 系统可用以下命令来创建和管理帐户和组:

<table>
<tr>
<th>命令</th>
<th>描述</th>
</tr>
<tr>
<td>useradd</td>
<td>将账户添加到系统。</td>
</tr>
<tr>
<td>usermod</td>
<td>修改账户属性。</td>
</tr>
<tr>
<td>userdel</td>
<td>从系统删除账户。</td>
</tr>
<tr>
<td>groupadd</td>
<td>将组添加到系统。</td>
</tr>
<tr>
<td>groupmod</td>
<td>修改组属性。</td>
</tr>
<tr>
<td>groupdel</td>
<td>从系统中删除组。</td>
</tr>
</table>

可以使用 [Manpage Help](http://www.tutorialspoint.com/unix/unix-manpage-help.htm) 查看这里提到每个命令的完整语法。

### 创建一个组

在创建任何账户之前需要先创建组，否则将不得不使用系统中现有的组。你会在 /etc/groups 文件中找到所有组的列表。

所有默认组都是系统帐户组成的特定组，不推荐普通账户使用。所以下面给出用来创建一个新组帐户的语法:

     groupadd [-g gid [-o]] [-r] [-f] groupname

下面列出详细的参数:
<table>
<tr>
<th>选项</th>
<th>描述</th>
</tr>
<tr>
<td>-g GID</td>
<td>组 ID 的数值。</td>
</tr>
<tr>
<td>-o</td>
<td>这个选项允许给组添加一个非唯一的 GID。</td>
</tr>
<tr>
<td>-r</td>
<td>这个标志表示给组添加一个系统账户。</td>
</tr>
<tr>
<td>-f</td>
<td>如果指定的组已经存在，这个选项会导致成功退出。附带 -g 时，如果指定 GID 已经存在，就选择其他(独特的) GID。</td>
</tr>
<tr>
<td>groupname</td>
<td>创建一个真实的组名称。</td>
</tr>
</table>

如果你没有指定任何参数，那么系统将使用默认值。

以下示例将使用默认值创建开发人员组，这为大部分的管理员接受。

    $ groupadd developers

### 修改组：

修改一个组,使用 **groupmod** 语法：

    $ groupmod -n new_modified_group_name old_group_name

将 developers_2 组的名称改为 developer，例如：

    $ groupmod -n developer developer_2

下边描述如何将developer的 GID 更改为 545：

    $ groupmod -g 545 developer

### 删除一个组：

删除现有的组，需要的所有东西就是 groupdel 命令和组名。例如删除 developer 组，命令是：

    $ groupdel developer

这个操作只是删除了组，而不涉及任何跟组相关的文件。这些文件仍然可以被它们的主人访问。

### 创建一个帐户

让我们看看如何在 Unix 系统上创建一个新的帐户。下面是用来创建一个用户帐户的语法：

    useradd -d homedir -g groupname -m -s shell -u userid accountname

下面列出详细的参数:

<table>
<tr>
<th>选项</th>
<th>描述</th>
</tr>
<tr>
<td>-d homedir</td>
<td>指定账户的主目录。</td>
</tr>
<tr>
<td>-g groupname</td>
<td>指定该账户所属的组账户。</td>
</tr>
<tr>
<td>-m</td>
<td>如果它不存在，则创建主目录。</td>
</tr>
<tr>
<td>-s shell</td>
<td>指定该帐户的默认 shell。</td>
</tr>
<tr>
<td>-u userid</td>
<td>您可以为账户指定一个用户id。</td>
</tr>
<tr>
<td>accountname</td>
<td>创建一个真实的帐户名称</td>
</tr>
</table>

如果你没有指定任何参数，那么系统将使用默认值。useradd 命令将修改 /etc/passwd 文件、/etc/shadow 文件、/etc/group 文件并创建一个主目录。

下面的示例将创建一个帐户：mcmohd，主目录设置为 /home/mcmohd，组为 developers。将 Korn Shell 分配给这个用户。

    $ useradd -d /home/mcmohd -g developers -s /bin/ksh mcmohd

上面的命令执行之前，必须确保你已经使用 groupadd 命令创建了 developers 组。

创建一个帐户之后，你可以使用 passwd 命令设置它的密码，如下所示：

    $ passwd mcmohd20
    Changing password for user mcmohd20.
    New UNIX password:
    Retype new UNIX password:
    passwd: all authentication tokens updated successfully.

当您输入 passwd 账户名，它会假定你是超级用户，从而更改密码。否则你只能使用这样的命令改变你的密码，而不能更改指定帐户的密码。

### 修改一个账户:

**usermod** 命令允许从命令行更改现有的账户。它使用和 useradd 命令相同的参数，加上 -l 参数，允许更改帐户名称。

例如，将账户名称 mcmohd 更改为 mcmohd20 并相应地改变主目录，需要执行以下命令：

    $ usermod -d /home/mcmohd20 -m -l mcmohd mcmohd20

### 删除一个账户:

**userdel** 命令可以用来删除现有的用户。这是一个非常危险的命令，必须小心使用。

这个命令只有一个参数或可用的选项：.r，用来删除帐户的主目录和邮件文件。

例如，删除帐户mcmohd20，需要发出以下命令：

    $ userdel -r mcmohd20

如果为了备份的目的，想保留它的主目录，省略 -r 选项。可以根据需要在稍后的时间删除主目录。