# 循环

循环是一个强大的编程工具，可以使您能够重复执行一系列命令。针对 Shell 程序员，有 4 种循环类型：

- while 循环
- for 循环
- until 循环
- select 循环

根据不同的情况使用不同的循环。例如只要给定条件仍然是 true，while 循环将执行给定的命令。而 until 循环是直到给定的条件变成 true，才会执行。

一旦你有了良好的编程实践，你就会开始根据情况使用适当的循环。while 循环和 for 循环在大多数其他编程语言如 C、C++ 和 PERL 等中都有实现。

## 嵌套循环

所有的循环都支持嵌套的概念，这意味着可以将一个循环放到另一个相似或不同的循环中。这个嵌套可以根据您的需求高达无限次。

下面是一个嵌套 while 循环的例子，基于编程的要求，其他循环类型也可以以类似的方式嵌套：

## 嵌套 while 循环

可以使用 while 循环作为另一个 while 循环体的一部分。

## 语法

```
    while command1 ; # this is loop1, the outer loop
    do
       Statement(s) to be executed if command1 is true
    
       while command2 ; # this is loop2, the inner loop
       do
      Statement(s) to be executed if command2 is true
       done
    
       Statement(s) to be executed if command1 is true
    done
```

## 例子

下面是循环嵌套的一个简单例子，在循环内部添加另一个倒计时循环，用来数到九：

```
    #!/bin/sh
    
    a=0
    while [ "$a" -lt 10 ]# this is loop1
    do
       b="$a"
       while [ "$b" -ge 0 ]  # this is loop2
       do
      echo -n "$b "
      b=`expr $b - 1`
       done
       echo
       a=`expr $a + 1`
    done
```

这将产生以下结果。重要的是要注意 **echo -n** 是如何工作的。这里 `-n` 选项让输出避免了打印新行字符。

```
    0
    1 0
    2 1 0
    3 2 1 0
    4 3 2 1 0
    5 4 3 2 1 0
    6 5 4 3 2 1 0
    7 6 5 4 3 2 1 0
    8 7 6 5 4 3 2 1 0
    9 8 7 6 5 4 3 2 1 0
```