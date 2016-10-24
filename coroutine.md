#协程

coroutine.create() 创建coroutine，返回coroutine， 参数是一个函数，当和resume配合使用的时候就唤醒函数调用

coroutine.resume() 重启coroutine，和create配合使用

coroutine.yield() 挂起coroutine，将coroutine设置为挂起状态，这个和resume配合使用能有很多有用的效果

coroutine.status() 查看coroutine的状态

注：coroutine的状态有三种：dead，suspend，running，具体什么时候有这样的状态请参考下面的程序

coroutine.wrap（） 创建coroutine，返回一个函数，一旦你调用这个函数，就进入coroutine，和create功能重复

coroutine.running() 返回正在跑的coroutine，一个coroutine就是一个线程，当使用running的时候，就是返回一个corouting的线程号
