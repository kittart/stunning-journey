![[532477b96c5d8339798c3b621e5a313.png]]

> ### Git 操作总结
> 1. **克隆仓库**
>     `git clone <仓库地址>`
> 2. **查看状态**
>     `git status`
> 3. **添加文件到暂存区**
>     `git add <文件名> # 添加所有更改的文件 git add .`
> 4. **提交更改**
>     `git commit -m "提交说明"`
> 5. **推送到远程仓库**
>     `git push origin <分支名>`
> 6. **拉取远程更改**
>     `git pull origin <分支名>`
> 7. **查看提交历史**
>     `git log`
> 8. **合并分支**
>     `git merge <分支名>`
> 9. **创建新分支**
>     `git branch <新分支名>`
> 10. **切换分支**
>     `git checkout <分支名>`
> 11. **删除分支**
>     `git branch -d <分支名>`
> ### 常见问题处理
> - **推送失败提示“fetch first”**：这通常是因为远程有新的提交。你可以先拉取远程更改并合并，然后再推送。
>     `c`
> - **合并时发生冲突**：Git会提示你哪些文件有冲突。你需要手动解决这些冲突，然后继续提交和推送。
> 
---

删除远程跟踪文件
```
删除文件并保留本地文件
git rm --cached <file>
删除目录并保留本地目录
git rm -r --cached <directory>


```
git clone ssh://admin@115.28.86.8:29418/~admin/昆仑_1025.git



[Git入门图文教程(1.5W字40图)🔥🔥--深入浅出、图文并茂 - 安木夕 - 博客园 (cnblogs.com)](https://www.cnblogs.com/anding/p/16987769.html)
git的工作流程一般是这样的：
１、在工作目录中添加、修改文件；
２、将需要进行版本管理的文件放入暂存区域；
３、将暂存区域的文件提交到git仓库。
因此，git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)
### git基操
> [!tip]
> ==git配置==
> git config --global user.name "名字"
> git config --global user.email "真实邮箱"
> ==查看一下是否配置成功==
> git config --list
> ==git和gitee账户建立ssh安全链接==
> ssh-keygen -t rsa -C "刚刚的真实邮箱"
[一个小时学会Git - 张果 - 博客园 (cnblogs.com)](https://www.cnblogs.com/best/p/7474442.html#_label3_1_1_4)
##### 配置本地的代码库
git config --global user.name "m17795927808"
git config --global user.email "m17795927808@163.com"
![[file-20240912091420547.png]]
##### 查看当前用户
git config --global --list
![[file-20240912205324458.png]]
![[file-20240912091814606.png]]
##### 生成 SSH 密钥
- 执行 `ssh-keygen` 命令，一路按回车即可完成生成密钥的操作。
- 公钥路径通常为 `~/.ssh/id_rsa.pub`。
##### 拷贝公钥到GITEE
- 使用命令 `cat ~/.ssh/id_rsa.pub` 查看并复制公钥。
- 将复制的公钥添加到你的 Gitee 账号的 SSH 公钥设置中
![[file-20240912092703502.png]]
##### 测试SSH链接:
ssh -T git@gitee.com
看到类似于 "Welcome to Gitee.com" 的提示信息则表示成功。
![[file-20240912094125409.png]]

##### 下载代码，拉取请求
![[file-20240912094512666.png]]
##### 本地仓库初始化 
git项目在项目目录
![[file-20240912095107179.png]]
##### 文件上传添加到本地仓库
- 使用 `git add xxx.cpp yyy.h` 命令将修改的文件添加到暂存区。
- 使用 `git commit -m "描述本次修改内容"` 提交文件到本地仓库。
##### 上传远程仓库链接
这样就把要修改的文件添加到待上传的本地仓库了，下一步就是上传到我们gitee的远程仓库里，还需要把本地仓库和远程仓库(gitee上手工创建远程仓库，右边图)建立一下链接
![[file-20240912100557199.png]]
![[file-20240912101350026.png]]
##### 拉取远程仓库
如果远端代码的文件数量和名称等和本地有冲突，需要远端代码与本地代码的冲突合并 （我们的远端代码可能含有 ReadMe 文件，本地代码没有，这时就需要我们去合并），如果没有冲突就不需要这一步
==git pull --rebase origin master==
pull是从远端拉下来
##### push到远端仓库 完成代码更新
![[file-20240912100456266.png]]
##### ==查看日志==
git log
==只从stage中删除，保留物理文件==
git rm --cached readme.txt 
==不但从stage中删除，同时删除物理文件==
git rm readme.txt

#### 文件状态以及查看
- **Untracked**: 未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过`git add` 状态变为`Staged`.
- **Unmodify**: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为`Modified`. 如果使用`git rm`移出版本库, 则成为`Untracked`文件
- **Modified**: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过`git add`可进入暂存`staged`状态, 使用`git checkout` 则丢弃修改过, 返回到`unmodify`状态, 这个`git checkout`即从库中取出文件, 覆盖当前修改
- **Staged**: 暂存状态. 执行`git commit`则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为`Unmodify`状态. 执行`git reset HEAD filename`取消暂存, 文件状态为`Modified`
 ![[file-20240912213701899.png]]
 查看文件变化 git status只能看见文件做了改动，如果要看改动了什么，需要用git diff
 ![[file-20240912215520966.png]]
**比较暂存区的文件与之前已经提交过的文件**
git diff --cached
**也可以把WorkSpace中的状态和repo中的状态进行diff**，命令如下:
比较repo与工作空间中的文件差异
git diff HEAD~n
![证件照end](https://img.picgo.net/2024/10/30/enda0ad8e347e5a3eec.jpg)



![证件照end](https://img.picgo.net/2024/10/30/enda0ad8e347e5a3eec.jpg)

![证件照end](https://img.picgo.net/2024/10/30/enda0ad8e347e5a3eec.jpg)