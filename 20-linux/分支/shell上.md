### 1. 条件表达式
#### 1.1 文件判断
常用的操作测试符
![[Pasted image 20240829084626.png]]
**判断文件是否存在**
>fufu@fufu-virtual-machine:~$ [ -f /etc/hosts ]
>fufu@fufu-virtual-machine:~$ echo $?
>0

**判断文件是否存在**+返回方式
>[ -f /etc/hosts ] && echo "文件存在" || echo "文件不存在"

**判断目录是否存在**
>[ -d /tmp ] && echo "目录存在" || echo "目录不存在"

![[Pasted image 20240829085400.png]]
#### 1.2 字符串判断
字符串测试操作符
![[Pasted image 20240829085517.png]]
**-z 判断字符串长度**
>x=  ; [ -z "$x" ] && echo "输入为空" || echo '输入有内容'

**-n判断字符串长度**
>x=12 ; [ -n "$x" ] && echo "输入有内容" || echo '输入为空'

**定义变量的方式进行判断**
>cmd=start;[ "$cmd" == "start" ] && echo start
#### 1.3 整数判断符

| []和 test | (())和`[[]]` |      |
| -------- | ----------- | ---- |
| -eq      | ==或=        | 相等   |
| -ne      | ！=          | 不相等  |
| -gt      | >           | 大于   |
| -ge      | >=          | 大于等于 |
| -lt      | <           | 小于   |
| -le      | <=          | 小于等于 |

#### 1.4 逻辑操作符

| []和tset |                           | 说明   | [[]]   | 说明  |
| ------- | ------------------------- | ---- | ------ | --- |
| -a      | `[条件a -a 条件b]` ab都成立才成立   | &&   | 与，都真为真 |     |
| -o      | `[条件a -o 条件b]` ab不成立，才不成立 | \|\| | 或，一真为真 |     |
| ！       |                           | ！    | 两端相反为真 |     |

_**逻辑操作符与整数判断配合**_
>`# [ 11 -ne 1 ] && echo "成立" || echo "不成立"`
>成立

 **_取反_**
>`# [ ! 11 -ne 1 ] && echo "成立" || echo "不成立"`
>不成立

**_两边都为真_**
>`# [  11 -ne 1 -a 1 -eq 1 ] && echo "成立" || echo "不成立"`
>成立

**_至少有一边为真_**
>`# [  11 -ne 1 -o 1 -eq 1 ] && echo "成立" || echo "不成立"`
>成立

**感叹号的特殊用法**
_使用历史命令,__感叹号加上history__中的序号,__即可执行_
>`#  !516`
 ls
 anaconda-ks.cfg  bootime.avg  setup.sh  vim

### **2** if语句
1.单分支
**条件两边要空格**
> if [ 条件 ];
> then
> ... 如果没有语句写，就写个：
> else
> ...
> fi 

2.多分支
> if[ tiaojian ];then
> ...
> elif[ tiaojian ];then
> ...
> else
> ...
> fi


#### 2.1练习题
![[f0cd5ed0457c13b9dbfcf211724744d.png]]

#### 2.2 if练习
例1，判断文件是不是脚本文件--单分支
![[Pasted image 20240828115143.png|200]]
2.判断是不是管理员 **没写fi**--双分支-
![[Pasted image 20240828115538.png|200]]

3.逻辑运算符格式1 
0-100 0-59 60-80 80-100 100单独写
![[Pasted image 20240828120449.png|200]]
3.1 格式2
![[Pasted image 20240828120740.png|200]]
4.x抵消
![[Pasted image 20240828122210.png|200]]
#### 2.3练习题

### **3** case条件语句
#### 3.1 case语法结构
```shell
case "字符串变量" in 
  值1)
     指令1
     ;;
  值2)
     指令2
     ;;
  值*)
     指令
esac ca
```

