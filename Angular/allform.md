# 响应式表单



<!-- tabs:start -->

#### **单个控件FormControl**

- 第一步：在你的app应用中注册响应式表单模块，该模块声明了一些你要用在响应式表单中的指令。

  - ```typescript
    //app.module.ts
    
    import { ReactiveFormsModule } from '@angular/forms';
    
    imports:[ FormsModule,ReactiveFormsModule .... ]
    ```

    

- 第二步：生成一个新的 `FormControl` 实例，并把它保存在组件中。

  - ```typescript
    name = new FormControl('');
    /**可以以用 FormControl 的构造函数设置初始值，这个例子中它是空字符串。
    通过在你的组件类中创建这些控件，你可以直接对表单控件的状态进行监听、修改和校验。*/
    
    创建了控件之后，你还要把它和模板中的一个表单控件关联起来
    ```

  

- 第三步：在模板中注册这个 `FormControl`。

  - ```html
    <label>
      Name:    
      <input type="text" [formControl]="name">
    </label>
    <!-- 可能报错：这样写好像会提示 [formControl] 指令需要导入，可能是因为二级路由的原因，试试在二级路由下面再导入一次 --> 
    <!-- imports:[ FormsModule,ReactiveFormsModule .... ] -->
    ```



#### **控件map组FormGroup**

- 第一步：创建一个 `FormGroup` 实例。

  - ```javascript
    import { FormGroup, FormControl } from '@angular/forms';
    
    /**这些独立的表单控件被收集到了一个控件组中,
       这个 FormGroup 用对象的形式提供了它的模型值，这个值来自组中每个控件的值
       FormGroup 实例拥有和 FormControl 实例相同的属性（比如 value、untouched）和方法（比如 setValue()）
    */
    profileForm = new FormGroup({
        firstName: new FormControl(''),
        lastName: new FormControl(''),
    });
    ```

  

- 第二步：把这个 `FormGroup` 模型关联到视图。

  - ```html
    <form [formGroup]="profileForm">
      
      <label>
        First Name:
        <input type="text" formControlName="firstName">
      </label>
    
      <label>
        Last Name:
        <input type="text" formControlName="lastName">
      </label>
    
    </form>
    ```

    

- 第三步：保存表单数据。

  - ```javascript
    onSubmit() {
      // 待办事项:使用事件发射器和表单值
      console.log(this.profileForm.value);
    }
    ```

  - ```html
    <form [formGroup]="profileForm" (ngSubmit)="onSubmit()">
      <label>
        First Name:
        <input type="text" formControlName="firstName" />
      </label>
    
      <label>
        Last Name:
        <input type="text" formControlName="lastName" />
      </label>
      <button>点击发送表单： 事件绑定在fom标签了</button>
    
      <button type="submit" [disabled]="!profileForm.valid">Submit</button>
    </form>
    显示表单最新的数据:{{ profileForm.value | json }}
    ```



#### **嵌套多层的 FormGroup**

某些类型的信息天然就属于同一个组。比如名称和地址就是这类嵌套组的典型例子

- 创建一个嵌套的表单组。

  - ```javascript
    import { FormGroup, FormControl } from '@angular/forms';
    
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

    

- 在模板中对这个嵌套表单分组。

  - ```html
    <div formGroupName="address">
      <h3>Address</h3>
    
      <label>
        Street:
        <input type="text" formControlName="street">
      </label>
    
      <label>
        City:
        <input type="text" formControlName="city">
      </label>
      
      <label>
        State:
        <input type="text" formControlName="state">
      </label>
    
      <label>
        Zip Code:
        <input type="text" formControlName="zip">
      </label>
    </div>
    ```

#### **更新部分数据模型**

有两种更新模型值的方式：

`setValue()` 方法的严格检查可以帮助你捕获复杂表单嵌套中的错误，而 `patchValue()` 在遇到那些错误时可能会默默的失败。

- 使用 `setValue()` 方法来为单个控件设置新值。 `setValue()` 方法会严格遵循表单组的结构，并整体性替换控件的值。

- 使用 `patchValue()` 方法可以用对象中所定义的任何属性为表单模型进行替换。

  - ```javascript
    //使用 updateProfile 方法传入下列数据可以更新用户的名字与街道住址。
    updateProfile() {
      this.profileForm.patchValue({
        firstName: 'Nancy',
        address: {
          street: '123 Drew Street'
        }
      });
    }
    
    /**
    当点击下面button按钮时，profileForm 模型中只有 firstName 和 street 被修改了。
    注意，street 是在 address 属性的对象中被修改的。
    这种结构是必须的，因为 patchValue() 方法要针对模型的结构进行更新。
    
    patchValue() 只会更新表单模型中所定义的那些属性。
    */
    ```

  - ```html
    <!-- 通过往模板中添加一个按钮来模拟一次更新操作，以修改用户档案。 -->
    <p>
      <button (click)="updateProfile()">Update Profile</button>
    </p>
    ```

  - 



#### **FormBuilder表单生成器**

- 当需要与多个表单打交道时，手动创建多个表单控件实例会非常繁琐。`FormBuilder` 服务提供了一些便捷方法来生成表单控件
- 用 `FormBuilder` 来代替手工创建这些 `FormControl` 和 `FormGroup` 实例。



- ###### 第一步：导入 `FormBuilder` 类。

  - ```javascript
    import { FormBuilder } from '@angular/forms';
    ```

    

- ###### 第二步：注入这个 `FormBuilder` 服务。

  - ```javascript
    //FormBuilder 是一个可注入的服务提供者，它是由 ReactiveFormModule 提供的。只要把它添加到组件的构造函数中就可以注入这个依赖。
    
    class Name {
        constructor(private fb: FormBuilder) { }
    }
    ```

    

- ###### 第三步：生成表单控件。

  - `FormBuilder` 服务有三个方法：`control()`、`group()` 和 `array()`。
  - 这些方法都是工厂方法，用于在组件类中分别生成 `FormControl`、`FormGroup` 和 `FormArray`。

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
  
  /**
  在上面的例子中，你可以使用 group() 方法，用和前面一样的名字来定义这些属性。
  这里，每个控件名对应的值都是一个数组，这个数组中的第一项是其初始值。 
  
  提示：你可以只使用初始值来定义控件，但是如果你的控件还需要同步或异步验证器，
  那就在这个数组中的第二项和第三项提供同步和异步验证器
  */
  ```

  

