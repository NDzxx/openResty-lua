#模块
模块类似于一个封装库 
Lua 的模块是由变量、函数等已知元素组成的 table，因此创建一个模块很简单，就是创建一个 table，然后把需要导出的常量、函数放入其中，最后返回这个 table 就行。

以下为创建自定义模块 module.lua，文件代码格式如下： 

```lua
-- 文件名为 module.lua

-- 定义一个名为 module 的模块

module = {}

-- 定义一个常量

module.constant = "这是一个常量"

-- 定义一个函数

function module.func1()

 io.write("这是一个公有函数！\n")

end

local function func2()

 print("这是一个私有函数！")

end

function module.func3()

 func2()

end

return module

```
##require函数
Lua提供了一个名为require的函数用来加载模块。要加载一个模块，只需要简单地调用就可以了。例如： 

```lua
local m = require("module")

print(m.constant)

m.func3()

```
##加载机制
```lua
local m = require("module/module")//当前目录下的module文件夹的module模块

print(m.constant)

m.func3()

```