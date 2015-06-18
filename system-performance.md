# UNIX 系统性能 #

本教程的目的是介绍一些可用的免费性能分析工具来对 UNIX 系统性能进行监控和管理，并提供了如何分析和解决 UNIX 环境中性能问题的指导。

UNIX 有以下需要进行监控和调整的主要资源类型：

- **CPU**

- **内存**

- **磁盘空间**

- **通信线路**

- **I/O 时间**

- **网络时间**

- **应用程序**


##  性能组件： ##
主要有以下五个组件，随着总系统时间的推移而变化：

<table>
<tr>
<th align="left">组件</th>
<th align="left">描述</th>
</tr>
   <tr>
      <td>用户状态 CPU</td>
      <td>在用户状态下，CPU 运行用户程序的所花费的时间。它包括用于执行库函数调用的时间，但是不包括自己在内核中花费的时间。</td>
   </tr>
   <tr>
      <td>系统状态 CPU</td>
      <td>在系统状态下，CPU 花费在运行程序上的时间。所有的 I/O 例程均需要内核服务。程序员可以通过使用阻塞 I/O 传输来影响这个值。</td>
   <tr>
      <td>I/O 时间和网络时间</td>
      <td>这些是花费在移动数据和 I/O 请求服务的时间</td>
   </tr>
   <tr>
      <td>虚拟内存的性能</td>
      <td>这包括了上下文的切换和交换。</td>
   </tr>
   <tr>
      <td>应用程序</td>
      <td>花费在运行其他程序的时间--系统没有为这个应用程序提供服务是因为另一个应用程序在当前状态下持有 CPU。</td>
   </tr>
</table>
	
## 性能工具： ##
UNIX 提供了以下重要工具来估量和调整 UNIX 系统的性能：

<table>
<tr>
<th align="left">命令</th>
<th align="left">描述</th>
</tr>
   <tr>
      <td>nice/renice</td>
      <td>修改运行程序的调度优先级。</td>
   </tr>
   <tr>
      <td>netstat</td>
      <td>打印网络连接，路由表，接口状态，无效连接和多播成员。</td>
   <tr>
      <td>time</td>
      <td>测量一个普通命令的运行时间或资源的使用情况。</td>
   </tr>
   <tr>
      <td>uptime</td>
      <td>系统平均负载。</td>
   </tr>
   <tr>
      <td>ps</td>
      <td>显示当前进程的快照。</td>
   </tr>
   <tr>
      <td>vmstat</td>
      <td>显示虚拟内存信息的统计。</td>
   </tr>
   <tr>
      <td>gprof</td>
      <td>显示调用关系图资料。</td>
   </tr>
   <tr>
      <td>prof</td>
      <td>进程性能分析。</td>
   </tr>
   <tr>
      <td>top</td>
      <td>显示系统的任务。</td>
   </tr>
</table>
