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

### HelloWorld Lua

```
--这是一个lua的语句
print("Hellolua")

a = [[
asdhaisfhaiufhasiudhasfhpf
asjdoaishdoas
]]

print(a)

--[[
	1.数字类型
	2.字符类型
	3.thread类型
	4.function类型
	5.table
	6.其他类型
]]

a = function(var)
	print("user input is "..var)
end

a("I'm A")
print(a)

myTable = {
    12,
    13
}

for k,v in pairs(myTable) do
    print(k,v)
end

--如果在一个function函数中创建的变量也是global(没有使用local关键字)，那么意味着它是一个全局的global变量

```

### 在lua中只有false和nil为假

### and
 
如果第一个我们要去计算的操作数为假的话，就返回第一个操作数，反之返回第二个数

### or

如果第一个为真，返回第一个值，反之返回第二个

```
print(1 or 5) -->1
print(0 or 5) -->0
print(nil or 5) -->5
print(false or 5) -->5
```
### not 永远返回的只是true和false
```
print(not nil)
print(not 1)
print(not 0)
print(not false)
```
### while 
```
m_table {1,2,3}
local index=1
while m_table[index] do
     print(m_table[index])
     index = index +1
end
```
### repeat(相当于其他语言中的do while)
```
local n = 1
repeat
    print("n = "..n)
    n = n + 1
until n==3
```
### for 
```
for i=1,10
```
### Table
```
s ="ok"
mytable ={
	1,
	2,
	k =12
	4
}
mytable[s] =10

print (mytable["k"])
print (mytable[s])

print(mytable.k)  --在lua中table.k相当于table["k"]

-- a.x a[x] 的区别
--[[
	a.x 等价于 a["x"]
	a[x]以变量x的值来索引table
]]

-- 第一种遍历方式

for i=1,#mytable do
	print("value is ==>"..mytable[i])
end

--第二种遍历方式 for ipairs 使用的方式与普通for获取等同，都是按照当前的索引来去迭代并显示值的
for i,v in ipairs(mytable) do
	print(i,v)
end

--第三种遍历方式 for pairs pairs 迭代器是完全将所有的值显示出来，并且要注意table中的索引并不完全是按照书写顺序来的
for k,v in pairs(mytable) do 
	print(k,v)
end

```

### IO 

1.写文件的方式

```
file  = io.open("t.txt",'r')
myText = "Hello"
file:write(myText)
file:close

local function read_files(fileName)
	-- 参数r表示只读方式打开，a表示追加，w表示写入，b表示打开二进制
    local f = assert(io.open(fileName,'r'))
    -- \*all 表示读取所有的文件内容,\*line表示读取一行，
    -- \*number读取一个数字 或者<num>读取一个不超过<num>个数的字符
	local content = f:read("*all")
    f:close
    return content
end

local rlt = read_files("nameList.txt")
print(rlt)

```

2.读文件的方式

```
  local f  = assert(io.open("t.txt",'a'))
  local string = f:read("*all")
  f:close()
  
  local function write_content(fileName,content)
  	local f = assert(io.open(fileName,'a'))
  	f:write(content)
  	f:close()
  end
  
  write_content("ok.txt","Hello world\n")
  
  local long_txt ={
  	this is a long text
  }
  
  write_content("ok.txt",long_txt)
  
```
  
### Lua串行化
```
function serialize(o)
	if type(o)=="number" then
		io.write(o)
	elseif  type(o)=="string" then
		io.write(string.format("%q",o))
	else 
		print(o)
	end
end

--保存无环的table

function n_serialize(o)
	if type(o)=="number" then
		io.write(o)
	elseif  type(o)=="string" then
		io.write(string.format("%q",o))
	elseif type(o)=="table" then
		io.write("{\n")
		for k,v in pairs(o) do
			io.write("  ",k," = ")
			n_serialize(v)
			io.write(",\n")
		end
		io.write("}\n")
	end
end

-- serialize('abc')
serialize("def")

n_serialize{a=12,b="lua"}
```
### 面向对象
```
--如何在lua中实现面向对象编程

Account ={
	balance = 12
}

-- 以.的方式命名的方法需要显示的传递自身的引用self
function Account.count( self,v )
	self.balance = self.balance+v
	print("value is "..self.balance)
end

-- ：这种方式隐式的帮我传递进了self
function Account:mytostring()
	print("结果是"..self.balance)
end

tt = Account;
--通过：调用方法同上
tt:count(12)
tt:mytostring()

local myClass = require("myClass")
myClass:showName()

```

myClass.lua

```
--通常我们把成员变量放在table中，将方法
--写table的外面
local myClass = {

	name = "Li xiaolong"
	
	--[[ 类似与下面的写在外面，但是没有下面的方式明了
	showName = new function()
	--body
	end
	]]
}

function myClass:showName()
	print(self.name)
end

return myClass
```

### 继承
```
--下面是模仿继承
Account  ={}

function Account:new( o ) 
	o  = o or {}
	setmetatable(o,self)
	self.__index = self
	return o
end

function Account:show(v )
	print(self.bb+v) --相当于访问父类中的bb,如果没有回报错
end

a  = Account:new{ bb =111 }
a : show( 1.0 )
```

#### 多继承

```
local function search(k,plist)
  for i=1, #plist do
    local v = plist[i][k]
    if v then
      return v
    end
  end
end

function createClass(...)
  local c = {}
  local parents = {...}

  setmetatable(c,{__index = function (t,k)
    return search(k,parents)
  end})

  c.__index = c

  function c:new(o)
    o = o or {}
    setmetatable(o,c)
    return o
  end

end
```

### 面向对象私密性实现方式
```
function newAccout(initlizedBanlance)
  local self = {balance=initlizedBanlance}
  local show = function(v)
    self.balance =self.balance -v
  end
  local getBanlance = function ()
    return self.balance
  end

  return {
    show =show,
    getBanlance = getBanlance
  }
end

acc = newAccout(200)
print(acc.getBanlance())
acc.show(100)
print(acc.getBanlance())

-- 单一方法演示

function newObject(value )
  -- body
  return function(action,v )
    -- body
    if action=="get" then return value
    elseif action=="set" then value =v
    else 
      error("invalid action")
    end
  end
end

d = newObject(0)
print(d("get"))
d("set",10)
print(d("get"))
```

