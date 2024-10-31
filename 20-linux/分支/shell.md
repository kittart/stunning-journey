[Shell编程基础篇-上 - 惨绿少年 - 博客园 (cnblogs.com)](https://www.cnblogs.com/clsn/p/7992981.html#auto-id-25)
[Shell编程基础篇-下 - 惨绿少年 - 博客园 (cnblogs.com)](https://www.cnblogs.com/clsn/p/8006210.html)
https://www.cnblogs.com/clsn/p/7992981.html#auto-id-25

#### 1.1什么是shell？
shell官方的介绍：shell通过提示您输入，给操作系统解释该输入，然后处理来自操作系统的任何结果输出，**shell可以看成是一个命令解释器**，**是用户跟操作系统之间的解释器**
##### 1.1.1常见的shell 有哪些
	Bourne Shell（/usr/bin/sh或/bin/sh）
	Bourne Again Shell（/bin/bash）
	C Shell（/usr/bin/csh）
	K Shell（/usr/bin/ksh）
	Shell for Root（/sbin/sh）
 最常用的 shell 是Bash，也就是 Bourne Again Shell。Bash由于易用和免费，在日常工作中被广泛使用，也是大多数Linux操作系统默认的Shell环境。
##### 1.1.2 shell编程注意事项
- shell命名：shell脚本一般名称为英文，大写，小写，后缀以sh结尾
- 不可以使用特殊符号以及空格
- shell编程，首行必须以 bin/bash 开头
- shell 脚本 变量首个字符必须为字母（a-z，A-Z）不能以数字，特殊字符开头，使用下划线但不能用破折号
#### 1.2常见的3种变量
Shell编程中变量分为三种，分别是系统变量、环境变量和用户变量
#### 1.3环境变量
当前shell运行时保存的信息，包括终端类型，当前目录，主目录，语言编码，默认命令搜索路径等信息。**运行 ==env== 命令可以查看当前环境变量**
==set== 查找所有的变量 set|grep a=12
⭕ **环境变量是一个名称和值的对应列表**。一种是shell启动时解析配置文件生成，还有一种临时的环境变量是在shell中使用export生成
###### 1.3.1常用的环境变量
PATH  		记录命令所示路径，以冒号为分割；
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/us
==HOME==  		打印用户家目录，只跟用户有关
==SHELL== 		显示当前Shell类型；
==USER==  		打印当前用户名，==切换用户会变==
ID    		打印当前用户id信息；
==PWD==   		显示当前所在家目录，==切换用户会变==
TERM  		打印当前终端类型；
HOSTNAME    显示当前主机名；
PS1         定义主机命令提示符的；
HISTSIZE    历史命令大小，可通过 HISTTIMEFORMAT 变量设置命令执行时间;
RANDOM      随机生成一个 0 至 32767 的整数;
HOSTNAME    主机名
![[d66469562f6d4798ba89a167bf56fc5.png]]

###### 1.3.2 声明临时环境变量
export a = 1 
切换用户或退出就不在了 ^024bd7
###### 1.3.3删除变量
unset a 删除变量
###### 1.3.4 查看环境变量
- echo 查看变量的值，用$取值使用-echo $PWD，而echo PWD仅仅是输出PWD字符串
	写成 ${a}, $指的是提取变量的值
- ==set== 查找所有的变量 set|grep a=12
##### 🔸通配符

| 通配符     |                                                       |
| ------- | ----------------------------------------------------- |
| **''**  | 单引号，原样输出                                              |
| **""**  | 弱引用，具有==变量置换，界定功能==,**有一些特殊字符在里面也生效，就像下面四个🚨**        |
| ==$==   | 取值符号                                                  |
| ==\==   | 转义字符                                                  |
| ==``==  | 返单引号，直接优先执行其中的内容，在""中生效                               |
| ==$()== | 在使用反引号或 `$()` 时，建议使用双引号包裹整个表达式，以避免输出中包含的空格或换行符导致的意外行为 |
|         |                                                       |
- 单双引号的大致作用
![[Pasted image 20240827103735.png|200]]
- 返单引号：
![[Pasted image 20240827232604.png|200]]
#### 🔸1.4读取用户输入的
标准输入情况
```c
read -p  'uaername:' user_var
echo "username : $suer_var"
```
🔴希望**输入隐藏**，如果是密码，不希望显示在外面，**就用s和p标志位**
```c
read -p 'username :' user_var
read-sp 'password :' pass_var
echo "username : $user_var"
echo "password : $pass_var"
```
🔴输入多个输入的时候,**用${ }**
```c
echo "Ecter names :"
read -a names //-a 告诉脚本正确地读取数组，names就像数组
echo"Names:${name[0],${name[1]}}"
```
🔴read 后面不加变量
在read命令之后，input进入一个名为reply的内置变量，所以即使read后面没有变量，也可以用￥REPLY
```c
echo "Enter name :"
read
echo "name : $REPLY"
```
#### 1.5参数传递
```c
echo $1 $2 $3 '> echo $1 $2 $3'
```

#### 🔸1.6数字运算
shell里面默认都是字符吗，所以要用整数运算符，里面是表达式，不用管格式
- `$[]` 
- `$(())`  双括号表达式运算速度更快
![[Pasted image 20240827232236.png|200]]
==expr== ：处理字符的时候来用expr ，因为是处理字符，所以要加空格，对于数字和运算符要用转义字符来运算，需要有`$`才能识别数字
![[Pasted image 20240827110337.png|200]]
==let== ：看见let的时候就要开始计算，所以可以不用`$`，运算表达式**必须有一个值来接受它** ，**操作符和表达式之间不允许有空格**

#### 🔸浮点数运算 bc
- **scale是你想要的小数个数**
- echo "20+5"|bc 可以和管道符来一起使用
- bc<<EOF 还可以用重定向来 << 
![[Pasted image 20240827232448.png|200]]

read var
read -p "请输入："  


### 1.7练习写脚本🚨
> #!/bin/bash
> `#`写注释，因为别人要调用，所以要写详细，以及各种情况说明
> echo 'abc'
> exit 0 //表示脚本执行完了，就退出，可以不写
练习：
![[Pasted image 20240827113122.png|400]]
![[Pasted image 20240827113625.png|400]]
>1.创建脚本，更改可执行权限--变成绿色就说明成功
>2.用vim编辑脚本
>3.`./scriptTask.sh` 用于在当前目录下执行名为 `scriptTask.sh` 的 Shell 脚本，**需要确保脚本文件有执行权限**
>脚本写：
```shell
 #!/bin/bash
  2
  3 a=20
  4 b=5
  5
  6 echo $((a + b))
  7 echo $((a - b))
  8 echo $((a * b))
  9 echo $((a / b))
 10
 11 echo $(expr $a + $b)
 12 echo $(expr $a - $b)
 13 echo $(expr $a \* $b)
 14 echo $(expr $a / $b)
 15
 16 echo "20+5"|bc
 17 echo "$a+$b" | bc
 18 let a++
 19 bc<<EOF
 20 scale=2
 21 a/b
 22 quit
 23 EOF
 24
 25 echo "scale=2;20/5"|bc
 26 echo "scale=2;sqrt($a)" | bc -l
 27
 28 result=`ls`
 29 echo "$result"
 30
 31 result=$(ls)
 32 echo "$result"
 33
 34 exit 0
```
运行得到
```shell
fufu@fufu-virtual-machine:~/a$ ./scriptTask.sh
25
15
100
4
25
15
100
4
25
25
Runtime error (func=(main), adr=5): Divide by zero
4.00
4.58
\
hello
hello.c
scriptTask.sh
test_0.txt
test_1.txt
\
hello
hello.c
scriptTask.sh
test_0.txt
test_1.txt
```

### 1.8变量相关
**下标从0开始**
> `echo "${a}"|wc -L
> `echo ${#a}
> `echo ${a:3} `从下标为3的地方开始截取
> `echo ${a:0-3} `从最后一个开始，往左截取3个
> `echo ${a:0-3：2}`
> `echo ${a:3:2}` 从下标为3的地方截取2个
> `echo ${a:3：-3}`用于从字符串`a`中，从索引`3`开始提取，直到末尾减去`3`个字符的子串
> expr ：处理字符的时候来用expr ，因为是处理字符，所以要加空格，对于数字和运算符要用转义字符来运算，需要有`$`才能识别数字
> expr substr "${a}" 2 3
> expr index "${a}" 'c' 在里面找c
#### 1.8.1替换
改变命令显示的结果，不改变原值
b='a1212aby'
echo ${b//a/uu} 得到：uu1212uuby
echo ${b/12/w} 得到： aw12aby
#### 替换小结

> [!important]
> 一个“/”表示替换匹配的第-个字符串。
> 两个“/”表示替换匹配的所有字符串

#### 匹配删除小结

> [!important]
> `#`表示从开头删除匹配最短。
> `##`表示从开头删除匹配最长。
> `%`表示从结尾删除匹配最短。
> `%%`表示从结尾删除匹配最长。
> `a*c`表示匹配的突符串，`*`表示匹配所有，`a*c`匹配开头为a、中间为任意多个字符、结尾为c的字符串。
> `a*C`表示匹配的字符串，`*`表示匹配所有，`a*C`匹配开头为a、中间为任意多个字符、结尾为C的字符串。

```
total_size() { 
# 使用 du 命令统计目录大小（以字节为单位） 
output=$(du -b "$watch") 
# 提取大小值：使用 Bash 字符串处理来去除目录路径 
size=${output%%$watch*} 
echo "$size" }
```
### 截取-分隔符
在字符串里面，任何一个字符都可以做分隔符
```
c='/home/xm/test/a.txt'
`echo ${c%%*/}
`echo ${c##*/}`- 斜杠为分隔符--从左往右
`echo ${c%%*/}` 从右往左找删除
`echo ${c%/*}` 用于去掉字符串中最后一次出现的`/`及其右边的所有内容
`echo ${c#*t}`
```
![[Pasted image 20240828102053.png|300]]
### 校验
a='abc'
b=''
- 如果变量非空且已定义，则返回 "hello"，如果变量为空或未定义，则返回空字符串（不输出内容）
echo ${a:+hello} --hello
echo ${b:+hello} -- NULL空
-  如果这个变量为空或者不存在，就返回hello，如果有值就返回abc
echo ${a:-hello} --abc
echo ${b:-hello} --hello
- 如果变量有值，就返回本身，如果为空，就输出标准错误
echo ${a:？hello} --abc
echo ${b:？hello} --error
- 如果变量有值，就返回变量本身，如果变量不存在或者为NULL，就返回赋值结果
echo ${a:=hello} --abc
echo ${b:=hello} --hello b='hello'
![[Pasted image 20240829083513.png]]
### 静态变量
readonly a=12 unset删除它

### test命令
1）**判断表达式**
if test (表达式为真)
if test !表达式为假
test 表达式1 –a 表达式2 两个表达式都为真
test 表达式1 –o 表达式2 两个表达式有一个为真
2）**判断字符串**
test –n 字符串 字符串的长度非零
test –z 字符串 字符串的长度为零
test 字符串1＝字符串2 字符串相等
test 字符串1！＝字符串2 字符串不等
3）**判断整数**
test 整数1 –eq 整数2 整数相等
test 整数1 –ge 整数2 整数1大于等于整数2
test 整数1 –gt 整数2 整数1大于整数2
test 整数1 –le 整数2 整数1小于等于整数2
test 整数1 –lt 整数2 整数1小于整数2
test 整数1 –ne 整数2 整数1不等于整数2
4）**判断文件**
test File1 –ef File2 两个文件具有同样的设备号和i结点号
test File1 –nt File2 文件1比文件2 新
test File1 –ot File2 文件1比文件2 旧
test –b File 文件存在并且是块设备文件
test –c File 文件存在并且是字符设备文件
test –d File 文件存在并且是目录
test –e File 文件存在
test –f File 文件存在并且是正规文件
test –g File 文件存在并且是设置了组ID
test –G File 文件存在并且属于有效组ID
test –h File 文件存在并且是一个符号链接（同-L）
test –k File 文件存在并且设置了sticky位
test –b File 文件存在并且是块设备文件
test –L File 文件存在并且是一个符号链接（同-h）
test –o File 文件存在并且属于有效用户ID
test –p File 文件存在并且是一个命名管道
test –r File 文件存在并且可读
test –s File 文件存在并且是一个套接字
test –t FD 文件描述符是在一个终端打开的
test –u File 文件存在并且设置了它的set-user-id位
test –w File 文件存在并且可写
test –x File 文件存在并且可执行

