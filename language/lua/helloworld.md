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
