#Lua 元表(Metatable)

在 Lua table 中我们可以访问对应的key来得到value值，但是却无法对两个 table 进行操作。

因此 Lua 提供了元表(Metatable)，允许我们改变table的行为，每个行为关联了对应的元方法。

##设置元表
```lua
mytable = setmetatable({},{})

//返回对象元素
getmetatable(mytable) -- 这回返回mymetatable

```




