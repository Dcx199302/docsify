# Form



### 一、模板驱动表单  [(ngModel)]

<!-- tabs:start -->

#### **js-1**

```javascript
//1.无数据类型定义.js
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-ngform',
  templateUrl: './ngform.component.html',
  styleUrls: ['./ngform.component.less']
})
export class NgformComponent implements OnInit {
  constructor() {}
  ngOnInit(): void {}

  model = {                        //1.模板驱动型表单
    id:132,
    name:""
  }

  submitted = false;
  onSubmit() { this.submitted = true; }   //2.提交的时候把this.model发出去

}
```

#### **js-2**

```javascript
//2.interface定义数据类型.js
import { Component, OnInit } from '@angular/core';

interface Heros {    //1.定义数据类型
    id: number,
    name: string,
    power?: string,
    alterEgo?: string
}

@Component({
 ....
})

export class NgformComponent implements OnInit {
  ...
  
  model:Heros = {    //2.约束类型
    id:132,
    name:""
  }

  submitted = false;
  onSubmit() { this.submitted = true; }   //提交时候- 发出数据this.model
}
```

#### **js-3**

```javascript
//3.使用类class定义数据类型
import { Component, OnInit } from '@angular/core';

export class Hero {     //1. class定义数据类型
  constructor(
    public id: number,
    public name: string,
    public power?: string,
    public alterEgo?: string
  ) {}
}

@Component({
	...
})

export class NgformComponent implements OnInit {
	...   
  model = new Hero(18, '');    //2.new 对应类型的数据

  submitted = false;
  onSubmit() { this.submitted = true; }

  //newHero() {  
  // 	this.model = new Hero(42, '');   //new 新表单-给model
  //}

}
```





#### **html**

注意点

- #heroForm
  -  代表Angular的获取 整个 form  （div等其他也这样用..） 相当于打标识 -- 这里的表单有状态.. 像一个对象包含表单的状态和方法等... 、例如：这里的 heroForm.form.valid（表单验证是否有效）和 heroForm.reset()    （表单重置）

- #nameStatus="ngModel"  
  - 同上面差不多，也是包含了输入状态判断 nameStatus.valid （验证是否有效）和 nameStatus.pristine （ 初始，没输入前）

```html
    <form (ngSubmit)="onSubmit()" #heroForm="ngForm">
      <div class="form-group">
        <label for="name">Name</label>
        <input type="text" class="form-control" id="name" required  [(ngModel)]="model.name" name="name" #nameStatus="ngModel">
        <div [hidden]="nameStatus.valid || nameStatus.pristine" class="alert alert-danger">
          Name is required 描述
        </div>
      </div>

      <button type="submit" class="btn btn-success" [disabled]="!heroForm.form.valid">Submit</button>
      <button type="button" class="btn btn-default" (click)="newHero(); heroForm.reset()">New Hero</button>
    </form>

```

```html
<!-- 关于表单的html基础知识 -->    
    <form (ngSubmit)="onSubmit()" #heroForm="ngForm">      <!-- ng的表单提交事件 (ngSubmit)="onSubmit()" -->
        												   <!-- #heroForm="ngForm"   标记下面当前表单的整体状态，下面用 -->
      <div class="form-group">
        <label for="name">Name</label>  				   <!-- <label for="name"></label>     html增加input的点击范围用的 -->
          													
        <input type="text" class="form-control" id="name" required [(ngModel)]="model.name" name="name" #nameStatus="ngModel">
          	<!-- id="name"   配合 label for="name" -->
             <!-- required 必填 - 好像是原生的验证条件，还有其他的--百度 >   									  
             <!-- ngModel双向绑定  name="xxxx" -> 必填，不清楚          ng 标识：当前输入框的状态 -->
          
        <div [hidden]="nameStatus.valid || nameStatus.pristine" class="alert alert-danger">   //获取input的输入状态--看注意点
          Name is required
        </div>
      </div>
	<!--       第二项：带下拉框的表单选项
        <div class="form-group">
			<label for="power">Hero Power</label>
            <select class="form-control" id="power" required  [(ngModel)]="model.power" name="power" #power="ngModel">
              <option *ngFor="let pow of powers" [value]="pow">{{pow}}</option>
            </select>
            <div [hidden]="power.valid || power.pristine" class="alert alert-danger">
              Power is required
            </div>
        </div> 
	-->
      <button type="submit" class="btn btn-success" [disabled]="!heroForm.form.valid">Submit</button> // form标识的状态方法-看注意点
      <button type="button" class="btn btn-default" (click)="newHero(); heroForm.reset()">New Hero</button>
    </form>
```





#### **app.module.ts**

```javascript
//...省略无关代码
import { FormsModule, ReactiveFormsModule } from '@angular/forms';

@NgModule({
  	imports: [
    	FormsModule,
    	ReactiveFormsModule
  	]
})
```





<!-- tabs:end -->





