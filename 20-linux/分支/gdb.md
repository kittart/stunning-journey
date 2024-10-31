先写一个.c文件
![[file-20240909120707890.png|500]]
![[file-20240909120915616.png|500]]
1.**启动gdb**
编译时需添加-g 选项  否则生成目标文件缺失调试信息
     gcc -g -c 1.c   --> gcc 1.o -o 1.exe
     gcc -g 1.c -o 1.exe (编译链接一同操作)
     gcc -g 1.c （默认生成a.out执行文件）
     三种方式任选一种皆可
启动命令如下：
     gdb 1.exe
     gdb -q 1.exe (不打印gdb版本信息，界面比较干净)
gdb 文件名 ：进入调试
q ：退出gdb
l 行号：显示binFile源代码，接着上次的位置往下列，每次列10行。
l 函数名：列出某个函数的源代码。
r ：运行程序
b 行号：在某一行设置断点
b 函数名：在某个函数开头设置断点
info b ：查看所有信息。
d break：删除所有断点
d 断点编号 ：删除序号为n的断点
disable breakpoints 断点编号：禁用断点
enable breakpoints 断点编号：启用断点

```
(gdb) print &n
$1 = (int *) 0x7fffffffe38c   # 假设地址为 0x7fffffffe38c
(gdb) print &result
$2 = (int *) 0x7fffffffe388   # 假设地址为 0x7fffffffe388
(gdb) x/1dw 0x7fffffffe38c
0x7fffffffe38c: 5
(gdb) x/1xw 0x7fffffffe388
0x7fffffffe388: 0x00000014
(gdb) x/2xw 0x7fffffffe388
0x7fffffffe388: 0x00000014  0x00000005

```
### core
core文件就是核心转储文件，显示核心已转储就生成core文件
![[file-20240910111030039.png]]
