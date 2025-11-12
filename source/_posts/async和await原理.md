---
title: async和await原理
tags: [async]
---
### async/await的本质是Generator生成器函数+Promise的语法糖,它使用一种看起来像'同步'的写法,来执行真正的异步操作.
 #### 为了理解它,分三步看:
 1. async/await做了什么?
 2. 它的前身:Generator函数
 3. 它们是如何结合到一起?

 ### 1. async/await的行为和转换
 - async函数:总是返回一个Promise对象.
 - 如果函数内部fanhui一个值,这个值会被Promise.resolve()包装
 - 如果函数内部抛出一个错误,会返回一个被reject的Promise对象
 - await表达式:只能在async函数内部:
 - 如果await后面是一个Promise,它会暂停执行,等待这个Promise完成(fulfilled或rejected),然后恢复执行并返回结果
 - 如果await后面是一个非Promise值(比如await 123),它会把这个值转换为一个已解决的Promise,然后执行同样的暂时和恢复逻辑
 #### 这个暂停和恢复是如何实现的呢?答案是Generator

 ### 2. Generator函数
 #### Generator函数(生成器函数)是ES6引入的,它可以通过yield关键字暂停函数执行,并通过.next()方法恢复执行
 ```javascript
 function* gen(){
    console.log('start');
    let result =yield '等待的值'; //第一次暂停
    console.log('恢复执行,拿到值',result); //从外部拿到值后恢复
    result '结束';
 }

 const g = gen(); //执行gen() 不会立即运行函数体,而是返回一个迭代器对象
 const step1 = g.next(); //输出'开始',执行到yield处暂停,返回{value: '等待的值', done: false}
 console.log(step1);

 const step2 = g.next('传给yield的值'); //从上次暂停处恢复,将'传给yield的值'赋值给result变量
 //输出'恢复执行,拿到值:传给yield的值'
 console.log(step2); //输出{value: '结束', done: true}
 ```

 #### 关键特性
 - yield可以看作是一个'断点'
 - 执行权在函数内外可以进行交换
 - 通过.next(value)方法,可以从外部函数内部传递数据

 ### 实现原理
 #### 
 1. 转换:当javascript引擎遇到async/await时,它会将async函数转换为Generator函数.await转换为yield
 2. 自动执行:引擎会提供一个类似run函数的自动执行器,这个执行器接管了Generator迭代器的控制权
 3. Promise驱动:
    - 执行器调用.next()启动Generator函数
    - 每当遇到yield(await)一个Promise,执行器就暂停并订阅这个Promise
    - 当Promise完成(resovle或reject)时,执行器会:
        - 成功(resolve):调用 .next(resolvedValue),将值传回Generator函数内部,并恢复执行
        - 失败(reject):调用.throw(rejectedError),在Generator函数内部抛出错误,可以被try-catched捕获
4. 返回值:整个async函数返回的Promise,由这个自动执行器管理,当Generator函数执行完毕(result.done===true),执行器会resolve或reject这个最终的Promise
#### 总结:async/await的原理是:利用Generator的暂停/恢复特性,通过一个自动执行器,将异步的Promise用同步的代码写法表达出来,从而实现异步操作的同步化. 