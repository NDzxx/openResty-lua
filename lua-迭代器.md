#Lua 迭代器

##泛型 for 迭代器
```lua
for k, v in pairs(t) 
    do print(k, v) 
end

```

##无状态的迭代器
无状态的迭代器是指不保留任何状态的迭代器，因此在循环中我们可以利用无状态迭代器避免创建闭包花费额外的代价。
每一次迭代，迭代函数都是用两个变量（状态常量和控制变量）的值作为参数被调用，一个无状态的迭代器只利用这两个值可以获取下一个元素。  

这种无状态迭代器的典型的简单的例子是ipairs，他遍历数组的每一个元素。
以下实例我们使用了一个简单的函数来实现迭代器，实现 数字 n 的平方：

```lua
function square(iteratorMaxCount,currentNumber)
   if currentNumber<iteratorMaxCount
   then
      currentNumber = currentNumber+1
   return currentNumber, currentNumber*currentNumber
   end
end

for i,n in square,3,0
do
   print(i,n)
end

```
##多状态迭代器

很多情况下，迭代器需要保存多个状态信息而不是简单的状态常量和控制变量，最简单的方法是使用闭包，还有一种方法就是将所有的状态信息封装到table内，将table作为迭代器的状态常量，因为这种情况下可以将所有的信息存放在table内，所以迭代函数通常不需要第二个参数。



以下实例我们创建了自己的迭代器：
```lua
array = {"Lua", "Tutorial"}

function elementIterator (collection)

 local index = 0

 local count = #collection

 -- 闭包函数

 return function ()

 index = index + 1

 if index <= count

 then

 -- 返回迭代器的当前元素

 return collection[index]

 end

 end

end

for element in elementIterator(array)

do

 print(element)

end


```
