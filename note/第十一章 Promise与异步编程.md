# 第十一章 Promise与异步编程

## 异步编程

JavaScript引擎中，只有一个主线程，当执行JavaScript代码块时，不允许其他代码块执行，而事件机制和回调机制的代码块会被添加到任务队列中，当符合某个触发回调或者事件的时候，就会执行该事件或者回调函数。

## Promise

Promise生命周期：pending（进行中） fulfilled（已完成） rejected（拒绝)。

Promise不会直接返回异步函数的执行结果，如果执行成功需要使用then()，错误时使用catch()。

```js
    const promise = instance.get('url')
    promise.then(result => console.log(result)).catch(err => console.log(err))
```

### 创建Promise

Promise构造函数只有一个参数，该参数是一个参数，称为执行器，执行器中有两个参数，分别是resolve()，reject()，表示成功和失败。

Promise的实例通过resolve或者reject函数返回，然后使用then和catch来获取，不能在实例中直接return。

``` js
        function promiseTest(num) {
            return new Promise((resolve, reject) => {
                if(num > 5){
                    resolve('num大于五');
                }
                else {
                    reject(Error('num小于五'));
                }
            })

        }
        promiseTest(2)
            .then(result => console.log(result)) 
            .catch(err=>console.log(err));      // Error: num小于五
```

###  相应多个Promise

Promise.all()方法 ，返回一个Promise对象，可接收单个可迭代对象(如数组)，只有在可迭代对象元素都是Promise，且都完成（resolve）后，返回的Promise对象才会被完成（resolve）。

```JavaScript
let p4 = Promise.all([p1, p2, p3]);
p4.then().catch();
```

如果有任意一个Promise被拒绝，那么返回的Promise也会立即被拒绝。

Promise.race方法，返回一个Promise对象，接收可迭代对象，数组中第一个解决的Promise对象的结果（resolve或reject），就是返回Promise对象的结果。