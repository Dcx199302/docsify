# rxjs

## 一、介绍



#### 一、Rxjs例子

<!-- tabs:start -->

##### **一般写法**

```javascript
document.addEventListener('click', () => console.log('Clicked!'));
```

##### **使用RxJS**

```javascript
import { fromEvent } from 'rxjs';

fromEvent(document, 'click').subscribe(() => console.log('Clicked!'));
```

<!-- tabs:end -->

#### 二、Purity纯度

- RxJS 的强大之处在于它能够使用纯函数生成值。这意味着您的代码不太容易出错。
- 通常你会创建一个不纯的函数，你的其他代码片段可能会弄乱你的状态。

<!-- tabs:start -->

##### **非纯写法**

```javascript
let count = 0;
document.addEventListener('click', () => console.log(`Clicked ${++count} times`));
```

##### **使用 RxJS 可以隔离状态**

```javascript
import { fromEvent } from 'rxjs';
import { scan } from 'rxjs/operators';

fromEvent(document, 'click')
  .pipe(scan(count => count + 1, 0))
  .subscribe(count => console.log(`Clicked ${count} times`));
```

<!-- tabs:end -->





#### 三、Flow流程

- RxJS 有一系列的操作符，可以帮助你控制事件如何通过你的 observables。

实现：每秒最多允许一次点击



<!-- tabs:start -->

##### **纯 JavaScript**

```javascript
let count = 0;
let rate = 1000;
let lastClick = Date.now() - rate;
document.addEventListener('click', () => {
  if (Date.now() - lastClick >= rate) {
    console.log(`Clicked ${++count} times`);
    lastClick = Date.now();
  }
});
```



##### **RxJS**

```javascript
import { fromEvent } from 'rxjs';
import { throttleTime, scan } from 'rxjs/operators';

fromEvent(document, 'click')
  .pipe(
    throttleTime(1000),
    scan(count => count + 1, 0)
  )
  .subscribe(count => console.log(`Clicked ${count} times`));
```



<!-- tabs:end -->



#### 四、Values

- 您可以转换通过 observable 传递的值。

实现：每次点击添加当前鼠标 x 位置值的方法



<!-- tabs:start -->

##### **javascript**

```javascript
let count = 0;
const rate = 1000;
let lastClick = Date.now() - rate;
document.addEventListener('click', event => {
  if (Date.now() - lastClick >= rate) {
    count += event.clientX;
    console.log(count);
    lastClick = Date.now();
  }
});
```



##### **Rxjs**

```javascript
import { fromEvent } from 'rxjs';
import { throttleTime, map, scan } from 'rxjs/operators';

fromEvent(document, 'click')
  .pipe(
    throttleTime(1000),
    map(event => event.clientX),
    scan((count, clientX) => count + clientX, 0)
  )
  .subscribe(count => console.log(count));
```



<!-- tabs:end -->



## 二、Rxjs概述

<!-- tabs:start -->

#### **Observable**

-  adj. 显著的；觉察得到的；看得见的 ; 可观察对象;
- 以下是一个 Observable，它在订阅时立即（同步）推送值`1`, `2`，`3`以及`4`自 subscribe 调用后经过一秒后的值，然后完成：

<!-- panels:start -->

<!-- div:left-panel -->

```javascript

import { Observable } from 'rxjs';
 
const observable = new Observable(subscriber => {
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
  setTimeout(() => {
    subscriber.next(4);
    subscriber.complete();
  }, 1000);
});
 
console.log('just before subscribe');
//要调用 Observable 并查看这些值，我们需要订阅它：
observable.subscribe({
  next(x) { console.log('got value ' + x); },
  error(err) { console.error('something wrong occurred: ' + err); },
  complete() { console.log('done'); }
});
console.log('just after subscribe');
```

<!-- div:right-panel -->

```javascript
//左边代码输出 -- rxjs是非异步的
//just before subscribe
//got value 1
//got value 2
//got value 3
//just after subscribe
//got value 4
//done

import { from } from 'rxjs';
//1. 发布
const observable = from([10, 20, 30]);
//2. 订阅
let subscription = observable.subscribe(x => console.log(x))
// Later:  3. 取消订阅
subscription.unsubscribe();

//发送三种状态出去， 
//next 数据 
//error 错误 
//complete 完成

```

<!-- panels:end -->



#### **Observer**

- n. 观察者，目击者；观察家，评论员；（会议等的）观察员