#### **验证表单输入**

- *表单验证*用于确保用户的输入是完整和正确的。
- 响应式表单包含了一组开箱即用的常用验证器函数。
- 这些函数接收一个控件，用以验证并根据验证结果返回一个错误对象或空值。

```javascript
//导入验证器函数
//从 @angular/forms 包中导入 Validators 类。
import { Validators } from '@angular/forms';
```

```javascript
//示例：
profileForm = this.fb.group({
  firstName: ['', Validators.required],
  lastName: [''],
  address: this.fb.group({
    street: [''],
    city: [''],
    state: [''],
    zip: ['']
  }),
});
```

- HTML5 有一组内置的属性，用来进行原生验证，
- 包括 `required`、`minlength`、`maxlength` 等。
- 虽然是*可选的*，不过你也可以在表单的输入元素上把它们添加为附加属性来使用它们。
- 这里我们把 `required` 属性添加到 `firstName` 输入元素上。

```javascript
<input type="text" formControlName="firstName" required>
    //提示： H5验证可以和Validtors 组合使用~ 
```



#### **显示表单状态**

- 当你往表单控件上添加了一个必填字段时，它的初始值是无效的（invalid）。
- 这种无效状态会传播到其父 `FormGroup` 元素中，也让这个 `FormGroup` 的状态变为无效的。
- 你可以通过该 `FormGroup` 实例的 `status` 属性来访问其当前状态。

```html
<p>
  Form Status: {{ profileForm.status }}
</p>

<!-- 当必填的input框不通过验证的时候， invalid状态 下面绑定disabled="!profileForm.valid"的button 不能点击 -->
<button type="submit" [disabled]="!profileForm.valid">Submit</button>  
```





#### **创建动态表单FormArray**

- 第一步：导入 `FormArray` 类。

  - ```javascript
    import { FormArray } from '@angular/forms';
    ```

    

- 第二步：定义一个 `FormArray` 控件。

  - ```javascript
    //你可以通过把一组（从零项到多项）控件定义在一个数组中来初始化一个 FormArray。
    
    profileForm = this.fb.group({
      firstName: ['', Validators.required],
      lastName: [''],
      address: this.fb.group({
        street: [''],
        city: [''],
        state: [''],
        zip: ['']
      }),
        
    /** FormGroup 中的这个 aliases 控件现在管理着一个控件，将来还可以动态添加多个。*/
      aliases: this.fb.array([
        this.fb.control('')
      ])
        
    });
    ```

  - 

- 第三步：使用 getter 方法访问 `FormArray` 控件。

  - 相对于重复使用 `profileForm.get()` 方法获取每个实例的方式，

  - getter 可以让你轻松访问表单数组各个实例中的别名。 表单数组实例用一个数组来代表未定数量的控件。

  - 通过 getter 来访问控件很方便，这种方法还能很容易地重复处理更多控件。

  - ```javascript
    get aliases() {
      return this.profileForm.get('aliases') as FormArray;
    }
    //注意：因为返回的控件的类型是 AbstractControl，所以你要为该方法提供一个显式的类型声明来访问 FormArray 特有的语法。
    ```

- 第四步：

  - 定义一个方法来把一个绰号控件动态插入到绰号 `FormArray` 中。

  - 用 `FormArray.push()` 方法把该控件添加为数组中的新条目。

  - ```javascript
    //给数组增加子控件的写法
    addAlias() {
      this.aliases.push(this.fb.control(''));
    }
    ```



- 第五步：在模板中显示这个表单数组。
  - 要想为表单模型添加 `aliases`，你必须把它加入到模板中供用户输入。
  - 和 `FormGroupNameDirective` 提供的 `formGroupName` 一样，
  - `FormArrayNameDirective` 也使用 `formArrayName` 在这个 `FormArray` 实例和模板之间建立绑定。

```html
<div formArrayName="aliases">
  <h3>Aliases</h3> <button (click)="addAlias()">Add Alias</button>

  <div *ngFor="let alias of aliases.controls; let i=index">
    <!-- The repeated alias template -->
    <label>
      Alias:
      <input type="text" [formControlName]="i">
    </label>
  </div>
</div>

<!-- *ngFor 指令对 aliases FormArray 提供的每个 FormControl 进行迭代。
因为 FormArray 中的元素是匿名的，所以你要把索引号赋值给 i 变量，
并且把它传给每个控件的 formControlName 输入属性。 -->
```



<!-- tabs:end -->
