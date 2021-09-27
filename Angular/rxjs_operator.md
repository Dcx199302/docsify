# Rx核心：操作符

[中文教学文档](https://cn.rx.js.org/)

## 一、创建类操作符

- throttleTime（1000）节流时间
- scan（)   扫描； 可以用于状态管理
- 其他流程控制操作符有 [**filter**](https://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-filter)、[**delay**](https://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-delay)、[**debounceTime**](https://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-debounceTime)、[**take**](https://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-take)、[**takeUntil**](https://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-takeUntil)、[**distinct**](https://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-distinct)、[**distinctUntilChanged**](https://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-distinctUntilChanged) 等等。
  - 翻译：     				筛选，延迟，去抖动时间、拿，直到、清楚的，不同-直到改变

实例：

```javascript
var button = document.querySelector('button');
Rx.Observable.fromEvent(button, 'click')
  .throttleTime(1000)
  .scan(count => count + 1, 0)
  .subscribe(count => console.log(`Clicked ${count} times`));
```

