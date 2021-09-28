## Angular

Angular CLI

```javascript

//ng build	
//把 Angular 应用编译到一个输出目录中。

//ng serve	
//构建你的应用并启动开发服务器，当有文件变化时就重新构建。

//ng generate	
//基于原理图（schematic）生成或修改某些文件。

//ng test	
//在指定的项目上运行单元测试。

//ng e2e	
//构建一个 Angular 应用并启动开发服务器，然后运行端到端测试。
```



### 	**创建组件**

```javascript
创建组件 ng generate service heroes/hero
  
   缩写 ng g c *name*  创建组件compoents

	card.component.html  //模板
	card.component.less  //样式
	card.component.spec.ts  //不用管
	card.component.ts //逻辑状态
```

### 	创建可注入服务serve

```javascript
ng generate service heroes/hero
	 缩写 ng g s *name*  创建服务serve



//hero.service.ts
import { Injectable } from '@angular/core';

@Injectable({       //装饰器
  providedIn: 'root',    //表示整个应用程序中都是可见的
})
export class HeroService {
  constructor() { } 
}


//需要用到服务的组件中
import { HeroService } from '../serves/hero.service'

constructor(public SearchServie:SearchServie) //可以使用SearchServie服务了
```



**card.component.ts**

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'hello-world',
  template: `
    <h2>Hello World</h2>
    <p>This is my first component!</p>
    `,
})
export class HelloWorldComponent {
  // The code in this class drives the component's behavior.
    message = 'Hello, World!';  //数据状态
}
```



**模板语法**

```vue
<p>{{ message }}</p>
```



**Angular 还支持属性绑定，以帮助你设置 HTML 元素的 Property 和 Attribute 的值，**

**并将这些值传给应用的展示逻辑。**

```html
<p [id]="sayHelloId" [style.color]="fontColor">You can set my color in the component!</p>
```



时间监听器

```html
<button (click)="sayMessage()" [disabled]="canClick">Trigger alert message</button>
```



# 例子

##### card.component.ts

```javascript
import { Component } from '@angular/core';
 
@Component ({
  selector: 'hello-world-bindings',  //组件name
  templateUrl: './hello-world-bindings.component.html'   //模板路径
})
export class HelloWorldBindingsComponent {
    fontColor = 'blue';   //各种装填
    sayHelloId = 1;
    canClick = false;
    message = 'Hello, World';
    sayMessage() {         //事件
        alert(this.message);
    }
}
```

##### card.component.html

```html
<button (click)="sayMessage()" [disabled]="canClick">Trigger alert message</button>
<p [id]="sayHelloId" [style.color]="fontColor">You can set my color in the component!</p>
```



### 基础用法

```JS
// *ngFor
// *ngIf
// [title]="product.name + ' details'"
// {{ product.name }} 插值
// (click)="share()"
```



```html
<div *ngFor="let product of products">
  <h3>
    <a [title]="product.name + ' details'">
      {{ product.name }}
    </a>
  </h3>
   

  <p *ngIf="product.description">
    Description: {{ product.description }}
  </p>

  <button (click)="share()">
    Share
  </button>
</div>

 <ul>
  <li *ngFor="let in of constructor(10);let index=index">{{index}}</li>
 </ul>
```



### 组件使用

```html
//所以组件需要在 app.module.js中进行声明，而不是单独在文件中引入
@NgModule({
 declarations: [   //declarations 声明
    AppComponent,
    TopBarComponent,
    ProductListComponent,
    ProductAlertsComponent
  ]
})
//使用的时候直接用组件就了
  <app-product-alerts> </app-product-alerts>
 
```



### 父组件传值子组件

```jsx
//父传出
<app-product-alerts [product]="product" >
  </app-product-alerts>

//子接受
import { Input } from '@angular/core';
export class ProductAlertsComponent implements OnInit {
  @Input() product: any;
  @Input() list:string[];    //字符串形式的数组
}

//子使用
<p *ngIf="product.price > 700"></p>
```



### 子组件调用父组件方法

```jsx
//子创建事件
import { Output, EventEmitter } from '@angular/core';
export class ProductAlertsComponent implements OnInit {
  @Output() notify = new EventEmitter();  //自定义事件notify
}
//子触发自定义事件
<button (click)="notify.emit()">Notify Me</button>

//父接收到事件时，触发自身对应的onNotify()事件
  <app-product-alerts (notify)="onNotify()">  </app-product-alerts>

//普通事件调用
<button (click)="share()">Share</button>
```



### 路由

```javascript

//1.引入写好的组件
import { ProductDetailsComponent } from './product-details/product-details.component';

//2.书写路由  app.module.ts  ==>  imports:[]  ==>  RouterModule.forRoot([{},{},{}])  
//        =====> {path:'',component:ProductDetailsComponent}

例：RouterModule.forRoot([
    	{ path: '', component: ProductListComponent },
    	{ path: 'products/:productId', component: ProductDetailsComponent }   
])

//3.HTML中使用
//  <a [routerLink]="['/']">点击跳转主页</a>
//	<a routerLink="/cart">运费查询</a>
//  <a [routerLink]="['/products', product.id]"> 根据ID跳转页面 </a>


