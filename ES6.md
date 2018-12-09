# ES6

### Promise

一个 Promise 对象表示一种操作，这种操作已经产生了或最终会产生一个值。
Promises 提供一种健壮的方式来封装异步操作的结果，以减少回调深层嵌套的问题的伤害（回调深渊）。

一个 Promise 可以有3种状态：

 - pending -- 下层操作还未完成， promise 正在等待。
 - fulfilled -- 操作已经完成，promise 完成，并且已经有值。类似于从同步函数返回了一个值。
 - rejected -- 运行过程中产生了错误，promise 被拒绝，并且带有一个错误原因。类似于同步操作中抛出异常。

当一个 Promise 处于fulfilled 或 rejected状态时，我们说它被 处理完成了（或解决了），一旦被处理了，它就不可变了，它的状态也不能改变了。
Promise 的 then 和 catch 方法可以被用于附带上执行完成时执行的回调，这些回调也会带着返回值或错误原因。
```JavaScript
const promise = new Promise((resolve, reject) => {
    // Perform some work (possibly asynchronous)
    // ...

    if (/* Work has successfully finished and produced "value" */) {
        resolve(value);
    } else {
        // Something went wrong because of "reason"
        // The reason is traditionally an Error object, although
        // this is not required or enforced.
        let reason = new Error(message);
        reject(reason);

        // Throwing an error also rejects the promise.
        throw reason;
    }
});
```

then 和 catch 方法可以用于在回调中附带返回值：

```
promise.then(value => {
    // Work has completed successfully,
    // promise has been fulfilled with "value"
});

promise.catch(reason => {
    // Something went wrong,
    // promise has been rejected with "reason"
});
```

作为替代，两种回调可以被附带在一个then的调用中：

```
promise.then(onFulfilled, onRejected);
```
给已经处理完成的 promise 附带回调将会立即把它们放进 *微任务* 队列，然后它们会尽快被调用。
附带回调前不需要检查 promise 的状态，不像其他的事件处理实现方式。

promise 的 then 方法可以返回一个新的 promise，从 then 返回的 promise 将会粘到 promise 链上：
Promise.all() 静态方法接受一个可遍历的 promises列表，并返回一个新的 promise。