### 二、响应式的表单

准备工作 app.module.ts

```
import { ReactiveFormsModule } from '@angular/forms';

@NgModule({
  imports: [
    // other imports ...
    ReactiveFormsModule
  ],
})
export class AppModule { }
```





#### 1、基本的表单控件

<!-- tabs:start -->

#### **js**

```javascript
import { Component, OnInit } from '@angular/core';
import { FormControl } from '@angular/forms';

@Component({
  selector: 'app-reactive-form',
  templateUrl: './reactive-form.component.html',
  styleUrls: ['./reactive-form.component.less']
})
export class ReactiveFormComponent implements OnInit {
  constructor() { }
  ngOnInit(): void {}
  
  name = new FormControl('');	
  
	HandleSubmit(){
        console.log(this.name)  //发送数据
    }

}
```

#### **html**

```html
<!-- 在组件类中创建控件后，必须将其与模板中的表单控件元素相关联。
使用formControl提供的绑定更新带有表单控件的模板，该绑定FormControlDirective也包含在ReactiveFormsModule. -->

<label for="name">Name: </label>
<input id="name" type="text" [formControl]="name">
```

#### **name.JSON**

```json
//name = new FormControl('') 表单控件长下面这样
{ 
"_hasOwnPendingAsyncValidator": false, 
"pristine": true, 
"touched": true, 
"onDisabledChange": [ null ], 
"rawValidators": null, 
"rawAsyncValidators": null, 
"composedValidatorFn": null, 
"composedAsyncValidatorFn": null, 
"onChange": [ null ], 
"pendingValue": "", 
"value": "", 
"status": "VALID", 
"errors": null, 
"valueChanges": { 
      "_isScalar": false, 
      "observers": [], 
      "closed": false, 
      "isStopped": false, 
      "hasError": false, 
      "thrownError": null, 
      "__isAsync": false 
}, 
  "statusChanges": { 
        "_isScalar": false, 
        "observers": [], 
        "closed": false, 
        "isStopped": false, 
        "hasError": false, 
        "thrownError": null, 
        "__isAsync": false 
},
  "_pendingTouched": true 
}
```



<!-- tabs:end -->



#### 2、分组表单--手动创建实例

<!-- tabs:start -->

#### **js**

```javascript
import { Component, OnInit } from '@angular/core';
import { FormControl,FormGroup } from '@angular/forms';

@Component({
  selector: 'app-reactive-form',
  templateUrl: './reactive-form.component.html',
  styleUrls: ['./reactive-form.component.less']
})
export class ReactiveFormComponent implements OnInit {
  constructor() { }
  ngOnInit(): void {}

  profileForm = new FormGroup({
    firstName: new FormControl(''),
    lastName: new FormControl(''),
    address: new FormGroup({
      street: new FormControl(''),
      city: new FormControl(''),
      state: new FormControl(''),
      zip: new FormControl('')
    })
  });

  updateProfile() {
    // 用js方式给表单赋值   不能直接 profileForm.firstName = 'abc'
    this.profileForm.patchValue({
      firstName: 'Nancy',
      address: {
        street: '123 Drew Street'
      }
    });
  }

  onSubmit() {
    // 拿到数据 --发送
    console.log(this.profileForm.value);
  }

}
```

#### **html**

```html
<form [formGroup]="profileForm" (ngSubmit)="onSubmit()">

    <label for="first-name">First Name: </label>
    <input id="first-name" type="text" required formControlName="firstName">
  
    <label for="last-name">Last Name: </label>
    <input id="last-name" type="text" formControlName="lastName">

    <div formGroupName="address">
      <h2>Address</h2>
    
      <label for="street">Street: </label>
      <input id="street" type="text" formControlName="street">
    
      <label for="city">City: </label>
      <input id="city" type="text" formControlName="city">
    
      <label for="state">State: </label>
      <input id="state" type="text" formControlName="state">
    
      <label for="zip">Zip Code: </label>
      <input id="zip" type="text" formControlName="zip">
    </div>

    <p>Complete the form to enable button.</p>
    <button type="submit" [disabled]="!profileForm.valid">Submit</button>
  </form>
  <button (click)="updateProfile()">Update Profile</button>

  <!-- {{ profileForm.value }} -->
  {{ profileForm.value | json }}
  {{ profileForm.value.address | json }}
```

<!-- tabs:end -->





#### 3、使用 FormBuilder 服务生成控件--表单生成器

<!-- tabs:start -->

#### **js**

```javascript
import { Component, OnInit } from '@angular/core';
import { FormBuilder, Validators } from '@angular/forms';

@Component({
  selector: 'app-reactive-form',
  templateUrl: './reactive-form.component.html',
  styleUrls: ['./reactive-form.component.less']
})
export class ReactiveFormComponent implements OnInit {


  // 该FormBuilder服务有三种方法：control()，group()，和array()。这些是用于在组件类中生成实例的工厂方法，包括表单控件、表单组和表单数组。
  constructor(private fb:FormBuilder) {}
  ngOnInit(): void {}

   profileForm = this.fb.group({
    firstName: ['',[Validators.required]],
    lastName: [''],
    address: this.fb.group({
      street: [''],
      city: [''],
      state: [''],
      zip: ['']
    }),
  });

  
}
```

