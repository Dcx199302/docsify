# 组件交互



### 一、父传子

<!-- tabs:start -->

#### **父组件.html**

```html
<app-child-interaction [number]="numbers"></app-child-interaction>
```

#### **子组件**

```javascript
export class ChildInteractionComponent implements OnInit {
  constructor() { }
  ngOnInit(): void {}

  @Input() number:number
}
```

<!-- tabs:end -->



### 二、子传父（子调用父的方法）-- 主动暴露

<!-- tabs:start -->

#### **子**

```javascript
import { Component, EventEmitter, OnInit, Output } from '@angular/core';
 ...
@Component({ ...})
export class ChildInteractionComponent implements OnInit {
 ...
  @Output() ageChange = new EventEmitter<Number>();
  age =  123
  // addAge(){    this.ageChange.emit(this.age) }
}
```

```html
<div>
    <input type="text">
    <button>按钮点击</button>
    <button (click)="ageChange.emit(age)">点击触发父组件事件</button>
</div>
```



#### **父**

```html
<app-child-interaction (ageChange)="hi($event)"></app-child-interaction>
```

```javascript
import { Component, OnInit } from '@angular/core';

@Component({ ...})
export class ParentInteractionComponent implements OnInit {
  ...
  hi(value){
    console.log(value)
  }

}
```

<!-- tabs:end -->



### 三、#标记方法   

--  #名字  标记组件   #childssss
--  在父组件控制器中声明一个由viewChild装饰器装饰的变量获得子组件的引用

<!-- tabs:start -->

#### **父**

```javascript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ChildInteractionComponent } from 'src/app/components/child-interaction/child-interaction.component';

@Component({...})
export class ParentInteractionComponent implements OnInit {
...
  @ViewChild('childssss')    //引用标记的方法
  childCompent:ChildInteractionComponent

  handleClick(){
    this.childCompent.NoEventEmitter()
  }

}
```

```html
<app-child-interaction #childssss></app-child-interaction>
<button (click)="handleClick()">点击调用app-child-interaction 的方法</button>
```

#### **子**

```javascript
import { Component,OnInit} from '@angular/core';

@Component({...})
export class ChildInteractionComponent implements OnInit {
  constructor() { }
  ngOnInit(): void {}

  NoEventEmitter(){
    console.log('1231212414412')
  }
}
```

<!-- tabs:end -->