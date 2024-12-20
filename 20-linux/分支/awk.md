[AWK常用技巧 - 惨绿少年 - 博客园 (cnblogs.com)](https://www.cnblogs.com/clsn/p/8419374.html)

**awk的核心是格式化**
![[file-20240909204927541.png]]
![[file-20240903113023606.png|400]]



| 内置变量 |                      |
| ---- | -------------------- |
| 变量名  | 属性                   |
| $0   | 当前记录                 |
| 1  n | 当前记录的第 n 个字段         |
| FS   | 输入字段分隔符 默认是空格        |
| RS   | 输入记录分割符 默认为换行符       |
| NF   | 当前记录中的字段个数，就是有多少列    |
| NR   | 已经读出的记录数，就是行号，从 1 开始 |
| OFS  | 输出字段分隔符 默认也是空格       |
| ORS  | 输出的记录分隔符 默认为换行符      |
> 
> 
> -F 指定分割符,可以直接写F后面或者单引号分
> $n :指第n列 内置变量 按照字段分隔开
> $0 :指全文本
> NF表示列
> NR表示行号，从1开始
> $NF表示最后一列
> RS -vRS可指定每行结束的标识符，默认是回车
> FS 读取指定分隔符，默认是空格
> awk '{print $0}' 2.txt 全文本打印
> $(NF-n) 倒数第n+列
> FS：**输入字字段分隔符，默认为空白字符**  
> OFS：**输出字段分隔符**，默认为空白字符  
> RS：**输入记录分隔符**，指定输入时的换行符，原换行符仍有效  
> ORS：**输出记录分隔符**，输出时用指定符号代替换行符  
> **NF**：字段数量，**共有**多少字段， `$NF`引用最后一列，$(NF-1)引用倒数第2列  
> **NR**：行号，后面可以跟多个文件，第二个文件行号继续从第一个文件最后行号开始  
> **FNR**：各文件分别计数，行号，后跟一个文件和NR一样，跟多个文件，**第二个文件行号从1开始**  
> FILENAME:当前文件名  
> ARGC:**命令行参数的个数**  
> ARGV：数组，保存的是命令行所给的各参数，**查看参数**  



|   |   |   |   |
|---|---|---|---|
|元字符|功能|示例|解释|
|^|行首定位符|/^root/|匹配所有以 root 开头的行|
|$|行尾定位符|/root$/|匹配所有以 root 结尾的行|
|.|匹配任意单个字符|/r..t/|匹配字母 r,然后两个任意字符，再以 l结尾的行，比如 root,r33l 等|
|*|匹配 0 个或多个前导字符(包括回车)|/a*ool/|匹配 0 个或多个 a 之后紧跟着 ool 的行，比如 ool，aaaaool 等|
|+|匹配 1 个或多个前导字符|/a+b/|匹配 1 个或多个 a 加 b 的行，比如ab,aab 等|
|?|匹配 0 个或 1 个前导字符|/a?b/|匹配 b 或 ab 的行|
|[]|匹配指定字符组内的任意一个字符|/^[abc]|匹配以字母 a 或b 或 c 开头的行|
|[^]|匹配不在指定字符组内任意一个字符|/^[^abc]/|匹配不以字母 a 或 b 或 c 开头的行|
|()|子表达式组合|/(rool)+/|表示一个或多个 rool 组合，当有一些字符需要组合时，使用括号括起来|
|\||或者的意思|/(root)\|B/|匹配root 或者 B 的行|
|\|转义字符|/a\/\//|匹配 a//|
|~,!~|匹配，不匹配的条件语句|$1~/root/|匹配第一个字段包含字符root 的所有记录|
|x{m}|x 重复m 次|/(root){3}/|需要注意一点的是，root 加括号和不|
|x{m,}|x 重复至少m 次|/(root){3,}/|加括号的区别，x 可以表示字符串也|
|X{m,n}|x 重复至少 m 次，但不超过 n 次|/(root){5,6}/|可以只是一个字符，所以/root\{5\}/表示匹配roo 再加上5 个t，及roottttt|
||需要指定参数：-posix  或者--re-interval    没 有该参数不能使用该模式|cat   rex.txt smierth,harry smierth,reru robin,tom|/rootroot\{2,\}/ 则   表 示 匹 配rootrootrootroot 等awk -posix '/er\{1,2\}/' rex.text smierth,harry smierth,reru|

示例：
- **打印所有列** 
awk -F: '{$1=$1;print}' 2.txt
![[file-20240903105419659.png|400]]
- $1代表第一列，第一字段分开的
![[file-20240903105550474.png|400]]
- **每一行有多少列** 
awk -F/ '{print NF}' 2.txt
![[file-20240903105740186.png|400]]
- **统计有多少行** 
awk -F/ '{printf NR}' 2.txt
![[file-20240903105823876.png|400]]
- **给内容加行号并显示** 
awk -F/ '{printf NR，$0}' 2.txt
![[file-20240903110005249.png|400]]
- **给某一列或什么中间加入字符用双引号加入** 
`awk -F： '{print "第一列：" $1 "\t第二列："$2}' 2.txt`
![[file-20240903110135283.png|400]]
- 打印最后一列
![[20-嵌入式linux/分支/assets/awk/file-20240903110356261.png|400]]
- $NR
![[file-20240903110520613.png|400]]
- **查看第n行n列**
`awk -F：'NR==3{print $4}' 2.txt`
![[file-20240903111348027.png|400]]
- **查看第n行到第n行的第几列**
`awk -F：'NR==3，NR==4{print $4}' 2.txt`
![[file-20240903111434963.png|400]]
- 自定分隔符分割
awk -v RS=":" '{print $0}' 2.txt
这条命令会将 `2.txt` 文件中的记录以冒号为分隔符进行分割，然后打印每个记录。
![[file-20240903113349036.png|400]]
- **输出内容以什么为换行符，默认**\n，
使用了 `-F:` 选项来设置字段分隔符为冒号 `:`，并且用 `-v ORS="/"` 来设置输出记录分隔符为斜杠 `/`。你的命令会把每一行的字段用斜杠 `/` 连接起来，并输出结果。
![[file-20240903113613275.png|400]]
你的命令 `awk '{ORS=" " ;print}' 2.txt` 正确地设置了输出记录分隔符 `ORS` 为一个空格，因此每一行记录之后都会加上一个空格。
这是一个有用的技巧，特别是在你想把文件中的所有行连接成一行并用特定字符（如空格）分隔时。如果你想用其他分隔符（如逗号或斜杠），只需将 `ORS` 设置为相应的字符：
![[file-20240903114025363.png]]
![[file-20240903114136805.png]]
- **显示行号的两个不同效果**
**使用 `NR`（记录号）**
awk '{print NR,$0}' 1.txt 2.txt
`NR` 是全局记录号，表示在所有输入文件中处理过的记录的总数。由于你同时处理了 `1.txt` 和 `2.txt`，它会跨文件计数，输出的行号从 1 到 14
![[file-20240903114253521.png|400]]
**使用 `FNR`（文件记录号）**
awk '{print FNR,$0}' 1.txt 2.txt 
`FNR` 是每个文件内部的记录号，因此它在每个文件中从 1 开始重新计数。在 `1.txt` 中，它的行号从 1 到 10，在 `2.txt` 中，它的行号也从 1 开始继续到 4。
![[file-20240903114338174.png|400]]
- 用：和/一起分隔开 
这条命令会打印所有包含 `3` 的行。`-F ":"` 设置字段分隔符为冒号 `:`，然后 `/3/` 是一个模式匹配，表示匹配包含 `3` 的行。
![[file-20240903120847754.png|400]]
这条命令会打印所有不包含 `3` 的行。`!/3/` 表示排除包含 `3` 的行。
![[file-20240903120905445.png|400]]
`$3!~/3/` 表示选择第三个字段（以冒号 `:` 分隔的字段）中不包含 `3` 的行。
![[file-20240903120935680.png|400]]
`2.txt` 文件中第三个字段包含 `3` 的所有行
![[file-20240903121005857.png|400]]
筛选第三个字段小于或等于 3 的行
![[file-20240903121045881.png|400]]
筛选第一个字段等于 `"rOOT"` 的行
![[file-20240903121140393.png|400]]
筛选第三个字段包含 `3` 的行
![[file-20240903121223043.png|400]]

### 内置函数
sub(r,s,$n)：与gsub类似，但仅替换第一个匹配的字符串，而不是替换全部

substr(s,i,n)：对字符串s进行截取，从第i位开始，截取n个字符串，如果n没有指定则一直截取到字符串s的末尾位置

gsub(r,s,$n)：将字符串t中所有与正则表达式r匹配的字符串全部替换为s,如果没有指定字符串t，则默认对$0进行替换操作

split(字符串，数组，分隔符)：将字符串按特定的分隔符切片后存储在数组中，如果没指定分隔符，则使用IFS定义的，数组下标从1开始

int(expr)：可以对小数取整

match(s,r)：根据正则表达式r返回其在字符串s中的位置坐标

```shell

fufu@fufu-virtual-machine:~$ awk 'BEGIN{split("hi,xiaoming",str,",");print str[1],str[2]}' 2.txt
hi xiaoming
fufu@fufu-virtual-machine:~$ awk 'BEGIN{a="xiaoming";print index(a,"o")}'                 4
fufu@fufu-virtual-machine:~$ awk 'BEGIN{print int (3.14)}'
3
fufu@fufu-virtual-machine:~$ awk 'BEGIN{a="xiaoming";print length(a)}'
8
fufu@fufu-virtual-machine:~$ awk 'BEGIN{t[0]="hi";t[1]="nihao";print length(t)}'
2
fufu@fufu-virtual-machine:~$ awk '{print length()}' 2.txt
31
47
36
36
fufu@fufu-virtual-machine:~$ awk 'BEGIN{print tolower("NI")}'
ni
fufu@fufu-virtual-machine:~$ awk 'BEGIN{a="xyz";print match(a,"[a-z]")}'
1
fufu@fufu-virtual-machine:~$ awk 'BEGIN{a="xyz";print match(a,"[0-9]")}'
0

```