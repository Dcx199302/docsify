# AN进阶


## 父子传值
<!-- tabs:start -->

#### **子组件.ts**

```javascript
import { Component, OnInit,Output, EventEmitter, Input } from '@angular/core';
import { LoginService } from 'src/app/services/login/login.service';
import { environment } from 'src/environments/environment';

interface Captcha{
  uid:string;
  imageName:string;
  values:string[];
  newListArray:string[]
}

@Component({
  selector: 'app-verification-code',
  templateUrl: './verification-code.component.html',
  styleUrls: ['./verification-code.component.less']
})

export class VerificationCodeComponent implements OnInit {
  constructor(private service: LoginService) {}
  ngOnInit(): void {}

  @Input()  PhoneNumber:number
  @Output() notify = new EventEmitter(); 

  iconSpin:boolean = false  //icon加载中
  empty = {uid:'',imageName:'', values:[],newListArray:[]}  // 空的
  CaptchaData:Captcha = this.empty  // 有数据

  //获取验证码
  getCaptcha(){
    this.iconSpin = true
    this.CaptchaData = this.empty

    this.service.getCaptchaImages(5).subscribe(data=>{
      const {uid, values,imageName } = data;

      const newData = values.map((item,index) => {
        return `${environment.AUTH_CAPTCHA}${uid}&index=${index}`
      });
      
      this.CaptchaData = {uid,imageName, values,newListArray:newData}
    })
    setTimeout(()=>{
      this.iconSpin = false
    },500)
  }

  // 处理有效的验证码
  handleValidCodecaptcha(numb){
    const {uid,values} = this.CaptchaData
    this.service.validCapchaImage(uid, values[numb]).subscribe(
      data=>{
        this.notify.emit(this.CaptchaData)
        this.CaptchaData = this.empty
        console.log("拿到号码：发送短信",this.PhoneNumber);
        
      },
      err =>{
        alert('点击错误，重新选择')
        setTimeout(() => {
          this.getCaptcha()
        }, 1000);
      }
    )
  }
    
}
```



#### **子组件.html**

```html
<div style="position: relative;position: absolute;width: 400px;background-color: #fff;">
    <div style="display: flex;justify-content: space-between;" *ngIf="CaptchaData.values.length > 1">
        <span>点击图中 <a>{{CaptchaData.imageName}}</a> 获取验证码</span><span (click)="getCaptcha()"><i nz-icon [nzType]="'sync'" [nzSpin]="iconSpin"></i></span>
    </div>

    <ul style="display: flex;justify-content: space-around;margin: 15px 0px;">
        <li *ngFor="let item of CaptchaData.newListArray,let i = index">
            <img (click)="handleValidCodecaptcha(i)" [src]="item" >
        </li>
    </ul>
</div>
```



#### **父组件.ts**

```javascript
import { Component, OnInit, ViewChild } from '@angular/core';
// Antd-Angular
import { AbstractControl, FormBuilder, FormGroup, Validators } from '@angular/forms';
//组件
import { VerificationCodeComponent } from 'src/app/components/verification-code/verification-code.component';

@Component({
  selector: 'app-test',
  templateUrl: './test.component.html',
  styleUrls: ['./test.component.less']
})

export class TestComponent implements OnInit {
    
  handleNotify(value){ 
    console.log(value);  //子调用父组件的方法  并传入值value过来
    
  }
    
  @ViewChild('child')   //需要在html中打标记  #child
  verificationS:VerificationCodeComponent      //一、拿子组件的方法过来，父组件中调用
    
  handleChildMethod(){                        
    this.verificationS.getCaptcha()			   //二、直接调用子组件的方法
  }

}
```



#### **父组件.html**

```html
<div>
  <h1 (click)="handleChildMethod()">发起请求，发送number</h1>
  <app-verification-code #child [PhoneNumber]="'13059224802'" (notify)="handleNotify($event)"></app-verification-code>
  <h2>挡住</h2>
</div>
```



<!-- tabs:end -->