//路由的参数js
import {ActivatedRoute} from '@angluar/router'
constructor(
	private route:ActivatedRoute,
)
//this.route.params.subscribe(item=>{  console.log(item.id)  })


//路由的方法js 跳转什么的~
import {Location} from '@angular/common'
constructor(
	public location:Location
)
//location.back()
```



### 插槽

```html
//父组件
<div>
  <app-child>
    <p>插槽内容</p>
    <p>其他sss</p>
  </app-child>
</div>

//子组件

  <!-- 插槽预留位置 -->
 <ng-content></ng-content>
```



### 声明周期

```javascript
1. constructor(){  //最先被执行 }

```



### serves 数据共享

```JS
1. 创建service服务
ng g s service/search
```



### HTTP请求

```javascript
1. 注册http服务
//app.module.ts
import { HttpClitentModule } from '@angular/common/http'

@NgModule({
    imports:[
//        AppRoutingModule,
          HttpClientModule
    ]
})

2.组件使用http
import { HttpClient } from '@angular/common/http'

constructor(
	private http:HttpClient;   //注入http
){}


getlist(){
    this.http.get('https://tenant.51yundong.me/v3/.....')
        .subscribe((res.any)=>{
        console.log(res.data);
        this.list = res.data
    })
}

```



### interface示例

```javascript
demo
// 1. 没有interface
    // function hello(obj:{label:string}){
    //     console.log(obj);
        
    // }
    // hello({label:123})  //报错
    // hello({label:'正确传值'}) 

//2. 使用了interface
interface labelobj{
     label:string，
}
function helloprint(labelobj:labelobj){
    console.log(labelobj);
}

// helloprint({label:true}) //报错
helloprint({label:'正确传值'})
```



## 二、interface具体写法

```javascript
//定义对象
interface labelobj{
     label:string，
     width?:number，    //添加？号，代表可选参数
     readonly x:number,  //readonly 只读，不可更改
     label:string|number  //多个类型 | 隔开

}

//定义函数
interface searchFunc{
	 ():boolean   //返回值要求数值类型
     (source:number,substr?:number):boolean   //规定传入值
}
            //正确
            let sf:searchFunc = function(sr,su){
                return sr > su
            }
            sf(100,200)

//Void  函数没有返回值
function say_hello(name:string):void{
    console.log(`hello ${name}`);
}
say_hello('xiaoMing小明')
```

#### null 和 underfined

```javascript
// --strictNullChecks:false 不可以写，会报错，true才可以这样写
let u:undefined = undefined
let n:null = null
let n1:number = 0
n1 = undefined

let n12:string|null|undefined  //这样写好点，都没问题
```



#### Array数组限制 

```javascript
interface StringArr{
    [index:number]:string|number   //index代表索引
}

let arr:StringArr = ['a','b','b']  //只能是字符和数字

let list:number[] = [1,2,3,4]  //只能是number类型的数组
let list:Array<number> = [1,2,3]  //第二种写法
let strlist:string[] = ['abc']
```



#### object对象限制

```javascript
interface NumberDict{
    [index:string]:number|string,
    length:number,
    name:string
}

let numdict:NumberDict = {
    length:10,
    name:'username'
}
```



#### 枚举类型(限定几种选择)

```javascript
enum Dirction{
    Up="UP",
    Down="DOWN",
    Left="LEFT",
    Right="RIGHT"
}

let dirc:Dirction = Dirction.Right

if(dirc == Dirction.Right){
    console.log('right',Dirction.Right);
}
```



#### 元组 tuple

```javascript
//了解一下
let numstuple:[number,string] = [0,'a']   //限定了第一个数字，第二个为字符串
```



### 断言

```javascriptx
(<string>someValue).length;
(someValue as string).length;
```



### 私有 公共

```javascriptx
//private 私有的  
//public 公共的


class Animal{
    private name:string;

    constructor(theName:string){
        this.name = theName
    }

    public run(){
        console.log(`${this.name} is running.....`)
    }
}

const animal = new Animal('wangcai')

animal.run()
console.log(animal.name) //属性“name”为私有属性，只能在类“Animal”中访问。
```

### 受保护的类

```javascript
class Animal{
    protected name:string;
    constructor(theName:string){
        this.name = theName
    }
    public run(){
        console.log(`${this.name} is running.....`)
    }
}

class Dog extends Animal{
    constructor(dogName:string){
        super(dogName)
    }
    wangwang(){
        console.log(`${this.name} is wangwang`);  //访问父类中受保护的属性
        
    }
}
const dog = new Dog('wangcai')
dog.wangwang()
```





## 三、Angular生命周期

```css
Angular 会按以下顺序调用钩子方法：

ngOnChanges - 在输入属性 (input)/输出属性 (output)的绑定值发生变化时调用。

ngOnInit - 在第一次 ngOnChanges 完成后调用。  //请求，开启定时器

ngDoCheck - 开发者自定义变更检测。  类似Vue的watch，性能消耗较大  //少

ngAfterContentInit - 在组件内容初始化后调用。   //少

ngAfterContentChecked - 在组件内容每次检查后调用。  //少

ngAfterViewInit - 在组件视图初始化后调用。       //少

ngAfterViewChecked - 在组件视图每次检查后调用。   //少

ngOnDestroy - 在指令销毁前调用。      //定时器...等
```

