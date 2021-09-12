# 基础语法

### 一、插值语法

<!-- tabs:start -->

#### **javascript**

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.less']
})
export class AppComponent {
  title = '这里是要展示的数据';
  name:'名字'
  date:Date = new Date()
}

```

#### **html**

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

<!-- tabs:end -->



### 二、属性绑定

<!-- tabs:start -->

#### **javascript**

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.less']
})
export class AppComponent {
  box:string = 'box-ts';
  isActive:boolean = true;
}
```

#### **html**

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



<!-- tabs:end -->



### 三、条件判断if

<!-- tabs:start -->

#### **html**

```jsx
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

#### **js**

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.less']
})
export class AppComponent {
  isMax:boolean = true;
}
```

<!-- tabs:end -->



### 四、for循环语句

<!-- tabs:start -->

#### **html**

```jsx
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

#### **js**

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.less']
})
export class AppComponent {
  colors = ['red','blue','yellow','green']
}
```

<!-- tabs:end -->



### 五、ngSwitch

<!-- tabs:start -->

#### **html**

```html
<div [ngSwitch]="types">
    <div *ngSwitchCase="1">types = 1时显示</div>
    <div *ngSwitchCase="2">types = 2时显示</div>
    <div *ngSwitchCase="3">types = 3时显示</div>
    <div *ngSwitchDefault> types不等于1-2-3时候显示 </div>
</div>
```

#### **js**

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.less']
})
export class AppComponent {
  types = 1  // types 修改成2 - 3 
}
```

<!-- tabs:end -->



### 六、事件绑定

<!-- tabs:start -->

#### **html**

```html
<button (click)="clickFun($event)"></button>

<input type="text" (input)="inputChange($event)" name="" id="" />

//button 获取 input 
<input #userName type="text" (input)="inputChange($event)" name="" id="" />   //#userName模板引用变量
<button (click)="getUserName(userName.value)"></button>
```

#### **js**

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.less']
})
export class AppComponent {
  clickFun(e:Event){
      console.log(e,"点击了按钮")
  }
    
  inputChange(e:Event){
      console.log(e.target.vlaue,"input值变动")
  }
    
  getUserName(value:string){
      console.log(value,"拿到输入框的数据")
  }
}
```

<!-- tabs:end -->



### 七、模板引用变量

<!-- tabs:start -->

#### **html**

```jsx
<div #box>
    <input type="text"></input>
    <button>按钮</button>
</div>
<button (Click)="getDomForBox(box)"> 点击获取到上面的模板 </button>
```

#### **js**

```javascript
export class AppComponent {
  getDomForBox(box){
      console.log(box)
  }
}
```

<!-- tabs:end -->

### 八、数据双向绑定

双向绑定只对表单元素有效-使用前需导入 **FormsModule** 模块

<!-- tabs:start -->

#### **html**

```html
<div>
	输入：<input [(ngModule)]="username">
</div>
```

#### **js**

```javascript
export class AppComponent {
 username:string = "用户名"
}
```

#### **xx.module.js**

```javascript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
<!-- 引入FormsModule -->
import { FormsModule } from '@angular/forms';

@NgModule({
  //声明组件内用到的视图
  declarations: [
    AppComponent
  ],
  //引入模块需要的类
  imports: [
    BrowserModule,
    AppRoutingModule,
<!-- 声明FormsModule -->
    FormsModule
  ],2
  //全局服务
  providers: [],
  //根组件
  bootstrap: [AppComponent]
})
export class AppModule { }
```

<!-- tabs:end -->

### 九、动态表单Form控件

使用表单控件三步骤

1. 注册响应式表单模块，该模块声明响应式表单中的一些指令
2. 生成一个新的FromControl实力，并保存在组件中
3. 在模板中注册这个FromControl

<!-- tabs:start -->

#### **html**

