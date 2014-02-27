#Git指令快速查看
### 3.1 何为分支

* Git创建分支```git branch testing```
* HEAD 指向当前所在的分支
* 切换到其他分支，可以执行```git checkout``` 命令

### 3.2 Git 分支 - 分支的新建与合并
* 新建并切换到该分支，运行```git checkout```并加上```-b```参数

	```
	$ git checkout -b iss53
	Switched to a new branch 'iss53'

	```
	
	相当于
	
	```
	$ git branch iss53
	$ git checkout iss53
	```
* 删除分支

	```
    $ git branch -d hotfix
	Deleted branch hotfix (was 3a0874c).
	```
* 合并分支的时候有时候会用到```git mergetool```该命令来处理冲突

### 3.3 Git 分支 - 分支的管理
* 查看分支```$ git branch -v``` +v则会显示最后一次提交的信息

	```
	$ git branch
  	iss53
	* master
  	testing
  	```
* 筛选出已经（或尚未）与当前分支合并的分支，--merged和--no-merged
   
	```
	$ git branch --merged
	  iss53
	* master
	$ git branch --no-merged
	  testing
	```
	
### 3.5 远端分支	

* 同步远程服务器上的数据到本地```git fetch origin```
* 推送本地分支```git push (远程仓库名) (分支名)```

  ```git push origin serverfix:serverfix```==```git push origin serverfix```上传我本地的 serverfix 分支到远程仓库中去，仍旧称它为 serverfix 分支,此语法，你可以把本地分支推送到某个命名不同的远程分支：若想把远程分支叫作 awesomebranch，可以用 git push origin serverfix:awesomebranch 来推送数据。
  
* 想要一份自己的 serverfix 来开发，可以在远程分支的基础上分化出一个新的分支来：
  
	```
	$ git checkout -b serverfix origin/serverfix
	  Branch serverfix set up to track remote branch serverfix from origin.
	  Switched to a new branch 'serverfix'
	```
	
* 跟踪远程分支

	```
	$ git checkout --track origin/serverfix
	  Branch serverfix set up to track remote branch serverfix from origin.
	  Switched to a new branch 'serverfix'
	```	
	
* 删除远程分支```git push [远程名] :[分支名]```

	```
	$ git push origin :serverfix
	  To git@github.com:schacon/simplegit.git
	  - [deleted]         serverfix
 	```

### 3.6 Git 分支 - 分支的衍合

* rebase的例子

	```
	$ git checkout experiment
	$ git rebase master
	First, rewinding head to replay your work on top of it...
	Applying: added staged command
	```

  