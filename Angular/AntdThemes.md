# ng-zorro-antd

#### 一、安装制定版本的ui

<!-- panels:start -->

<!-- div:title-panel -->
一、安装需要的zorro-antd 版本

```javascript
ng add ng-zorro-antd@10.2.2
```



<!-- div:left-panel -->

安装选项：

![img](https://img.alicdn.com/tfs/TB19fFHdkxz61VjSZFtXXaDSVXa-680-243.svg)

<!-- div:right-panel -->

添加图标资源:(y/N)

设置自定义主题文件:(y/N)

选择您的地区代码:(en Us, ca ES, de de, zh CN…)

选择模板来创建项目:(使用方向键)空白侧梅努
<!-- panels:end -->



#### 二、使用暗黑风格  app / style.less

```less
// @import "../node_modules/ng-zorro-antd/ng-zorro-antd.less";
@import "~ng-zorro-antd/ng-zorro-antd.dark.less";
@theme: 'dark';

// The prefix to use on all css classes from ant.
@ant-prefix: ant;

// An override for the html selector for theme prefixes
@html-selector: html;

//其他全部注释掉
```



#### 三、使用什么组件就去app.module.ts 中按需引入

```javascript

import { ThemesTestComponent } from './themes-test/themes-test.component';
import { NzCollapseModule } from 'ng-zorro-antd/collapse';
import { NzCheckboxModule } from 'ng-zorro-antd/checkbox';
import { NzButtonModule } from 'ng-zorro-antd/button';

registerLocaleData(zh);

@NgModule({
  imports: [
    NzCollapseModule,
    NzCheckboxModule,
    NzButtonModule
  ],
})
export class AppModule { }

```