#### 3.2 case值的书写方式
```shell

apple)
      echo -e "$RED_COLOR apple $RES"
      ;;
也可以这样写，输入2种格式找同一个选项
apple|APPLE)
      echo -e "$RED_COLOR apple $RES"
      ;;
```
#### 3.3 case语句小结
case语句就相当于多分支的if语句。case语句的优势是更规范、易读。
case语句适合变量的值少，且为固定的数字或字符串集合。(1,2,3)或(start,stop,restart)。
系统服务启动脚本传参的判断多用case语句，多参考rpcbind/nfs/crond脚本；菜单脚本也可以使用case
#### 3.4 case练习
用case编写个两数加减乘除
![[Pasted image 20240829104917.png]]
`$?` 是一个特殊的变量，用于存储上一个命令的退出状态码

### **4** shell循环
#### 4.1do循环格式
> for((   ))
> do
> 循环体
> done

> for i in 字符串
> do
> 	echo "$i"
> done

> for i in {1..10}//1-10
> do
> 	echo "$i+1"
> done

> while【条件】
> do
> done
#### 4.1读取文件
> while read linesth
> do
>      echo "$linesth"
>  done< /home/fufu/1.txt

![[Pasted image 20240829121852.png]]

在数组最后加东西



#### 4.1练习题
##### 1.比较两数大小

![[01519ee4b7999668b712acb1a324679.png|400]]
> `expr 1 + $n2 &>/dev/null`
> `[ $? -eq 2 ] && echo "$n2 not int"`
- `expr 1 + $n1` 尝试执行一个数学表达式，`expr` 是一个命令，用于计算整数表达式的值。
- `&>/dev/null` 将输出重定向到 `/dev/null`，这意味着忽略命令的输出。
- `[ $? -eq 2 ]` 检查上一条命令的退出状态码。若等于 `2`，表示 `expr` 命令失败，通常是因为 `$n1` 不是整数。
- `&&` 表示如果上一个命令成功（退出码为 `0`），那么执行 `echo "$n1 not int"`，打印错误消息。
#### 2. 输出带颜色的水果
![[file-20240829222922274.png|400]]
![[file-20240829222848127.png|400]]