```html
<div>
    <!-- 单个 动态表单控件-->
    Myfroms:<inpu type="test" [FormControl]="Myfroms">
</div>
    
    <!-- 多个 动态表单控件组 -->
<from [formGroup]="loginForm">
    <label>
        账号：<input type="text" formControlName="userName">
    </label>
    <label>
        密码：<input type="passworld" formControlName="passworld">
    </label>
        <button (click)="submitForm()"></button>
</from>
```

#### **js**

```javascript
import { Component } from '@angular/core';
import { FormControl,FromGroup } from '@angular/forms'

@Component({ ... })
export class AppComponent {
            
   <!-- 单个响应式 -->
  Myfroms:FormControl = new FormControl('')    //这个是一个对象{ value:'' }
  printMyfroms(){
      console.log(this.Myfroms.value)
      // Myfroms的值不能直接  this.Myfroms = 'xxxx' (报错)   
      // 需要用固定写法： this.Myfroms.setValue('xxxx')  正确
  }
          
            
 <!-- 多个值响应式 -->
 loginFrom:FromGroup = new FromGroup({
     userName: new FormControl(''),
     passworld: new FormControl(''),
  })
  
  // 提交表单           
  submitForm(){ 
      console.log(this.loginFrom.value) 
  }
                           
}
```

#### **xx.module.ts**

```javascript
import { FormsModule,ReactiveFormsModule } from '@angular/forms'

@NgModule({
   //...
  imports: [
      //...注册 响应式表单控件
      FormsModule,
      ReactiveFormsModule
  ]
})
export class AppModule { }
```

<!-- tabs:end -->



#### 实例

<!-- tabs:start -->

#### **html**

```html
<from active="">
  账号：<input required #nameInpA="ngModel" type="text" [(ngModel)]="fromData.name" name="userName">
    <br>
    <span >验证结果：{{ nameInpA.valid }}</span>
    <span *ngIf="!nameInpA.valid">请输入账号</span>
    <hr>
  密码：<input required #pasInB="ngModel" type="text" [(ngModel)]="fromData.password" name="password">
    <br>
    <span >验证结果：{{ pasInpB.valid }}</span>
    <span *ngIf="!pasInp.valid">请输入密码</span>
    <hr>
        <button (click)="submitFrom()">提交</button>
</from>
        
 总结：
        required = 必填
        #nameInpA="ngModel"  = userName输入框的验证结果状态 nameInpA.valid （有效性）
        #pasInB="ngModel"  = password输入框的验证结果状态 pasInB.valid （有效性）
```

#### **js**

```javascript
import { Component } from '@angular/core';
import { FormControl,FromGroup } from '@angular/forms'

export class AppComponent {
 fromData = {
     userName:'',
     password:''
 }                          
}
```

#### **xx.module.ts**

```javascript
import { FormsModule,ReactiveFormsModule } from '@angular/forms'
@NgModule({
   //...
  imports: [
      //...注册 响应式表单控件
      FormsModule,
      ReactiveFormsModule
  ]
})
export class AppModule { }
```

#### **ngModel跟踪修改状态与有效性验证**

| 状态             | true类     | false类      |
| ---------------- | ---------- | ------------ |
| 控件已经被访问过 | ng-touched | ng-untouched |
| 控件值已经变化   | ng-dirty   | ng-pristine  |
| 控件值是有效的   | ng-valid   | ng-invalid   |

#### **状态类style修改**

```css
.na-invalid{
    border-color:red;   //验证不通过时，表单边框变红色
}
```

<!-- tabs:end -->

### 十、自定义表单验证

<!-- tabs:start -->

#### **html**

```html
<form active="" [FormControl]="valiDataFrom">
    <label>
        账号：<input type="text" formControlName="userName">
    </label>
        <p *ngIf="valiDataFrom.get('userName')?.errors?.required">请输入账号</p>
        <p *ngIf="valiDataFrom.get('userName')?.errors?.maxLength?.requiredLength">账号请输入长度为4-19位</p>
        <p *ngIf="valiDataFrom.get('userName')?.errors?.minLength?.requiredLength">账号请输入长度为4-19位</p>
        
        
    <label>
        密码：<input type="text" formControlName="userName">
    </label>
        <p *ngIf="valiDataFrom.get('userName')?.errors?.required">请输入密码</p>
        <p *ngIf="valiDataFrom.get('password')?.errors?.msg">{{valiDataFrom.get('password').errors.msg}}</p>
        
        
    <label>
        手机号：<input type="text" formControlName="userName">
        ......
    </label>
        
        <button (click)="submitForm()">提交</button>
        .......
</form>
```

