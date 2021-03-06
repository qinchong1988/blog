#Git指令快速查看

### 1.1 Git config

git https 无法获取，请配置本地的 git，关闭 https 验证

```
git config --global http.sslVerify false
```

  ```
	[alias]
    last = log -1 HEAD
    ci = commit -a -v
    co = checkout
    br = branch
    st = status
    throw = reset --hard HEAD
  	throwh = reset --hard HEAD^
  ```

### 1.2 Git hotfix小技巧

  当在开发的时候突然发现一个小bug，但是自己的feature又开发到一半，这个时候可以使用git stash暂存之前的修改,待HotFix之后在利用git stash apply
  还原之前的开发.

### 2.4 Git 基础-[撤消操作](http://git-scm.com/book/zh/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C)


* 修改最后一次提交```$ git commit --amend```
* 取消已经暂存的文件```$ git reset HEAD benchmarks.rb```
* 取消对文件的修改```$ git checkout -- benchmarks.rb```

### 2.5 Git 基础 - 远程仓库的使用
* 查看当前配置有哪些远程仓库，可以用```git remote```命令(可以加上```-v```)
* 添加远程仓库```git remote add [shortname] [url]```

  ```$ git remote add pb git://github.com/paulboone/ticgit.git```
  
* 抓取所有 Paul 有的，但本地仓库没有的信息```git fetch pb```
* 从远程仓库抓取数据```$ git fetch [remote-name]```
* 推送数据到远程仓库```git push [remote-name] [branch-name]```
* 查看远程仓库信息```git remote show [remote-name]```

  ```
  $ git remote show origin
  * remote origin
  URL: git://github.com/schacon/ticgit.git
  Remote branch merged with 'git pull' while on branch master
    master
  Tracked remote branches
    master
    ticgit
    ```
* 远程仓库的重命名和删除```$ git remote rename pb paul``` and ```git remote rm paul```


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

### 3.6 Git 分支 - [分支的衍合](http://git-scm.com/book/zh/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E8%A1%8D%E5%90%88)


* rebase的例子

	```
	$ git checkout experiment
	$ git rebase master
	First, rewinding head to replay your work on top of it...
	Applying: added staged command
	```
	
	

  
