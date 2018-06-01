asyncio的基本语法和使用

协程是一个对象,不能直接运行,需要添加到事件循环之中,由事件循环来调用执行协程.

基本的概念:
`event_loop`事件循环：将协程注册到事件循环中

程序开启一个无限的循环，程序员会把一些函数注册到事件循环上。当满足事件发生的时候，调用相应的协程函数。

`coroutine` ：协程对象，指一个使用async关键字定义的函数，它的调用不会立即执行函数，而是会返回一个协程对象。协程对象需要注册到事件循环，由事件循环调用。

`task` ：对协程对象进一步封装,用于记录多个需要协程对象和协程的状态信息.`asyncio.ensure_future(coroutine)`和`loop.create_task(coroutine)`是两种创建`task`的方式


`future`： 代表将来执行或没有执行的任务的结果。它和task上没有本质的区别

`async`:用于将一个函数定义为一个协程对象.
```python
async def func():  # 定义协程
        pass
```
`await`：当协程运行时遇到`await`会挂起(跳出/暂停)当前协程,执行下一个协程.






`asyncio.get_event_loop`
`run_until_complete`

创建简单的协程的步骤:
1.调用`get_event_loop`创建一个事件循环`loop`
2.调用`create_task`方法,将需要执行的协程对象放入`task`中
3.调用`run_until_complete`,将`task`中的协程注册到事件循环`loop`中
4.
5.