#### **html**

```html
<form [formGroup]="profileForm" (ngSubmit)="onSubmit()">

    <label for="first-name">First Name: </label>
    <input id="first-name" type="text" required formControlName="firstName">
  
    <label for="last-name">Last Name: </label>
    <input id="last-name" type="text" formControlName="lastName">

    <div formGroupName="address">
      <h2>Address</h2>
    
      <label for="street">Street: </label>
      <input id="street" type="text" formControlName="street">
    
      <label for="city">City: </label>
      <input id="city" type="text" formControlName="city">
    
      <label for="state">State: </label>
      <input id="state" type="text" formControlName="state">
    
      <label for="zip">Zip Code: </label>
      <input id="zip" type="text" formControlName="zip">
    </div>

    <p>Complete the form to enable button.</p>
    <button type="submit" [disabled]="!profileForm.valid">Submit</button>
  </form>
  <button (click)="updateProfile()">Update Profile</button>

  <!-- {{ profileForm.value }} -->
  <p>Form Status: {{ profileForm.status }}</p>
  {{ profileForm.value | json }}
  {{ profileForm.value.address | json }}

```

<!-- tabs:end -->



#### 4.手动创建和表单生成器对比

<!-- tabs:start -->

#### **手动创建实例**

```javascript
profileForm = new FormGroup({
  firstName: new FormControl(''),
  lastName: new FormControl(''),
  address: new FormGroup({
    street: new FormControl(''),
    city: new FormControl(''),
    state: new FormControl(''),
    zip: new FormControl('')
  })
});
```

#### **表单生成器**

```javascript
profileForm = this.fb.group({
  firstName: [''],
  lastName: [''],
  address: this.fb.group({
    street: [''],
    city: [''],
    state: [''],
    zip: ['']
  }),
});
```



<!-- tabs:end -->



#### 5.添加随时增减的input框



<!-- tabs:start -->

#### **FormArray.js**

```javascript
import { Component, OnInit } from '@angular/core';
import { FormBuilder, Validators,FormArray } from '@angular/forms';

@Component({
  selector: 'app-reactive-form',
  templateUrl: './reactive-form.component.html',
  styleUrls: ['./reactive-form.component.less']
})
export class ReactiveFormComponent implements OnInit {
  constructor(private fb:FormBuilder) {}
   ngOnInit(): void {}

   profileForm = this.fb.group({
    firstName: ['',[Validators.required]],
    lastName: [''],
    address: this.fb.group({
      street: [''],
      city: [''],
      state: [''],
      zip: ['']
    }),
    aliases: this.fb.array([
      this.fb.control('')
    ])
  });

  // （与重复profileForm.get()获取每个实例的方法相比，getter 可以轻松访问表单数组实例中的别名。
  // 表单数组实例表示数组中未定义数量的控件。通过 getter 访问控件很方便，而且这种方法很容易重复用于其他控件。（别名getter）
  get aliases() {
    return this.profileForm.get('aliases') as FormArray;
  }

  addAlias(e) {     //随时添加一个输入控制的input框
    e.preventDefault()
    this.aliases.push(this.fb.control(''));
  }

}
```



#### **html**

```html
<form [formGroup]="profileForm" (ngSubmit)="onSubmit()">

    <label for="first-name">First Name: </label>
    <input id="first-name" type="text" required formControlName="firstName">
  
    <label for="last-name">Last Name: </label>
    <input id="last-name" type="text" formControlName="lastName">

    <div formGroupName="address">
      <h2>Address</h2>
    
      <label for="street">Street: </label>
      <input id="street" type="text" formControlName="street">
    
      <label for="city">City: </label>
      <input id="city" type="text" formControlName="city">
    
      <label for="state">State: </label>
      <input id="state" type="text" formControlName="state">
    
      <label for="zip">Zip Code: </label>
      <input id="zip" type="text" formControlName="zip">
    </div>

    <div formArrayName="aliases">
      <h2>Aliases</h2>
      <button (click)="addAlias($event)">+ Add another alias</button>    <!-- 增加多个input框 -->
    
      <div *ngFor="let alias of aliases.controls; let i=index">
        <!-- The repeated alias template -->
        <label for="alias-{{ i }}">Alias:</label>
        <input id="alias-{{ i }}" type="text" [formControlName]="i">
      </div>
    </div>

    <p>Complete the form to enable button.</p>
    <button type="submit" [disabled]="!profileForm.valid">Submit</button>
  </form>
  <button (click)="updateProfile()">Update Profile</button>
```



<!-- tabs:end -->