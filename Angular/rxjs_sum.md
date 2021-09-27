# Rxjs总结

### 一、创建Observable可观察对象

- 观察对象

<!-- tabs:start -->

#### **All**

```javascript
//可以使用new Observable. 最常见的是，使用创建的功能，如创建观测of，from，interval，等
import {  Observable,fromEvent, of, from  } from 'rxjs';
const observable = new Observable()

const observable = fromEvent(document, 'click')

const dataSource = of(1, 2)

const observable = from([10, 20, 30]);
```



#### **函数**

```javascript
import {  Observable  } from 'rxjs';

const observable = new Observable();
```

#### **事件**

```javascript
import { fromEvent } from 'rxjs';

fromEvent(document, 'click')
```

#### **数组**

```javascript
import { of } from 'rxjs';

const observable =of(1, 2)
```

#### **数组**

```javascript
import { from } from 'rxjs';

const observable = from([10, 20, 30]);
```



<!-- tabs:end -->



### 二、总结observer

<!-- panels:start -->

<!-- div:left-panel -->

-  观察对象

- Observable：adj. 显著的；觉察得到的；看得见的

  - ```javascript
    import {  Observable  } from 'rxjs';
    
    const observable = new Observable(response=>{
        	response.next(1)
        	response.next(2)
        	response.error('出现错误')
        	response.complete('通知完毕')
    	}    
    );
    ```

<!-- div:right-panel -->

-  观察-订阅subscribe

- subscribe ：  订阅；捐款；认购；赞成；签署

  - ```javascript
    observable.subscribe({
      next(x) { console.log('需要的数据' + x); },
      error(err) { console.error('发生了错误: ' + err); },
      complete() { console.log('完成'); }
    })
    //“下一个”通知：发送一个值，如数字、字符串、对象等
    //“错误”通知：发送 JavaScript 错误或异常
    //“完成”通知：不发送值
    //在 Observable执行时，可以传递零到无限的 Next 通知
    //发送了 Error 或 Complete 通知后，则此后无法发送其他通知
    ```

<!-- panels:end -->



<!-- tabs:start -->

#### **All**

```javascript
//写法一:
const obj = {
    next(x) { console.log('需要的数据' + x); },
  error(err) { console.error('发生了错误: ' + err); },
  complete() { console.log('完成'); }
}
observable.subscribe(obj);

//写法二： 
observable.subscribe({ next(x) { console.log(x) },...此次省略error和complete })

//写法三:
observable.subscribe( response => console.log(response) )
```

#### **重复订阅**

```javascript
//可以：重复订阅  不会影响 观察对象Observable
observable.subscribe(x => { console.log(x+1) });
observable.subscribe(y => {  console.log(y+2) });
observable.subscribe(z => {  console.log(z+2) });
```

#### **简单**

```javascript
observable.subscribe( response => console.log(response) )
```

### **三、取消订阅**

- subscription ： 订阅行为 n. 捐献；订阅；订金；签署

```javascript
//取消订阅，类似于定时器的取消，可以节约性能
subscription = observable.subscribe( response => console.log(response) )
subscription.unsubscribe();
//or
observable.subscribe( response => console.log(response) ).unsubscribe();
```

- 同时取消多个订阅

```javascript
import { interval } from 'rxjs';
 
const observable1 = interval(400);
const observable2 = interval(300);
 
const subscription = observable1.subscribe(x => console.log('first: ' + x));
const childSubscription = observable2.subscribe(x => console.log('second: ' + x));
 
subscription.add(childSubscription);  //添加

setTimeout(() => {
  // 取消 自身订阅 和 子订阅  
  subscription.unsubscribe();
}, 1000);
```

<!-- tabs:end -->



### 四、理解rxjs

```javascript
function subscribe(subscriber) {
  const intervalId = setInterval(() => {
    subscriber.next('hi');
  }, 1000);
 
  return function unsubscribe() {
    clearInterval(intervalId);
  };
}

const unsubscribe = subscribe({next: (x) => console.log(x)});

unsubscribe(); // 清除定时
```



观察--观察者关系

- 观察的对象 observable
- 观察 subscribe
- 观察者 observer

```javascript
import {  Observable  } from 'rxjs';

const observable = new Observable();

const observer = {
  next: x => console.log('Observer got a next value: ' + x),
  error: err => console.error('Observer got an error: ' + err),
  complete: () => console.log('Observer got a complete notification'),
};

// 观察对象.观察(观察者）
// observable.subscribe(observer);
```





### 五、subject

- n. 主题；起因；科目；主词；
- 用于处理：多播  ， 默认observable是单播

<!-- tabs:start -->

#### **单播**

```javascript
import { from,Observable,of } from 'rxjs';
//1. 发布
const observable = of(10, 20, 30);
const observable = from([10, 20, 30]);
const observable = new Observable()
//等...

observable.subscribe(i=>{console.log(i)});
```

#### **多播**

```javascript
import { Subject } from 'rxjs';
//多播
const subject = new Subject();

subject.next(1);
subject.next(2);
//传入了不同的值，还可以传 observable
```

#### **单多播对比**

<!-- panels:start -->

<!-- div:left-panel -->

```javascript
import { Subject, from,of, Observable } from 'rxjs';
// 多播
const subject = new Subject()
subject.subscribe(item=>{
      item.forEach(element => {
        console.log("多播",element)
      });
})

// 准备两个可观察对象（带上数据）
const obsOf = of(1,2,3,4)
const obsFrom = from([1,2,3,4])
    
// 多播的subject才有next()的方式，
// 传入一个 '可观察对象observable'
subject.next(obsOf)
subject.next(obsFrom)
```

<!-- div:right-panel -->

```javascript
import { Subject, from,of, Observable } from 'rxjs';
// 单播
const observable = new Observable(
  res=>{
    res.next('abc')
    res.next('cde')
  }
)
observable.subscribe(item=>{
  console.log("单播",item)
})
```

<!-- panels:end -->

<!-- tabs:end -->



### 六、操作符Operators 复杂-研究

- [计] 运算符； 操作符 ；--- 经营者；操作者；

- ```javascript
  import {  Observable  } from 'rxjs';
  const observable = new Observable();
  
  observable.pipe(map((x) => x * x)).subscribe((v) => console.log(v));
  ```

<!-- tabs:start -->

#### **管道类操作符**

```javascript
observable.pipe()
of(1, 2, 3).pipe(map((x) => x * x))   //遍历每一个map  输出： 1 4 9
of(1, 2, 3).pipe(first())			 //处理第一个第一个 输出:  1

//多个操作符写法： 
// observable.pipe(op1(), op2(), op3(), op4());
```

#### **创建类操作符**

```javascript
import { interval } from 'rxjs';
import { map } from 'rxjs/operators';

//操作符 interval 定时器
const observable = interval(1000 /* 没一秒执行一次 */);

const fileObservable = observable.pipe(map((x) => console.log(x)));  /*  当前执行的次数 */
fileObservable.subscribe()
```



<!-- tabs:end -->



