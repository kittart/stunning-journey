
| vim 模式 |                                     |
| ------ | ----------------------------------- |
| 命令模式   | [[#**1. 命令模式**|**1. 命令模式**]]                    |
| 底线命令模式 | [[#**底线命令模式**（Command-Line Mode）：|**底线命令模式**（Command-Line Mode）：]] |
| 查找字符串  | [[#查找操作|查找操作]]                           |
| 替换     | [[#**替换指令 切换到底线命令模式下**|**替换指令 切换到底线命令模式下**]]            |
|        |                                     |

[Vim配置文件[非常全面]_vim的配置文件-CSDN博客](https://blog.csdn.net/qq_41113081/article/details/100152358)

---
### **命令模式**（Normal Mode）：
用于执行基本的编辑操作，如移动光标、删除、复制等。通过按 `Esc` 键返回到命令模式。
在其他模式下按 `Esc` 键可以返回到命令模式
#### 常用命令模式操作：

- **移动光标**：
    
    - `h`：向左移动一个字符
    - `j`：向下移动一行
    - `k`：向上移动一行
    - `l`：向右移动一个字符
    - `w`：跳到下一个单词的开头
    - `b`：跳到上一个单词的开头
- **删除和复制文本**：
    
    - `d`：删除文本，例如 `dw` 删除一个单词
    - `x`：删除光标位置的字符
    - `y`：复制文本，例如 `yy` 复制当前行
    - `p`：粘贴已复制或删除的文本
- **进入其他模式**：
    
    - `i`：进入插入模式
    - `:`：进入底线命令模式
    - `v`：进入可视模式（选择文本）
记住
### **快捷键操作：**
![[Pasted image 20240822102151.png|400]]

### **底线命令模式**（Command-Line Mode）：
用于执行更复杂的命令，如保存文件、退出 Vim、查找和替换等。通过在命令模式下按 `:` 键进入底线命令模式。
#### 常用底线命令模式操作：
- **保存文件**：
    - `:w`：保存文件
    - `:w filename`：保存文件到指定名称 `filename`
- **退出 Vim**：
    - `:q`：退出 Vim（如果没有未保存的更改）
    - `:q!`：强制退出 Vim（不保存更改）
    - `:wq` 或 `:x`：保存更改并退出 Vim
- **查看文件信息**：
    - `:e filename`：编辑指定的文件
    - `:ls` 或 `:buffers`：列出所有打开的缓冲区
    - `:b buffer_number`：切换到指定的缓冲区
#### 分屏与窗口管理
- `:split filename` 或 `:sp filename`：水平分屏并打开文件。
- `:vsplit filename` 或 `:vsp filename`：垂直分屏并打开文件。
- `Ctrl + w + w`：在分屏窗口之间切换。
- `:q`：关闭当前分屏窗口。
#### 退出 `vim`
当你需要退出 `vim` 时，可以根据情况使用：
- `:wq` 保存并退出。
- `:q!` 不保存并强制退出。
### **替换指令|切换到底线命令模式下**
:{作用范围}s/{目标}/{替换}/{替换标志}
作用范围：没有指定范围，则作用于当前行
替换标志：g 如果不加就替换每一行的第一个匹配的
1.输入； 1s/a000/g
代表把第一行的a替换为000
![[Pasted image 20240822092703.png|200]]
得到结果：
![[Pasted image 20240822092734.png|200]]
2.%s/a/00/g
代表将所有的a替换成00
![[Pasted image 20240822093046.png|200]]
同理，将所有的00替换成a
![[Pasted image 20240822093057.png|200]]
得到结果：
![[Pasted image 20240822093111.png|200]]
g ：
c ：提示
e ：
i ：忽略大小写



### 查找操作
1. 查找字符串：**模糊查找**
- `/`后加要查找的字符串，从光标处开始向下开始查找字符串
- ？后加要查找的字符串，从光标处开始向上开始查找字符串
2. 查找单词：**精确查找**
- shift `*`或`#`
`*`向下完整匹配光标下的单词
`#` 向上完整匹配光标下的单词
**光标定位在单词上- `shift */#`** 
之后按 N/n 按n(小写)查找下一个,按N(大写)查找上一个
3. 单词头尾锁定符：\< >\
![[Pasted image 20240822094839.png|200]]
