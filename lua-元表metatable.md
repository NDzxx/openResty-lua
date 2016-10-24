#Lua 元表(Metatable)

在 Lua table 中我们可以访问对应的key来得到value值，但是却无法对两个 table 进行操作。

因此 Lua 提供了元表(Metatable)，允许我们改变table的行为，每个行为关联了对应的元方法。

##设置元表
```lua
mytable = setmetatable({},{})

//返回对象元素
getmetatable(mytable) -- 这回返回mymetatable

```

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

##__call 元方法