#### **ts**

```javascript
import { Component } from '@angular/core';
import { FormControl，FormGroup,FormBuilder, Validators} from '@angular/forms'

export class AppComponent {
  // 一、构造函数里注入 FormBuilder
  	constructor(private fb:FormBuilder){ } 
  // 二、错误提醒数据
    formErrors = {
        "title":'',
        "content":''
    }
  // 三、在组件类的初始化函数里对表单中的元素的校验进行定义，并调用表单的valueChanges方法，检测表单的输入变化

    valiDataFrom:FormGroup = this.fb.groub({
       		userName:['',[Validators.required,Validators.maxLength(18),Validators.minLength(6)]],
       		password:["",[this.passWordVal]],ss
       		phone:['',[Validators.required,this.phoneVal]]
       })

    
    //验证手机号的自定义方法
    phoneVal(phone:FormControl):object {
        const value = phone.value || '';
        if(!value) return {desc:'请输入手机号'}
        const valid = /[0-9]{11}/.test(value)
        return valid ? {} : { desc:'联系电话必须是11位数字' }
    }

	//验证密码的自定义方法
	passWordVal(password:FormControl):object {
        const value = password || "";
        const valid = value.match(/^[a-zA-Z]{1}([a-zA-Z0-9]|[._]){4,19}$/)
        return valid ? { } : {passwordValidator : {desc:'只能输入5-20个以字母开头、可带数字、“_”、“.”的字串'}}
    }


	submitForm(){
        console.log(this.valiDataFrom.errors)   //查看哪里验证不通过
    }
    
}
```

#### **app.module.ts**

```javascript
import { FormsModule,ReactiveFormsModule } from '@angular/forms'
@NgModule({
   //...
  imports: [
      //...注册 响应式表单控件
      FormsModule,
      ReactiveFormsModule
  ]
})
export class AppModule { }
```

<!-- tabs:end -->



### 十一、管道 pipe

- {{ 输入数据 | 管道: 管道参数 }} 
- 链式管道 {{ 数据 | A | B }}  先执行A 管道 --> B管道
- {{date | date: 'fullDate' | uppercase}}

<!-- tabs:start -->

#### **html**

```javascript
<div>{{dateTime | data:'yyyy-mm-dd HH:mm:ss'}}</div>  //时间格式2021-09-12 15:19:00
<div>{{ }}</div>    JsonPipe 将输入数据对象经过JSON.stringify() 方法转换后输出对象的字符串
<div>{{ }}</div>    UpperCasePipe 小写字母转大写
<div>{{ }}</div>    LowerCasePipe 大写转小写
<div>{{ }}</div>	DecomalPipe	  将数值按照特定的格式显示文本
<div>{{ }}</div>    CurrentcyPipe 将数值进行货币格式化处理
<div>{{ }}</div>	SlicePipe	  将数组或字符串剪成新子集
<div>{{ }}</div>	PercentPipe	  将数值转百分比格式
```

#### **js**

```javascript
import { Component } from '@angular/core';
import { FormControl,FromGroup } from '@angular/forms'

export class AppComponent {
	dateTime:Date = new Date()                        
}

```

#### **自定义管道**

```js
//cli创建管道  路径 ：项目下跟src/pipes/test    cli创建会自动在app.module.ts 中引入 declarations：{ TestPipe }
命令 ： ng g p pipes/test    

//test.pipe.ts	     代码
//test.pipe.spec.ts  测试文件
```

#### **test.pipe.ts**

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





<!-- tabs:start -->

#### **html**

```html
快捷
```

#### **js**

```javascript

```

<!-- tabs:end -->

