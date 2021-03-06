
## Reading
### Nodejs event loop, callback
- [ ] https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/
- [ ] 带你彻底弄懂Event Loop https://juejin.im/post/6844903670291628046
- [x] EventLoop queue order https://medium.com/@jain.sm/nodejs-event-loop-and-libuv-6bf3668c482

### Nodejs source code
- [x] https://medium.com/@berkaybindebir/deep-dive-node-js-762552ad31a8
- [ ] https://github.com/yjhjstz/deep-into-node
- [ ] V8 之旅： 垃圾回收器 http://newhtml.net/v8-garbage-collection/ 
- [ ] node源码粗读（10）：通过fs.write来看异步I/O和回调执行的整体流程 https://cnodejs.org/topic/5ac49eca96f344940fbbad43
- [ ] node源码粗读(1)：一个简单的nodejs文件从运行到结束都发生了什么 https://cnodejs.org/topic/5a012ffe84ed7ceb219ea7a9

## Javascript evet loop, callback
- [x] https://medium.com/@Rahulx1/understanding-event-loop-call-stack-event-job-queue-in-javascript-63dcd2c71ecd
- [x] https://dev.to/khaosdoctor/node-js-under-the-hood-2-understanding-javascript-48cn
- [x] https://gist.github.com/jesstelford/9a35d20a2aa044df8bf241e00d7bc2d0

## v8
V8 is a Javascript engine written in C++ that created for using in the Chrome browser
It’s compiles and executes Javascript code, handles call stack, handles memory allocation, handles garbage collecting
But V8 cannot handle DOM because there is no browser.

### Garbage collection

Difficulties: An object is a candidate for garbage collection when it is unreachable from the root node, so not referenced by the root object or any other active objects. Root objects can be global objects, DOM elements or local variables.

Memory usage:
1. Code area
2. The Objects heap has two main segments, the New Space and the Old Space.

Technical issues:
1. how to distinguish pointers and objects
2. objects are moved frequently, so as pointers

Reference:
https://github.com/yjhjstz/deep-into-node/blob/master/chapter2/chapter2-0.md

## How does node.js works
1. run “node index.js” for executing our Node JS code
2. Node creates a new process and executes our codes into an event loop
3. Each instance of Node has own event loop (run in one single thread, called the main thread) and each instance will run in a single thread in CPU.
4. Node.js listens and passes every concurrent traffic in a queue, which will be executed by an event loop.
5. Event loop check method, if sync do it now, else pass the async method to theadpool and let c++ do it
6. Event then will look at the callback queue and pick the call back function
7. If all pending tasks are done, event loops run all close callbacks and exit from the loop.

## libuv
although event loops is single-thread

the low-level operations like reading a file or requesting an HTTP server works in another thread in the “Thread Pool” and this is handling by libuv.

### How does a single thread handle asynchronous code in Node.js?
By using `libuv`, node can ask os to do something like open and read a file. If it takes sometime for os to work, node will continue it's task. Then the os will remind node in the event queue once it finished its task.


## Call stack
The call stack is a Last-In, First-Out (return goes back to the point of the most recent call) data structure containing the address at which function will resume and often local variables and parameters from each call

## Module Types
Node.js includes three types of modules:

1. Core Modules like (`http`, `fs`)
2. Local Modules
4. Third Party Modules

reference: https://medium.com/javascript-in-plain-english/node-call-stack-explained-fd9df1c49d2e
