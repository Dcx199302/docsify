## 一、base

```javascript
export class AppComponent {
    title = '这里是要展示的数据';
    name:'名字'
    date:Date = new Date()
    box:string = 'box-ts';
    isActive:boolean = true;
    isMax:boolean = true;
    colors = ['red','blue','yellow','green']
	types = 1  // types 修改成2 - 3 
	username:string = "用户名"
	dateTime:Date = new Date()  

    clickFun(e:Event){ console.log(e,"点击了按钮") }
	inputChange(e:Event){ console.log(e.target.vlaue,"input值变动") }
	getUserName(value:string){ console.log(value,"拿到输入框的数据") }
	getDomForBox(box){ console.log(box) }
            
}
```



<!-- tabs:start -->

#### **插值**

```html
<!-- 正确例子 -->
<div>
   <p>{{name}}</p>
   <p>{{name + "你好啊"}}</p>
   <p>{{name?"张三":"李四"}}</p>
   <p>{{name?1 + 1:"李四"}}</p>
   <p>时间：{{date}}</p>
</div>

<!-- 错误例子 -->
<p>{{ new Date() }}</p>   //报错
<p>{{ if(...){ ... } }}</p>   //报错
```

#### **属性绑定**

##### 一、Attribute属性绑定

```html
<h3 [id]="'dom-title'">  Attribute属性绑定 </h3>
<div [id]="'box'">属性字符串绑定</div>
<div [id]="box">读取-xx.comonent.ts-属性 box = box-ts</div>

```

##### 二、类绑定class

```jsx
//单一类绑定
<div [class.h3-dom]="true"> 单一类绑定 </div>

//多重类绑定
<div [class]="'h3-dom title-dom min-title'"> 多个类绑定 -- 1 </div>
<div [class]="{ 'h3-dom':true , 'title-dom':false }"> 多个类绑定 -- object对象 </div>
<div [class]="[ 'h3-dom' , 'title-dom' , 'min-title']"> 多个类绑定 -- Array数组 </div>
    
//ngClass
<div [ngClass]="{'active':isActive}"> js控制class类 </div>

```

##### 三、样式绑定

```jsx
//单个样式
<h3 [style.width]="'300px'"> 单一样式绑定 </h3>
<h3 [style.width.px]="'300'"> 单一样式绑定 可以写像素 </h3>
<h3 [style.color]="'red'"> 单一样式绑定 </h3>

//多个样式
<div [style="'background:red;color:#fff'"]>多个样式绑定</div>
<div [ngStyle]="{'color':'red'}"></div>
```

#### **if判断**

```html
<div *ngIf="isMax"> if控制isMax显示 </div>
<div *ngIf="!isMax"> if控制isMax显示-取反 </div>


if/else  渲染指定的Temlpate模板
    <ng-container *ngIf="isMax; else elesTemlpate">
        <div> isMax = true </div>
    </ng-container>

    <ng-container #elesTemlpate>
        <div> isMax = true </div>
    </ng-container>
```

#### **for循环**

```html
<div *ngFor="let color of colors let i=index let odd=odd">
    {{odd}}
    {{i}}
    {{color}}
</div>

//解析完后显示的效果
<ng-template ngFor let-color [ngForOf]="colors" let-i="index" let-odd="odd">
    <div>{{odd}} {{i}}{{color}}</div>
</ng-template>
```

#### **ngSwitch**

```html
<div [ngSwitch]="types">
    <div *ngSwitchCase="1">types = 1时显示</div>
    <div *ngSwitchCase="2">types = 2时显示</div>
    <div *ngSwitchCase="3">types = 3时显示</div>
    <div *ngSwitchDefault> types不等于1-2-3时候显示 </div>
</div>
```

#### **事件绑定**

```html
<button (click)="clickFun($event)"></button>

<input type="text" (input)="inputChange($event)" name="" id="" />

//button 获取 input 
<input #userName type="text" (input)="inputChange($event)" name="" id="" />   //#userName模板引用变量
<button (click)="getUserName(userName.value)"></button>
```

#### **模板引用**

```html
<div #box>
    <input type="text"></input>
    <button>按钮</button>
</div>
<button (Click)="getDomForBox(box)"> 点击获取到上面的模板 </button>
```

#### **双向绑定**

- 双向绑定只对表单元素有效-使用前需在 app.moudle.ts 导入 **FormsModule** 模块
- import ：[  ... FormsModule  ]

```html
<div>
    输入：<input [(ngModule)]="username">
</div>
```

#### **管道pipe**

- {{ 输入数据 | 管道: 管道参数 }}
- 链式管道 {{ 数据 | A | B }} 先执行A 管道 --> B管道
- {{date | date: 'fullDate' | uppercase}}

```html
<div>{{dateTime | data:'yyyy-mm-dd HH:mm:ss'}}</div>  //时间格式2021-09-12 15:19:00
<div>{{ }}</div>    JsonPipe      将输入数据对象经过JSON.stringify() 方法转换后输出对象的字符串
<div>{{ }}</div>    UpperCasePipe 小写字母转大写
<div>{{ }}</div>    LowerCasePipe 大写转小写
<div>{{ }}</div>    DecomalPipe   将数值按照特定的格式显示文本
<div>{{ }}</div>    CurrentcyPipe 将数值进行货币格式化处理
<div>{{ }}</div>    SlicePipe     将数组或字符串剪成新子集
<div>{{ }}</div>    PercentPipe   将数值转百分比格式
```

**自定义管道**

```javascript
//cli创建管道  路径 ：项目下跟src/pipes/test    cli创建会自动在app.module.ts 中引入 declarations：{ TestPipe }
命令 ： ng g p pipes/test    

//test.pipe.ts         代码
//test.pipe.spec.ts  测试文件
```

```javascript
import { Pipe, PipeTransform } from '@angular/core';
@Pipe({
  name: 'test'
})
export class TestPipe implements PipeTransform {

  transform(value: unknown, ...args: unknown[]): unknown {
    return null;
  }
}

// value 收到的数据
// ...args 收到的参数
// return 'xxxx'  返回结果
```



<!-- tabs:end -->

