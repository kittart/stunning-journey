#### 备份文件
```shell
#!/bin/bash
# 定义源目录和备份目录
SOURCE_DIR="/path/to/source"
BACKUP_DIR="/path/to/backup"
# 创建备份文件名
DATE=$(date +%Y%m%d%H%M%S)
BACKUP_FILE="$BACKUP_DIR/backup_$DATE.tar.gz"
# 执行备份
tar -czvf $BACKUP_FILE $SOURCE_DIR
echo "备份完成：$BACKUP_FILE"
```
#### 批量重命名文件
```shell
#!/bin/bash
count=1
for file in *.txt; do
  mv "$file" "file$count.txt"
  ((count++))
done
echo "所有文件已重命名。"
```
检查网络连接
```shell
#!/bin/bash
ping -c 1 www.google.com &> /dev/null
if [ $? -eq 0 ]; then
  echo "网络连接正常。"
else
  echo "无法连接到网络。"
fi
```
自动化系统更新
```shell
#!/bin/bash
echo "开始系统更新..."
sudo apt update
sudo apt upgrade -y
sudo apt autoremove -y
echo "系统更新完成！"
```
打印象棋盘
```shell
29、打印国际象棋棋盘 
#!/bin/bash 
# 打印国际象棋棋盘
# 设置两个变量,i 和 j,一个代表行,一个代表列,国际象棋为 8*8 棋盘 
# i=1 是代表准备打印第一行棋盘,第 1 行棋盘有灰色和蓝色间隔输出,总共为 8 列 
# i=1,j=1 代表第 1 行的第 1 列;i=2,j=3 代表第 2 行的第 3 列 
# 棋盘的规律是 i+j 如果是偶数,就打印蓝色色块,如果是奇数就打印灰色色块 
# 使用 echo ‐ne 打印色块,并且打印完成色块后不自动换行,在同一行继续输出其他色块 
for i in {1..8} 
do 
	for j in {1..8} 
	do 
		sum=$[i+j] 
		if [ $[sum%2] -eq 0 ];then 
		echo -ne "\033[46m \033[0m" 
		else echo -ne "\033[47m \033[0m" 
		fi 
		done 
	echo 
done
```
#### 查找僵尸进程
```shell
查找 Linux 系统中的僵尸进程 
#!/bin/bash 
# 查找 Linux 系统中的僵尸进程 
# awk 判断 ps 命令输出的第 8 列为 Z 是,显示该进程的 PID 和进程命令 
ps aux | awk '{if($8 == "Z"){print $2,$11}}'
```
多脚本调用
```shell
#!/bin/bash

# 检查参数个数是否为3个（两个数和一个运算符）
if [ $# -ne 3 ]; then
    echo "Usage: $0 number1 operator number2"
    exit 1
fi

# 获取参数
num1=$1
operator=$2
num2=$3

# 计算并输出结果
case $operator in
    +) result=$(echo "$num1 + $num2" | bc) ;;
    -) result=$(echo "$num1 - $num2" | bc) ;;
    \*) result=$(echo "$num1 * $num2" | bc) ;;
    /) result=$(echo "scale=2; $num1 / $num2" | bc) ;;
    *) echo "Invalid operator! Use +, -, *, or /." ; exit 1 ;;
esac
echo "Result: $result"
```
```shell
#!/bin/bash

# 读取用户输入的两个数字和运算符
read -p "Enter the first number: " num1
read -p "Enter the operator (+, -, *, /): " operator
read -p "Enter the second number: " num2

# 三种调用 call.sh 脚本的方式：

# 1. 使用 source 命令
echo "Calling with source:"
source ./call.sh $num1 $operator $num2

# 2. 使用 . (点) 命令
echo "Calling with dot:"
. ./call.sh $num1 $operator $num2

# 3. 直接执行脚本
echo "Calling with direct execution:"
./call.sh $num1 $operator $num2
n1
```

两个脚本调用，输入俩数加减乘除
主调脚本
```shell

```
被调脚本
```shell
 if [ $# -ne 3 ] ;then
  6     echo "输入不足三个，请重新输入"
  7     exit 1
  8 fi
  9 n1=$1
 10 operator=$2
 11 n2=$3
 12
 13 case $operator in
 14     '+')
 15         res=$(echo "$n1 + $n2" | bc )
 16         ;;
 17     '-')
 18         res=$(echo "$n1 - $n2" | bc )
 19         ;;
 20     '*')
 21         res=$(echo "$n1 * $n2" | bc )
 22         ;;
 23     '/')
 24         if [ $n2 -eq 0 ]
 25         then
 26             echo "除数不为0"
 27             exit 2
 28         else
 29             res=`echo "scale=2;$n1/$n2" | bc`
 30             echo "$n1 /$n2 = $res"
 31         fi
 32         ;;
 33     *)
 34         echo "输入运算符错误"
 35         exit 3
 36         ;;
 37 esac
 38 exit 0
 39 echo "答案是：$res"
```