```javascript
import { Observable } from 'rxjs';
//第一种：
    // 1.创建可观察对象
    const observable = new Observable(sub=>{
        sub.next(999)
    })

    // 2.观察者
    const observer = {
        next: x => console.log('Observer got a next value: ' + x),
        error: err => console.error('Observer got an error: ' + err),
        complete: () => console.log('Observer got a complete notification'),
      };

    // 3. 可观察对象.订阅 (观察者)
    observable.subscribe(observer)

    // 输出结果
    // Observer got a next value: 999

//第二种方式：
 observable.subscribe(x => console.log('Observer got a next value: ' + x));
```



#### **Operators**

- [计] 运算符； 操作符 ；--- 经营者；操作者；
- 运算符是**函数**。有两种运算符
  - 管道传输到 Observables 的**运算符**`observableInstance.pipe(operator())`  可观察到的实例
  - **创建运算符**是另一种运算符，可以作为独立函数调用以创建新的 Observable

```javascript
import { of } from 'rxjs';
import { map } from 'rxjs/operators';

of(1, 2, 3).pipe(map((x) => x * x)).subscribe((v) => console.log(`value: ${v}`));
  
// 输出:
// value: 1  value: 4   value: 9

//创建运算符 ： of(1,2,3) 
//管道运算符 ： observable.pipe(map(x=>{x * x}))     pipe：管道    这里的map是rxjs的运算符
```



<!-- panels:start -->

<!-- div:title-panel -->

##### 常用操作符

<!-- div:left-panel -->

```javascript
import { of } from 'rxjs';
import { map } from 'rxjs/operators';

of(1, 2, 3)
  .pipe(map((x) => x * x))     //运算符map类似于同名的 Array 方法。就像[1, 2, 3].map(x => x * x)
  .subscribe((v) => console.log(`value: ${v}`));
// 输出:
// value: 1   value: 4   value: 9

of(1, 2, 3)
  .pipe(first())
  .subscribe((v) => console.log(`value: ${v}`));
// 输出:
// value: 1

obs.pipe(op1(), op2(), op3(), op4());  //使用了多个操作符
```



<!-- div:right-panel -->

**创建运算符**

创建操作符是可用于创建具有一些常见预定义行为的 Observable 或通过加入其他 Observable 的函数。

典型示例是`interval`函数。它接受一个数字（不是 Observable）作为输入参数，并返回一个Observable

```javascript
import { interval } from 'rxjs';
const observable = interval(1000 /* number of milliseconds */);
```



<!-- panels:end -->

#### **Subscription**

- 捐献；订阅；订金；签署

<!-- panels:start -->

<!-- div:title-panel -->

- Subscription 本质上只有一个`unsubscribe()`功能来释放资源或取消 Observable 执行。
- 通过将一个订阅“add添加”在一起，这样`unsubscribe()`对一个订阅中的一个的调用可以取消多个订阅。
- Subscriptions 也有一个`remove(otherSubscription)`方法，用于撤销子 Subscription 的添加。

<!-- div:left-panel -->

```javascript
import { interval } from 'rxjs';
 
const observable1 = interval(400);
const observable2 = interval(300);
 
const subscription = observable1.subscribe(x => console.log('first: ' + x));
const childSubscription = observable2.subscribe(x => console.log('second: ' + x));
 
subscription.add(childSubscription);
 
setTimeout(() => {
  // Unsubscribes BOTH subscription and childSubscription 取消订阅和子订阅  
  subscription.unsubscribe();
}, 1000);
```



<!-- div:right-panel -->

```javascript
//logs 输出
//second: 0
//first: 0
//second: 1
//first: 1
//second: 2
```



<!-- panels:end -->



#### **Subject**

- 主题；起因；科目；主词
- RxJS Subject 是一种特殊类型的 Observable，它允许将值多播到许多观察者。虽然普通的 Observable 是单播的（每个订阅的 Observer 拥有一个独立的 Observable 执行），但Subject是多播的。

```javascript
import { from,Subject  } from 'rxjs';

const Asubject = new Subject();
Asubject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});
Asubject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});
 
const Bobservable = from([1, 2, 3]);
Bobservable.subscribe(Asubject); // 您可以订阅提供的主题(Subject)
Bobservable.subscribe({
        next:(e)=>{console.log(e)}		
    }); // 您可以订阅提供的主题(Subject)
```

<!-- tabs:end -->



## 三、概述详情

### 一、Observable可观察对象



<!-- panels:start -->

<!-- div:left-panel -->

456

<!-- div:right-panel -->

789

<!-- panels:end -->
