# Docsify 工具简单教程

<hr/>


#### 一、tabs分栏
注释开头 注释结尾
 <!-- tabs:start -->
#### **写法**

```javascript
    <!-- tabs:start -->
    #### **分页A**
    A内容
    #### **分页B**
    A内容
    <!-- tabs:start -->
```

#### **JavaScript**


```javascript
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

export class NzDemoFormNormalLoginComponent implements OnInit {
  validateForm!: FormGroup;

  submitForm(): void {
    for (const i in this.validateForm.controls) {
      if (this.validateForm.controls.hasOwnProperty(i)) {
        this.validateForm.controls[i].markAsDirty();
        this.validateForm.controls[i].updateValueAndValidity();
      }
    }
  }

  constructor(private fb: FormBuilder) {}

  ngOnInit(): void {
    this.validateForm = this.fb.group({
      userName: [null, [Validators.required]],
      password: [null, [Validators.required]],
      remember: [true]
    });
  }
}
```

#### **Html**

```html
<form nz-form [formGroup]="validateForm" class="login-form" (ngSubmit)="submitForm()">
  <nz-form-item>
    <nz-form-control nzErrorTip="Please input your username!">
      <nz-input-group nzPrefixIcon="user">
        <input type="text" nz-input formControlName="userName" placeholder="Username" />
      </nz-input-group>
    </nz-form-control>
  </nz-form-item>
  <nz-form-item>
    <nz-form-control nzErrorTip="Please input your Password!">
      <nz-input-group nzPrefixIcon="lock">
        <input type="password" nz-input formControlName="password" placeholder="Password" />
      </nz-input-group>
    </nz-form-control>
  </nz-form-item>
  <div nz-row class="login-form-margin">
    <div nz-col [nzSpan]="12">
      <label nz-checkbox formControlName="remember">
        <span>Remember me</span>
      </label>
    </div>
    <div nz-col [nzSpan]="12">
      <a class="login-form-forgot">Forgot password</a>
    </div>
  </div>
  <button nz-button class="login-form-button login-form-margin" [nzType]="'primary'">Log in</button>
  Or
  <a>register now!</a>
</form>
```

#### **CSS**

```css
.login-form {
        max-width: 300px;
      }

      .login-form-margin {
        margin-bottom: 16px;
      }

      .login-form-forgot {
        float: right;
      }

      .login-form-button {
        width: 100%;
      }
```

<!-- tabs:end -->


#### 二、左右分栏

<!-- panels:start -->

<!-- div:title-panel -->
标题栏

<!-- div:left-panel -->
```ts

    <徐!-- panels:start -->
        <成!-- div:title-panel -->
                    标题栏
        <东!-- div:left-panel -->
                    左边写描述、说明
        <修!-- div:right-panel -->
                    代码块
    <改!-- panels:end -->
```

<!-- div:right-panel -->
右边给左边的代码块写描述、说明

这里写代码块有点小影响

是由注释作分割，里面的文字要删除掉

"徐成东修改"
<!-- panels:end -->