# js执行机制

[aa](https://juejin.im/post/6844903512845860872)


<img src="./img/执行栈.jpg" width=500px>

同步和异步任务分别进入不同的执行"场所"，同步的进入主线程，异步的进入Event Table并注册函数。
当指定的事情完成时，Event Table会将这个函数移入Event Queue。
主线程内的任务执行完毕为空，会去Event Queue读取对应的函数，进入主线程执行。
上述过程会不断重复，也就是常说的Event Loop(事件循环)。

怎么知道主线程执行栈为空啊？js引擎存在monitoring process进程，会持续不断的检查主线程执行栈是否为空
一旦为空，就会去Event Queue那里检查是否有等待被调用的函数。



### 宏队列与微队列

Js 中，有两类任务队列：宏任务队列（macro tasks）和微任务队列（micro tasks）。宏任务队列可以有多个，微任务队列只有一个
宏任务：script（全局任务）, setTimeout, setInterval, setImmediate, I/O, UI rendering.
微任务：process.nextTick （node.js中进程相关的对象）, Promise, Object.observer, MutationObserver。

<img src="./img/宏任务微任务.jpg" width=500px>