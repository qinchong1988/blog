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