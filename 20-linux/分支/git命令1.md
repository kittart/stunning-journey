
===================================================
			Git版本管理：
			主要是管理代码的版本为主
		版本管理分为2种：
			1、分布式管理：Git
			2、集中式管理：SVN
		----------------------------
Git命令：
1、版本克隆
git clone ssh库地址		//将远程服务器的版本拷贝到本地目录
如：git clone ssh://admin@115.28.86.8:29418/~admin/test_324_2_0618.git
	[克隆完了之后，切换到版本目录里面去，进入主线版本:主分支]
2、推版本：三部曲
	2.1：添加文件
		git add 文件名		// 添加单个文件，将文件放到缓存
		git add .			// 批量添加当前目录下所有修改的文件	
	2.2：提交文件到本地库
		git commit -m "文字描述[本次操作的意图]"
					// 将缓存的内容提交到本地库，产生最新版			
	2.3：推版本到远程库
	git push		
	3、修改用户信息：全局修改[针对所有版本]
		git config --global user.name "用户名"
		git config --global user.email "邮箱@qq.com"
	4、拉版本:
		git pull	//将远程库最新版修改的文件拉到本地并合并到本地库	
	5、合并：
		git merge
	6、解决冲突：
		git rebase
	查看比较git diff ，找到冲突的文件，再vim修改，再提交
	7、查看提交历史，获取版本id/版本号
		git log
	8、版本回退
		git reset --hard 版本号	// 通过git log 拿到指定版本号
	9、命令区别：
		git pull	//拉最新修改的文件到本地并合并
		git fetch	//抓取最新修改的文件到本地，不合并[需用 git merge合并]
		git clone 	//整个库都拷贝下载到本地，产生本地库
	10：分支操作
	10.1 查看分支
		git branch		// 查看当前分支及本地分支绿色的
		git branch -a   // 查看所有分支
	10.2 创建分支
		git branch 分支名字		// 指定名字创建分支
	10.3 切换分支
		git checkout <branch_name> //切换到指定分支
		git checkout -b <branch_name> //创建并切换到指定分支 
	10.4 合并分支
		git merge 分支名 
	10.5 部分合并
		git cherry-pick    <commitHash>某个版本id //命令的作用，就是将指定的提交（commit）应用于其他分支。
	// 上面命令就会将指定的提交commitHash，应用于当前分支
【参考 https://blog.csdn.net/qq_35432904/article/details/107232691】
补充命令：
11、stash
git stash 隐藏当前工作的修改
如果不隐藏自己修改的半成品代码，就会发生切换到别的分支后，将然后自己的半成品代码带入其他分支，这样就发生很多不必要的麻烦。
git stash save message 执行存储时，添加备注，方便查找，只有git stash 也要可以的，但查找时不方便识别。

git stash list 查看隐藏的工作信息列表

git stash drop 删除隐藏的工作信息

git stash pop 恢复隐藏的工作信息，同时删除隐藏的工作信息

git stash apply [stash@{0}] 恢复指定的隐藏工作信息，但是不会删除隐藏的工作信息


12.diff
git diff HEAD -- . 查看最新本地版本库和工作区所有文件的区别

git diff HEAD -- [file-name] 查看最新本地版本库和工作区文件的却别

git diff HEAD^ -- [file-name] 查看本地上一个版本和工作区文件的却别

git diff [local branch] origin/[remote branch] 比较本地分支和远程分支的区别

		
13、# 生成一个可供发布的压缩包
git archive		
**查看支持的归档格式有tar、tgz、tar.gz、zip**
git archive --list 
**导出最新的版本库**
git archive -o ../latest.zip HEAD

**导出一个目录**
git archive -o ../git-1.4.0-docs.zip  HEAD:Documentation/ 
**导出指定提交记录**
git archive -o ../git-1.4.0.tar 8996b47 
**导出为tar**.gz格式
git archive   8996b47 | gzip > ../git-1.4.0.tar.gz
**导出最后一次提交修改过的文件** 
git archive -o ../updated.zip HEAD $(git diff --name-only HEAD^)
