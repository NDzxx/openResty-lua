#Lua 元表(Metatable)

在 Lua table 中我们可以访问对应的key来得到value值，但是却无法对两个 table 进行操作。

因此 Lua 提供了元表(Metatable)，允许我们改变table的行为，每个行为关联了对应的元方法。

##设置元表
```lua
mytable = setmetatable({},{})

//返回对象元素
getmetatable(mytable) -- 这回返回mymetatable

```
##为表添加操作符
| 模式| 描述 |
| --- | --- |
| -add| 对应的运算符 '+'. |
| -sub| 对应的运算符 '-'. |
| -mul| 对应的运算符 '*'. |
| -div| 对应的运算符 '/'. |
| -mod| 对应的运算符 '%'. |
| -unm| 对应的运算符 '-'. |
| -connect| 对应的运算符 '..' |
| -eq| 对应的运算符 '==' |
| -lt| 对应的运算符 '<' |
| -le| 对应的运算符 '<=' |
```lua
-- 计算表中最大值，table.maxn在Lua5.2以上版本中已无法使用

-- 自定义计算表中最大值函数 table_maxn

function table_maxn(t)

 local mn = 0

 for k, v in pairs(t) do

 if mn < k then

 mn = k

 end

 end

 return mn

end

-- 两表相加操作

mytable = setmetatable({ 1, 2, 3 }, {

 __add = function(mytable, newtable)

 for i = 1, table_maxn(newtable) do

 table.insert(mytable, table_maxn(mytable)+1,newtable[i])

 end

 return mytable

 end

})

secondtable = {4,5,6}

mytable = mytable + secondtable

 for k,v in ipairs(mytable) do

print(k,v)

end

```
##__call 元方法
...





##__tostring 
__tostring 元方法用于修改表的输出行为。 

