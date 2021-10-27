# router

## 一、获取路由参数

<!-- tabs:start -->

#### **一、get参数获取**

```javascript
import { ActivatedRoute } from '@angular/router';

export class BuyerComponent implements OnInit {
    //1. 引入ActivatedRoute
    constructor(private activatedRoute:ActivatedRoute) { }
	ngOnInit(): void {
    	this.activatedRoute.queryParams.subscribe(query=>{
    		//2. 打印参数
        	console.log(query)
    })
  }
}
```

#### **二、没写**

<!-- tabs:end -->





## 二、Http统一拦截

- /app/interceptor/...
- 给http请求修改url 和添加 headers属性 

<!-- tabs:start -->

#### **http.interceptor.ts**

```javascript
import { Injectable } from '@angular/core';
import {
  HttpEvent, HttpInterceptor, HttpHandler, HttpRequest, HttpResponse
} from '@angular/common/http';

import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators';
import { Router } from '@angular/router';

/** Pass untouched request through to the next request handler. */
@Injectable()
export class MyHttpInterceptor implements HttpInterceptor {
    constructor (private router: Router) {}
  intercept(httpRequest: HttpRequest<any>, next: HttpHandler):
    Observable<HttpEvent<any>> {
    // 拦截请求,给请求头添加token
    let url = httpRequest.url // 可以对url进行处理
    // let token = document.cookie && document.cookie.split("=")[1]
    let token = '12312312312312312312'
    // 登录请求排除在外
    // if (!url.includes('login')) {
        httpRequest = httpRequest.clone({
            url, // 处理后的url,再赋值给req
            headers: httpRequest.headers.set('Authorization', token)//请求头统一添加token
        })
    // }
    return next.handle(httpRequest).pipe(
        tap(
         event => {
          if (event instanceof HttpResponse) {
           console.log(event);
           if (event.status >= 500) {
            // 处理错误
           }
          }
         },
         error => {
          // token过期 服务器错误等处理
        //   this.router.navigate(['/login']);
         })
       );
  }
}
```

#### **app.module.ts**

```clike
 import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
 import { MyHttpInterceptor } from './interceptor/http.interceptor';
 providers: [
    { provide: NZ_I18N, useValue: zh_CN },
    { provide: HTTP_INTERCEPTORS, useClass: MyHttpInterceptor, multi: true }
  ],
```



<!-- tabs:end -->



## 三、路由守卫

- 基本的守卫逻辑

- 路径：src/app/auth/

  

<!-- tabs:start -->

#### **auth.service.ts**

```javascript
import { Injectable } from '@angular/core';
import { Observable, of } from 'rxjs';
import { delay, tap } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class AuthService {

constructor() { }

isLoggedIn = true; //默认未登录

// 记录登录之后,需要跳转到原来请求的地址

  redirectUrl!: string;
// 登录
  login(): Observable<boolean> {
    return of(true).pipe(
      delay(1000),
      tap(val => this.isLoggedIn = true)
    );
  }
// 登出
  logout(): void {
    this.isLoggedIn = false;
  }
}
```



#### **auth.guard.ts**

```javascript
import { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from '@angular/router';

import { AuthService } from './auth.service'; 
@Injectable({
  providedIn: 'root',
})
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService, private router: Router) {}
  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): boolean {
    let url: string = state.url
    return this.checkLogin(url);
  }
  
  checkLogin(url: string): boolean {
    if (this.authService.isLoggedIn) { return true; }

    // 保存原始的请求地址,登录后跳转到该地址
    this.authService.redirectUrl = url;

    // 未登录,跳转到登录页面
    this.router.navigate(['/']);
    return false;
  }
}
```

<!-- tabs:end -->













demo===============

<!-- tabs:start -->

<!-- tabs:end -->