### 5 shell数组
##### 5.1 数组中的增删改查
数组的定义
```shell
# 定义数组
[root@clsn scripts]# stu=(001 002 003)
# 打印数组
[root@clsn scripts]# echo ${stu[@]}
001 002 003
# 显示数组长度
[root@clsn scripts]# echo ${#stu}
3
```
**查:** _遍历数组的内容_
```shell
# 打印数组内容（通过数组下标或索引）
[root@clsn scripts]# echo ${stu[0]}
001
[root@clsn scripts]# echo ${stu[1]}
002
[root@clsn scripts]# echo ${stu[2]}
003
[root@clsn scripts]# echo ${stu[3]}
```
```shell
# 遍历数组
  方法一
[root@clsn scripts]# for i in ${stu[@]};do echo $i ;done 
001
002
003
    # 方法二
[root@clsn scripts]# array=(1 2 3 4 5)
[root@clsn scripts]# for i in `eval 
echo {1..${#array[@]}}`;
do 
	echo ${array[i-1]};
done
1
2
3
4
5
```
**增**_：数组添加_
```shell
[root@clsn scripts]# stu[3]=004
[root@clsn scripts]# echo ${stu[@]}
001 002 003 004
```
**改**：_数组修改_
```shell
[root@clsn scripts]# stu[2]=000
[root@clsn scripts]# echo ${stu[@]}
001 002 000 004
```
**删**：_数组删除_
```shell
[root@clsn scripts]# unset stu[2]
[root@clsn scripts]# echo ${#stu[@]}
3
[root@clsn scripts]# echo ${stu[@]}
001 002 004
```
**替换**：数组替换echo输出的东西只是进行操作然后打印，不改变实际的值
```shell
fufu@fufu-virtual-machine:~$ a=('xm' 'lm' 'mm')
fufu@fufu-virtual-machine:~$ a=("${a[@]//m/w}")
fufu@fufu-virtual-machine:~$ echo ${a[@]}
xw lw ww
```
##### 5.2 关联数组的下标是字符串
declare -A a1
a1["app"] = 'QQ'
a1["flower"] = 'rose'
a1["food"] = 'fish'
```shell
#!/bin/bash
# 定义一个关联数组
declare -A a1
# 定义两个普通数组
a=('QQ' 'flower' 'food')
b=('app' 'rose' 'fish')
# 遍历数组并将内容作为下标赋值
for ((j=0; j<${#a[@]}; j++)); do
    a1[${a[j]}]=${b[j]}
done
# 输出关联数组的所有值
echo "All values in the associative array: ${a1[@]}"
# 输出关联数组的所有键值对
for key in "${!a1[@]}"; do
    echo "Key: $key, Value: ${a1[$key]}"
done
```
### shell函数
function
![[file-20240830102709110.png]]

```shell
#!/bin/bash
# 需要监控的目录
 watch="/home/fufu/scripts"
# 存储上次扫描的文件列表
prev_files=""
while true; do
  # 获取当前目录中的文件列表（按名称排序）
  curr_files=$(ls "$WATCH_DIR" | sort)
  # 比较当前文件列表与上次的文件列表
  if [ "$curr_files" != "$prev_files" ]; then
    echo "Directory contents have changed."
    exit 0
  fi
  # 更新上次的文件列表
  prev_files="$curr_files"
  # 每隔 30 秒扫描一次
  sleep 30
done
```

```shell
#!/bin/bash
# 需要监控的目录
# 使用 du 命令统计总大小（以字节为单位） 
du_output=$(du -sb "$WATCH_DIR") 
# 提取大小值 
total_size=$(echo "$du_output" | cut -f1) 
echo "$total_size" }
while true; do
  cur_files=$(ls "$watch")
      if [ "$cur_files" != "$last" ]; then
         echo "文件变化"
          exit 0
          fi
	#把当前的更新一下
  last_files="$cur_files"
  # 统计并输出目录总大小
  total_size=$(calculate_total_size)
  echo "Total size of the directory: $total_size bytes"
  # 如果需要退出脚本，可以在这里添加退出条件
  # exit 0
done
```
```
#!/bin/bash
wh
watch="/home/fufu/scripts"
# 上一次的文件
last_files=""

# 计算目录大小
total_size() {
    # 使用 du 命令统计目录大小（以字节为单位）
    output=$(du -b "$watch")
    # 提取大小值：使用 Bash 字符串处理来去除目录路径
    size=${output%%$watch*}
    echo "$size"
}
# 文件变化
while true; do
    cur_files=$(ls "$watch")
    if [ "$cur_files" != "$last_files" ]; then
        echo "文件变化"
        total_size=$(total_size)
        echo "Total size of the directory: $total_size bytes"
        exit 0
    fi
    # 更新上一次的文件列表
    last_files="$cur_files"
    sleep 30
done

```
```shell
 # 计算目录大小
 33 total_size() {
 34     output=$(du -b "$watch")
 35     # 提取大小值（去掉目录路径）
 36     size=${output%%$watch*}
 37     echo "$size"
 38 }
 39
 40 # 获取初始的目录大小
 41 first_size=$(total_size)
 42 echo "Initial size of the directory: $first_size bytes"
 43
 44 # 文件变化检测
 45 while true; do
 46     # 获取当前目录大小
 47     cur_size=$(total_size)
 48
 49     # 获取当前的文件列表
 50     cur_files=$(ls "$watch")
 51
 52     # 显示当前目录大小
 53     echo "Current size: $cur_size bytes"
 54
 55     # 检查文件变化
 56     if [ "$cur_files" != "$last_files" ]; then
 57         echo "文件发生变化"
 58         echo "变化前的大小：$first_size bytes"
 59         echo "变化后的大小：$cur_size bytes"
 60         exit 0
 61     fi
 62
 63     # 更新上一次的文件列表
 64     last_files="$cur_files"
 65
 66     # 等待 30 秒
 67     sleep 30
 68 done

```

```shell
#!/bin/bash
# 监控的目录路径
watch="/your/directory/path"  # 将此更改为你要监控的目录路径
# 计算目录大小
total_size() {
    output=$(du -sb "$watch" 2>/dev/null)  # 使用 -s 仅输出总大小，并重定向错误输出
    size=${output%%[^0-9]*}  # 提取数字部分（大小值）
    echo "$size"
}
# 获取初始的目录大小
first_size=$(total_size)
echo "Initial size of the directory: $first_size bytes"
# 初始化文件列表
last_files=$(ls "$watch")
# 文件变化检测
while true; do
    # 获取当前目录大小
    cur_size=$(total_size)
    # 获取当前的文件列表
    cur_files=$(ls "$watch")
    # 显示当前目录大小
    echo "Current size: $cur_size bytes"
    # 检查文件变化
    if [ "$cur_files" != "$last_files" ]; then
        echo "文件发生变化"
        echo "变化前的大小：$first_size bytes"
        echo "变化后的大小：$cur_size bytes"
        exit 0
    fi
    # 更新上一次的文件列表
    last_files="$cur_files"
    # 等待 30 秒
    sleep 30
done
```
![[file-20240831095851214.png]]
```shell
!/bin/bash                                                                                                                                                                                                                                                             
  2 #files name ：log_sripts.sh
  3 #created time : 2024-8-31
  4 
  5 watch_path=/home/fufu/scripts/log
  6 path=/home/fufu/scripts
  7 
  8 #检查路径存在
  9 if [ -e "$watch_path" ];then
 10 
 11     #若存在看是不是文件 or 目录 
 12     if [ -f "$watch_path" ];then
 13         echo "$watch_path 是普通文件"
 14  
 15         #检查空文件
 16         if [ -s "$watch_path" ];then
 17             rm -f "$watch_path"
 18             echo "文件 $watch_path 不为空，已删除"
 19             #文件不为空，删除文件创建logical目录
 20             mkdir ${path}/logical
 21             echo "logical目录已经创建"
 22             touch ${path}/logical/output.txt
 23 
 24             i=1
 25             while read strline
 26             do
 27                 echo "The $i account is \"${strline%%:*}\"">>${path}/logical/output.txt
 28                 ((i++))
 29             done</etc/passwd
 30 
 31             echo "$new_files已经保存了数据"
 32         fi
 33         #如果不是文件
 34     elif [ -d "$watch_path" ];then
 35         echo "$watch_path是目录文件"
 36         #是目录就删除
 37         rm -f "$watch_path"
 38         echo "这个目录已经删除"
 39 
 40         mkdir -p ${path}/logical
 41         echo "logical已经创建"
 42         #复制/etc/passwd
 43         cp /etc/passwd  ${path}/1.cp
 44 
 45         cd ${logical}
 46         #拆分/etc/passwd 成4行一个小文件-split
 47         split -l 4 1.cp
 48         echo "文件拆分完成"
 49 
 50         #压缩
 51         tar -zcf spon.tar.gz 1.cp x*
 52         cd -
 53     fi
 54 else
 55     #文件不存在
 56     echo "/home/fufu/scripts/log不存在"
 57     whoami > user1.txt
 58     pwd >> user1.txt
 59 
 60     cur_user=$(whoami)
 61     cur_log1=$(pwd)
 62     
 63     echo "当前用户：$cur_user"
 64     echo "当前目录: $cur_log1"
 65 fi

```
### 1.for循环
#### 1.1 shell中的for
**_Shell_** **_中的两种样式_**
###### 样式一：
for i in 1 2 3 
  do 
    echo $i
done
###### 样式二：
for i in 1 2 3;do  echo $i;done
#### 2.【for练习题】

### 3.while循环