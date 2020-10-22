# JavaScript中的EventLoop



## JS的运行机制

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6897a203c68148a0964c58164395b4d2~tplv-k3u1fbpfcp-zoom-1.image)

先来解释上图中出现的几个单词所要表达的含义。

Heap(堆)、Stack(栈)、Queue(队列)、Event Loop(事件轮询)

### 程序中的堆栈队列

**Heap(堆)**

堆， 是一种动态存储结构，是利用完全二叉树维护的一组数据，堆分为两种，一种为**最大堆**，一种为**最小堆**，将根节点最大的堆叫做**最大堆**或**大根堆**，根节点最小的堆叫做**最小堆**或**小根堆**。 堆是**线性数据结构**，相当于**一维数组**，有唯一后继。

如最大堆

![image-20200930152008918](/Users/gaozhixu/Library/Application Support/typora-user-images/image-20200930152008918.png)

**栈（Stack）**

栈在程序中的设定是限定仅在表尾进行插入或删除操作的线性表。 栈是一种数据结构，它按照**后进先出**(`LIFO: last-in-first-out`)的原则存储数据，先进入的数据被压入栈底，最后的数据在栈顶，需要读数据的时候从栈顶开始弹出数据。 栈是只能在某一端插入和删除的特殊线性表。

![image-20200930152050494](/Users/gaozhixu/Library/Application Support/typora-user-images/image-20200930152050494.png)

**队列（Queue**）

队列特殊之处在于它只允许在表的前端（`front`）进行删除操作，而在表的后端（`rear`）进行插入操作，和栈一样，队列是一种操作受限制的线性表。 进行插入操作的端称为队尾，进行删除操作的端称为队头。  队列中没有元素时，称为**空队列**。

队列的数据元素又称为队列元素。在队列中插入一个队列元素称为入队，从队列中删除一个队列元素称为出队。因为队列只允许在一端插入，在另一端删除，所以只有最早进入队列的元素才能最先从队列中删除，故队列又称为**先进先出**（`FIFO: first-in-first-out`）

![image-20200930152111055](/Users/gaozhixu/Library/Application Support/typora-user-images/image-20200930152111055.png)

### js中的堆栈队列

下面我解释下**JavaScript语言**中的堆、栈、队列。

**堆**

堆， 动态分配的内存，大小不定也不会自动释放，存放**引用类型**，指那些可能由多个值构成的对象，保存在堆内存中，包含引用类型的变量，实际上保存的不是变量本身，而是指向该对象的指针。可以简单理解为存储代码块。

堆的作用：存储引用类型值的数据

```js
let obj = {
    name: '北歌'，
    puslic: '前端自学驿站'
}

let func = () => {
    console.log('hello world')
}
```

![image-20200930152134076](/Users/gaozhixu/Library/Application Support/typora-user-images/image-20200930152134076.png)

**栈**

js中的栈准确来将应该叫调用栈(EC Stack)，会自动分配内存空间，会自动释放，存放**基本类型**，简单的数据段，占据固定大小的空间。

栈的作用：存储基本类型值，还有一个很要的作用。**提供代码执行的环境**

**队列**

js中的队列可以叫做**任务队列**或**异步队列**，任务队列里存放各种异步操作所注册的回调，里面分为两种任务类型，宏任务(`macroTask`)和微任务(`microTask`)。

好，下面可以回到正题上来了。

### 为什么会出现Event Loop

总所周知JS是一门单线程的非阻塞脚本语言，Event Loop就是为了解决JS异步编程的一种解决方案。

### JS为什么是单线程语言，那它是怎么实现异步编程(非阻塞)运行的

第一个问题： JavaScript的诞生就是为了处理浏览器网页的交互（DOM操作的处理、UI动画等),  设计成单线程的原因就是不想让浏览器变得太复杂，因为多线程需要共享资源、且有可能修改彼此的运行结果（两个线程修改了同一个DOM节点就会产生不必要的麻烦），这对于一种网页脚本语言来说这就太复杂了。

第二个问题： JavaScript是单线程的但它所运行的宿主环境—浏览器是多线程，浏览器提供了各种线程供Event Loop调度来协调JS单线程运行时不会阻塞。

### 小结

先总结一波个人对于JS运行机制的理解：

