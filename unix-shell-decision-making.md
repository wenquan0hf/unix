## Unix Shell决策

编写 shell 脚本时，可能存在一种情况，你需要在两条路径中选择一条路径。所以你需要使用条件语句，确保你的程序做出正确的决策并执行正确的操作。

Unix Shell 支持条件语句，这些语句基于不同的条件，用于执行不同的操作。在这里，我们将介绍以下两个决策语句：

- **if……else**语句
- **case…… esac**语句

### if……else 语句：

if……else 语句是非常有用的决策语句，它可以用来从一个给定的选项集中选择一个选项。

Unix Shell 支持以下形式的 if……else 的语句：

- [if...fi statement](http://www.tutorialspoint.com/unix/if-fi-statement.htm)
- [if...else...fi statement](http://www.tutorialspoint.com/unix/if-else-statement.htm)
- [if...elif...else...fi statement](http://www.tutorialspoint.com/unix/if-elif-statement.htm)


大部分的 if 语句使用关系运算符检查关系，这部分知识在前一章已经讨论过。

### case…… esac语句:

你可以使用多个 if……elif 语句执行一个多路分支。然而，这并不总是最好的解决方案，特别是当所有的分支都依赖于一个单一变量的值。

Unix Shell 支持 **case……esac** 语句，可以更确切地处理这种情况，它比重复 if……elif 语句更加有效。

 case...esac 语句只有一种形式，详细说明如下：

- [case...esac statement](http://www.tutorialspoint.com/unix/case-esac-statement.htm)

Unix Shell的 case……esac 语句非常类似于 switch……case 语句，switch……case 语句在其他编程语言如 C 或 C++ 和 PERL 等中实现。