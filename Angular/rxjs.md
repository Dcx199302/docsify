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

输出结果：

```js
just before subscribe
got value 1
got value 2
got value 3
just after subscribe
got value 4
done
```



#### **Observer**

- n. 观察者，目击者；观察家，评论员；（会议等的）观察员

```javascript
```



#### **Operators**

- 经营者；操作者；[计] 运算符； 操作符 ；

```javascript
```



#### **Subscription**

- 捐献；订阅；订金；签署

```javascript
```



#### **Subject**

- 主题；起因；科目；主词

```javascript
```



#### **Scheduler**

- n. 计划员；时间调度员；程序机，调度机；调度程序；制表人;  调度器

```javascript
```



#### **Testing RxJS Code with Marble Diagrams**

- 用(大理石图, 弹珠图 )测试RxJS代码

```javascript
```



<!-- tabs:end -->







<!-- tsbs:start -->

<!-- tsbs：end -->