> 代码执行开启一个全局调用栈(主栈)提供代码运行的环境，在执行过程中同步任务的代码立即执行，遇到异步任务将异步的回调注册到任务队列中，等待同步代码执行完毕查看异步是否完成，如果完成将当前异步任务的回调拿到主栈中执行

## 进程和线程

进程：进程是 CPU 资源分配的最小单位(是能拥有资源和独立运行的最小单位)

线程：线程是 CPU 调度的最小单位(线程是建立在进程的基础上的一次程序运行单位)

对于进程和线程并没有确切统一的描述，可以简单的理解：

> 比如一个应用程序: 如QQ、浏览器启动时会开启一个进程，而该进程可以有多个线程来进行资源调度和分配，达到运行程序的作用。
>
> 更通俗的话讲：打开QQ应用程序开启了进程来运行程序(QQ), 有多个线程来进行资源调度和分配(多个线程来分配打开QQ所占用的运存)，达到运行程序(QQ)的作用.

用操作系统来作个例子：

![image-20200930152213854](/Users/gaozhixu/Library/Application Support/typora-user-images/image-20200930152213854.png)

> 线程依赖进程，一个进程可以有一个或者多个线程，但是线程只能是属于一个进程。

### JS的单线程

js的单线程指的是javaScript引擎只有一个线程

单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。如果前一个任务耗时很长，后一个任务就不得不一直等着。 js 引擎执行异步代码而不用等待，是因有为有任务队列和事件轮询。

- 任务队列：任务队列是一个先进先出的队列，它里面存放着各种任务回调。
- 事件轮询：事件轮询是指主线程重复从任务队列中取任务、执行任务的过程。

### 浏览器的多线程

1. GUI 渲染线程
   - 绘制页面，解析 HTML、CSS，构建 DOM 树，布局和绘制等
   - 页面重绘和回流
   - 与 JS 引擎线程互斥，也就是所谓的 JS 执行阻塞页面更新
2. JS 引擎线程
   - 负责 JS 脚本代码的执行
   - 负责准执行准备好待执行的事件，即定时器计数结束，或异步请求成功并正确返回的事件
   - 与 GUI 渲染线程互斥，执行时间过长将阻塞页面的渲染
3. 事件触发线程
   - 负责将准备好的事件交给 JS 引擎线程执行
   - 多个事件加入任务队列的时候需要排队等待(JS 的单线程)
4. 定时器触发线程
   - 负责执行异步的定时器类的事件，如 setTimeout、setInterval
   - 定时器到时间之后把注册的回调加到任务队列的队尾
5. HTTP 请求线程
   - 负责执行异步请求
   - 主线程执行代码遇到异步请求的时候会把函数交给该线程处理，当监听到状态变更事件，如果有回调函数，该线程会把回调函数加入到任务队列的队尾等待执行

## Event Loop

呼，终于回到正题了！

对于事件轮询上面其实已经解释的很清楚了：

> 事件轮询就是解决javaScript单线程对于异步操作的一些缺陷，让 javaScript做到既是**单线程**，又绝对**不会阻塞**的核心机制，是用来协调各种事件、用户交互、脚本执行、UI 渲染、网络请求等的一种机制。

### 浏览器中的Eveent Loop执行顺序

[Processing model](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model)规范定义了`Eveent Loop`的循环过程：

一个Eveent Loop只要存在，就会不断执行下边的步骤：

