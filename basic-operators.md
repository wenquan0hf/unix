## Unix shell 基本操作符

每一种 shell 都支持各种各样的操作符。我们的教程基于默认的 shell(Bourne)，所以在我们的教程中涵盖所有重要的 Bourne shell 操作符。

下面列出我们将讨论的操作符：

- 算术运算符。
- 关系运算符。
- 布尔操作符。
- 字符串运算符。
- 文件测试操作符。

最初的 Bourne shell 没有任何机制来执行简单算术运算，它使用外部程序 **awk** 或者最简单的程序 **expr**。

下面我们用一个简单的例子说明，两个数字相加：

    #!/bin/sh
    
    val=`expr 2 + 2`
    echo "Total value : $val"

这将产生以下结果：

    Total value : 4

注意以下事项：

- 操作符和表达式之间必须有空格，例如 2+2 是不正确的，这里应该写成 2 + 2。
- 完整的表达应该封闭在两个单引号 '' 之间。

### 算术运算符:

下面列出 Bourne Shell 支持的算术运算符。

假设变量 a 赋值为 10，变量 b 赋值为 20：

[示例说明](http://www.tutorialspoint.com/unix/unix-arithmetic-operators.htm)
<table>
<tr>
<th>运算符</th>
<th>描述</th>
<th>例子</th>
</tr>
<tr>
<td>+</td>
<td>加法 - 将操作符两边的数加起来</td>
<td>`expr $a + $b` will give 30</td>
</tr>
<tr>
<td>-</td>
<td>减法 - 用操作符左边的操作数减去右边的操作数</td>
<td>`expr $a - $b` will give -10</td>
</tr>
<tr>
<td>*</td>
<td>乘法 - 将操作符两边的数乘起来</td>
<td>`expr $a \* $b` will give 200</td>
</tr>
<tr>
<td>/</td>
<td>除法 - 用操作符左边的操作数除以右边的操作数</td>
<td>`expr $b / $a` will give 2</td>
</tr>
<tr>
<td>%</td>
<td>取模 - 用操作符左边的操作数除以右边的操作数，返回余数</td>
<td>`expr $b % $a` will give 0</td>
</tr>
<tr>
<td>=</td>
<td>赋值 - 将操作符右边的操作数赋值给左边的操作数</td>
<td>a=$b would assign value of b into a</td>
</tr>
<tr>
<td>==</td>
<td>相等 - 比较两个数字，如果相同，返回true</td>
<td>[ $a == $b ] would return false.</td>
</tr>
<tr>
<td>!=</td>
<td>不相等 - 比较两个数字，如果不同，返回true。</td>
<td>[ $a != $b ] would return true.</td>
</tr>
</table>

这里需要非常注意是，所有的条件表达式和操作符之间都必须用空格隔开，例如 [$a == $b] 是正确的,而 [$a==$b] 是不正确的。

所有的算术计算都是针对长整数操作的。

### 关系运算符:

Bourne Shell 支持以下的关系运算符，这些运算符是专门针对数值数据的。它们不会对字符串值起作用，除非他们的值是数值数据。

例如，下面的操作符将检查 10 和 20 之间的关系以及 “10” 和 “20”的关系，但不能用于判断 “ten” 和 “twenty” 的关系。

假设变量 a 赋值为 10， 变量 b 赋值为 20：

[示例说明](http://www.tutorialspoint.com/unix/unix-relational-operators.htm)
<table>
<tr>
<th>运算符</th>
<th>描述</th>
<th>例子</th>
</tr>
<tr>
<td>-eq</td>
<td>检查两个操作数的值是否相等，如果值相等，那么条件为真。</td>
<td>[ $a -eq $b ] is not true. </td>
</tr>
<tr>
<td>-ne</td>
<td>检查两个操作数的值是否相等，如果值不相等，那么条件为真。</td>
<td>[ $a -ne $b ] is true. </td>
</tr>
<tr>
<td>-gt</td>
<td>检查左操作数的值是否大于右操作数的值，如果是的，那么条件为真。</td>
<td>[ $a -gt $b ] is not true. </td>
</tr>
<tr>
<td>-lt</td>
<td>检查左操作数的值是否小于右操作数的值，如果是的，那么条件为真。</td>
<td>[ $a -lt $b ] is true.</td>
</tr>
<tr>
<td>-ge</td>
<td>检查左操作数的值是否大于等于右操作数的值，如果是的，那么条件为真。</td>
<td>[ $a -ge $b ] is not true. </td>
</tr>
<tr>
<td>-le</td>
<td>检查左操作数的值是否小于等于右操作数的值，如果是的，那么条件为真。</td>
<td>[ $a -le $b ] is true. </td>
</tr>
</table>

这里需要非常注意是，所有的条件表达式和操作符之间都必须用空格隔开，例如 [$a <= $b] 是正确的，而 [$a<=$b] 是不正确的。

### 布尔操作符:

Bourne Shell 支持以下的布尔操作符。

假设变量 a 赋值为 10， 变量 b 赋值为 20：

[示例说明](http://www.tutorialspoint.com/unix/unix-boolean-operators.htm)
<table>
<tr>
<th>运算符</th>
<th>描述</th>
<th>例子</th>
</tr>
<tr>
<td>!</td>
<td>这表示逻辑否定。如果条件为假，返回真，反之亦然。</td>
<td>[ ! false ] is true. </td>
</tr>
<tr>
<td>-o</td>
<td>这表示逻辑 OR。如果操作对象中有一个为真，那么条件将会是真。</td>
<td>[ $a -lt 20 -o $b -gt 100 ] is true. </td>
</tr>
<tr>
<td>-a</td>
<td>这表示逻辑 AND。如果两个操作对象都是真，那么条件才会为真，否则为假。</td>
<td>[ $a -lt 20 -a $b -gt 100 ] is false. </td>
</tr>
</table>

### 字符串运算符:

Bourne Shell 支持以下字符串运算符。

假设变量 a 赋值为 "abc"， 变量 b 赋值为 "efg"：

[示例说明](http://www.tutorialspoint.com/unix/unix-string-operators.htm)

<table>
<tr>
<th>运算符</th>
<th>描述</th>
<th>例子</th>
</tr>
<tr>
<td>=</td>
<td>检查两个操作数的值是否相等，如果是的，那么条件为真。</td>
<td>[ $a = $b ] is not true. </td>
</tr>
<tr>
<td>!=</td>
<td>检查两个操作数的值是否相等，如果值不相等，那么条件为真。</td>
<td>[ $a != $b ] is true. </td>
</tr>
<tr>
<td>-z</td>
<td>检查给定字符串操作数的长度是否为零。如果长度为零，则返回true。</td>
<td>[ -z $a ] is not true. </td>
</tr>
<tr>
<td>-n</td>
<td>检查给定字符串操作数的长度是否不为零。如果长度不为零，则返回true。</td>
<td>[ -z $a ] is not false. </td>
</tr>
<tr>
<td>str</td>
<td>检查字符串str是否是非空字符串。如果它为空字符串，则返回false。</td>
<td>[ $a ] is not false.</td>
</tr>
</table>

### 文件测试操作符:

下列操作符用来测试与Unix文件相关联的各种属性。

假设一个文件变量 file，包含一个文件名 "test"，文件大小是100字节，在其上有读、写和执行权限：

[示例说明](http://www.tutorialspoint.com/unix/unix-file-operators.htm)
<table>
<tr>
<th>运算符</th>
<th>描述</th>
<th>例子</th>
</tr>
<tr>
<td>-b file</td>
<td>检查文件是否为块特殊文件，如果是，那么条件为真。</td>
<td>[ -b $file ] is false. </td>
</tr>
<tr>
<td>-c file</td>
<td>检查文件是否为字符特殊文件，如果是，那么条件变为真。</td>
<td>[ -c $file ] is false. </td>
</tr>
<tr>
<td>-d file</td>
<td>检查文件是否是一个目录文件，如果是，那么条件为真。</td>
<td>[ -d $file ] is not true. </td>
</tr>
<tr>
<td>-f file</td>
<td>检查文件是否是一个不同于目录文件和特殊文件的普通文件，如果是，那么条件为真。</td>
<td>[ -f $file ] is true. </td>
</tr>
<tr>
<td>-g file</td>
<td>检查文件是否有组ID(SGID)设置，如果是，那么条件为真。</td>
<td>[ -g $file ] is false. </td>
</tr>
<tr>
<td>-k file</td>
<td>检查文件是否有粘贴位设置，如果是，那么条件为真。</td>
<td>[ -k $file ] is false. </td>
</tr>
<tr>
<td>-p file</td>
<td>检查文件是否是一个命名管道，如果是，那么条件为真。</td>
<td>[ -p $file ] is false. </td>
</tr>
<tr>
<td>-t file</td>
<td>检查文件描述符是否可用且与终端相关，如果是，条件为真实。</td>
<td>[ -t $file ] is false. </td>
</tr>
<tr>
<td>-u file</td>
<td>检查文件是否有用户id(SUID)设置，如果是，那么条件为真。</td>
<td>[ -u $file ] is false. </td>
</tr>
<tr>
<td>-r file</td>
<td>检查文件是否可读，如果是，那么条件为真。</td>
<td>[ -r $file ] is true. </td>
</tr>
<tr>
<td>-w file</td>
<td>检查文件是否可写，如果是，那么条件为真。</td>
<td>[ -w $file ] is true. </td>
</tr>
<tr>
<td>-x file</td>
<td>检查文件是否可执行，如果是，那么条件为真。</td>
<td>[ -x $file ] is true. </td>
</tr>
<tr>
<td>-s file</td>
<td>检查文件大小是否大于0，如果是，那么条件为真。</td>
<td>[ -s $file ] is true. </td>
</tr>
<tr>
<td>-e file</td>
<td>检查文件是否存在。即使文件是一个目录目录，只有存在，条件就为真。</td>
<td>[ -e $file ] is true. </td>
</tr>
</table>

### C Shell操作符:

下面的链接给出了关于 C Shell 操作符的简单介绍。

[C Shell操作符](http://www.tutorialspoint.com/unix/unix-c-shell-operators.htm)

### Korn Shell操作符:

下面的链接给出了关于 Korn Shell 操作符的简单介绍。

[Korn Shell操作符](http://www.tutorialspoint.com/unix/unix-korn-shell-operators.htm)
