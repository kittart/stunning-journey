### 标准 I/O 流
每个进程（包括命令）在运行时都有三个标准的 I/O 流：
1. **标准输入（Standard Input，`stdin`）**：默认从键盘获取输入。文件描述符为 `0`
2. **标准输出（Standard Output，`stdout`）**：默认输出到屏幕。文件描述符为 `1`
3. **标准错误（Standard Error，`stderr`）**：默认输出错误信息到屏幕。文件描述符为 `2`
4. 索引对应文件
## 重定向操作
**输出重定向** `>` `>>`  `&> / >& `
**输入重定向** `<`

#### ==覆盖输出 >==
**默认标准输出** **如果是标准错误就加 ==2==**
将命令的输出写入文件，若文件存在，就覆盖
> ls > output.txt  
> cat 1.txt > `/dev/null` 禁止输出的作用 传入数据流
> cat 1.txt > `/dev/null` 2>&1 数据流流向的通道1
- ==合并多个文件==：
	cat 1.txt 2.txt > 3.txt
	将这俩合并到新的3.txt文件里面，跟cp复制命令一样
	cat 1.txt > 1.txt.bak
#### ==追加输出 >>==
将命令的输出追加到文件末尾，若文件不存在，就创建这个文件
> echo "New Line" >> output.txt

#### ==输入重定向 <==
将文件的内容重定向为命令的输入
> cat < 1.txt

#### ==重定向错误输出 2>==
将错误输出写入文件，若文件存在，则覆盖文件
> ls /nonexistent_directory 2> 1.txt
> 将ls命令的错误输出信息保存到 1.txt中

#### ==追加错误输出 2>>==
将错误输出追加到文件末尾，若文件不存在，则创建该文件

> ls /nonexistent_directory 2>> 1.txt
> 这会将 `ls` 命令的错误信息追加到 `error.txt` 文件末尾

```shell
# 使用 cut 提取账号名称，并通过重定向写入新文件 
cut -d: -f1 /etc/passwd > "$new_file" 
# 使用 sed 格式化输出 
sed -i 's/^/The /; s/$/ account is/' "$new_file" 
# 添加行号 
nl "$new_file" | sed 's/\t/ /' > "${new_file}.tmp" && mv "${new_file}.tmp" "$new_file" 
echo "提取的账号信息已保存到 $new_file"
```
## 组合重定向
### 1.合并标准输出和错误输出  2>&1
- cat 1.txt >> /dev/null 2>&1
	/dev/null 空文件起到禁止输出的作用
	2> :输出 错误
	&1 ：通道1


 - 将标准输出和标准错误同时覆盖到文件
> ls /valid_directory /nonexistent_directory > output.txt 2>&1
> 这会将 `ls` 命令的输出和错误信息同时保存到 `output.txt` 文件中
- 将标准输出和标准错误同时追加到文件
> command >> file.txt 2>&1
> 这会将 `command` 的输出和错误信息追加到 `file.txt` 文件末尾
### 2.将标准输出和错误分开重定向
可以将标准输出和标准错误分别重定向到不同的文件
> ls /valid_directory /nonexistent_directory > output.txt 2> error.txt
> 将 `ls` 命令的标准输出保存到 `output.txt`，错误输出保存到 `error.txt`

## echo 标准输出
- echo 'abc' > ./a.txt
	在当前的目录下创建a.txt，并输出
	![[Pasted image 20240824094527.png]]
	单独输入echo 代表换行
	![[Pasted image 20240824094706.png]]
	echo -n 取消换行
	echo -e 使转义字符生效 
	echo -e =="a/tcd"== 双引号加
`\`转义字符 占用1字节 转义特殊意义的字符 

接下来看这个
[[进程通信]]