# Angular （MVC）

- 特殊文件描述
  - e2e——自动化测试文件
  - karma.conf.ts——自动化测试配置文件
  - environments——环境配置（开发环境、生产环境）

<!-- tabs:start -->

#### **模块app.module.ts**

```javascript
import {AppComponent} from './app.component'
import {HelloComponent} from './helle/hello.component'

@NgModule({
    declarations:[    		//declarations 声明；宣告  包含：组件、
        AppComponent,         //程序的主组件
        HelloComponent 		//1.自定义的新组件 -- 引入
    ],
})

export class AppModule { }
```

#### **JS模块app.component.ts**

```javascript
//装饰器
@Component({  
	selector:'app-root',  //选择器
    templateUrl:'./app.component.html',  //组件模板
    styles:["./app.component.scss"],     //数组格式的css样式表
})

export class AppComponent{
    title:'变量数据'
}
```

####  **html模板app.component.html**

```html
<div class="titleColor">
    {{title}}
</div>
<app-hello></app-hello>  <!-- 使用自定义的组件 -->
```

#### **CSS样式**

```css
.titleColor{
    color:red;
}
```



<!-- tabs:end -->