- 1.在tasks(任务)队列中选择最老的一个task,用户代理可以选择任何task队列，如果没有可选的任务，则跳到下边的microtasks步骤。
- 2.将上边选择的task设置为[正在运行的task](https://html.spec.whatwg.org/multipage/webappapis.html#currently-running-task)。
- 3.Run: 运行被选择的task。
- 4.将Eveent Loop的[currently running task](https://html.spec.whatwg.org/multipage/webappapis.html#currently-running-task)变为null。
- 5.从task队列里移除前边运行的task。
- 6.Microtasks: 执行[microtasks任务检查点](https://html.spec.whatwg.org/multipage/webappapis.html#perform-a-microtask-checkpoint)。（也就是执行microtasks队列里的任务）
- 7.更新渲染（Update the rendering）：可以简单理解为浏览器渲染...
- 8.如果这是一个worker event loop，但是没有任务在task队列中，并且[WorkerGlobalScope](https://html.spec.whatwg.org/multipage/workers.html#workerglobalscope)对象的closing标识为true，则销毁Eveent Loop，中止这些步骤，然后进行定义在[Web workers](https://html.spec.whatwg.org/multipage/workers.html#workers)章节的[run a worker](https://html.spec.whatwg.org/multipage/workers.html#run-a-worker)。
- 9.返回到第一步。

Eveent Loopp会不断循环上面的步骤，概括说来：

- `Eveent Loop`会不断循环的去取`tasks`队列的中最老的一个task(可以理解为宏任务）推入栈中执行，并在当次循环里依次执行并清空`microtask`队列里的任务。
- 执行完`microtask`队列里的任务，有**可能**会渲染更新。（浏览器很聪明，在一帧以内的多次dom变动浏览器不会立即响应，而是会积攒变动以最高60HZ(大约16.7ms每帧)的频率更新视图）

### 宏任务和微任务优先问题

> 在任务对列(queue)中注册的异步回调又分为两种类型，宏任务和微任务。我们为了方便理解可以认为在任务队列中有宏任务队列和微任务队列。宏任务队列有多个，微任务只有一个

- 宏任务(macro Task)
  - script(整体代码)
  - setTimeout/setInterval
  - setImmediate(Node环境)
  - UI 渲染
  - requestAnimationFrame
  - ....
- 微任务(micro Task)
  - Promise的then()、catch()、finally()里面的回调
  - process.nextTick(Node 环境）
  - ...

个人理解的执行顺序：

1. 代码从开始执行调用一个全局执行栈，script标签作为宏任务执行

2. 执行过程中同步代码立即执行，异步代码放到任务队列中，任务队列存放有两种类型的异步任务，宏任务队列，微任务队列。

3. 同步代码执行完毕也就意味着第一个宏任务执行完毕(script)

   - 1、先查看任务队列中的微任务队列是否存在宏任务执行过程中所产生的微任务

     ​	1-1、有的话就将微任务队列中的所有微任务清空

     ​	2-2、微任务执行过程中所产生的微任务放到微任务队列中，在此次执行中一并清空

   - 2、如果没有再看看宏任务队列中有没有宏任务，有的话执行，没有的话事件轮询第一波结束

     ​	2-1、执行过程中所产生的微任务放到微任务队列

     ​	2-2、完成宏任务之后执行清空微任务队列的代码

![image-20200930152246734](/Users/gaozhixu/Library/Application Support/typora-user-images/image-20200930152246734.png)

所以是宏任务优先，在宏任务执行完毕之后才会来一次性清空任务队列中的所有微任务。

```javascript
// => 代码一执行就开始执行了一个宏任务-宏0
console.log('script start'); 

setTimeout(() => { // 宏 1
  console.log('北歌');
}, 1 * 2000);

Promise.resolve()
    .then(function() { // 微1-1
      console.log('promise1');
    })
    .then(function() { // 微1-4 => 这个then中的会等待上一个then执行完成之后得到其状态才会向Queue注册状态对应的回调，假设上一个then中主动抛错且没有捕获，那就注册的是这个then中的第二个回调了。
      console.log('promise2'); 
    });


async function foo() {
  await bar() // => await(promise的语法糖)，会异步等待获取其返回值
  // => 后面的代码可以理解为放到异步队列微任务中。 这里可以保留疑问后面会详细说
  console.log('async1 end') // 微1-2
}
foo()

function bar() {
  console.log('async2 end') 
}

async function errorFunc () {
  try {
    await Promise.reject('error!!!')
  } catch(e) {
      // => 从这后面开始所有的代码可以理解为放到异步队列微任务中
    console.log(e)  // 微1-3
  }
  console.log('async1');
  return Promise.resolve('async1 success')
}
errorFunc().then(res => console.log(res)) // 微1-5

console.log('script end');

```

#### 画图分析

相信通过上面的讲解你们应该都能明白，为了让你们更深刻的理解，形成较强的场景印象，我画了个动图

![img](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/34fd0e7689da430aa0d6f6975d0774b8~tplv-k3u1fbpfcp-zoom-1.image)

