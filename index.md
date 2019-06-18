# Event Loop

JS 在执行的过程中会产生执行环境，这些执行环境会被顺序的加入到执行栈中。如果遇到异步的代码，会被挂起并加入到 Task（有多种 task） 队列中。一旦执行栈为空，Event Loop 就会从 Task 队列中拿出需要执行的代码并放入执行栈中执行，所以本质上来说 JS 中的异步还是同步行为。

不同的任务源会被分配到不同的 Task 队列中，任务源可以分为 `微任务（microtask）` 和 `宏任务（macrotask）`。在 ES6 规范中，`microtask` 称为 `jobs`，`macrotask` 称为 `task`。`异步操作中微任务快于宏任务`。

微任务包括 `process.nextTick `，`promise` ，`Object.observe` ，`MutationObserver`

宏任务包括 `script` ， `setTimeout` `，setInterval` `，setImmediate` ，`I/O` ，`UI rendering`

一次 Event loop 顺序

1. 执行同步代码，这属于宏任务
2. 执行栈为空，查询是否有微任务需要执行
3. 执行所有微任务
4. 必要的话渲染 UI
5. 然后开始下一轮 Event loop，执行宏任务中的异步代码