### 开发环境搭建

#### 编辑器使用Sublime text 2 

1. 点击工具栏，Tool->Build System->New Build System
2. 在新建的脚本文件中添加以下代码

    ```
	{
   	  "cmd": ["lua", "$file"],
  	  
  	  "file_regex": "^(?:lua:)?[\t ](...*?):([0-9]*):?([0-9]*)",
    
  	  "selector": "source.lua"
    
	}
	```
3. ctrl + s将文件保存为lua.sublime-build,保存到默认位置即可。
4. 这个时候Tool->Build System，勾选lua为默认选项即可。
5. ctrl + n新建一个lua文件，输入
print("hello world")
6. ctrl + b运行，这个时候我们就能在控制台看到输出"hello world"啦！
如果提示 No such file or directory ... 则在刚才的配置中加入一行："path": "/usr/local/bin"，这个是lua的安装路径

	```
	{
   	 "cmd": ["lua", "$file"],
    
     "file_regex": "^(?:lua:)?[\t ](...*?):([0-9]*):?([0-9]*)",
   	 
  	 "path": "/usr/local/bin",
	
   	 "selector": "source.lua"
	}
	```
	
#### 这里要讲一下如何安装插件：

1. 打开 Sublime Text 2，按下 Control + ` 调出 Console
2. 将以下代码粘贴进命令行中并回车：

>import urllib2,os; pf='Package Control.sublime-package'; ipp=sublime.installed_packages_path(); os.makedirs(ipp) if not os.path.exists(ipp) else None; urllib2.install_opener(urllib2.build_opener(urllib2.ProxyHandler())); open(os.path.join(ipp,pf),'wb').write(urllib2.urlopen('http://sublime.wbond.net/'+pf.replace(' ',' ')).read()); print 'Please restart Sublime Text to finish installation'

3. 关闭并再一次打开sublime text，并command＋shift＋p 调出插件配置。
4. 输入 instal  等待Download 可安装的插件列表
5. 输入lua 查找，找到后选中并回车键确认，等待安装

在 PackageControl中install Lua Dev SublimeLinter-lua