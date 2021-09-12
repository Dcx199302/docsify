# Angular重难点

## 一、架构概览

<!-- tabs:start -->

#### **Angular概述**

1. 用 Angular 扩展语法编写 HTML 模板， 

2. 用组件类(class)管理这些模板，

3. 用服务添加应用逻辑， 

4. 用模块打包发布组件与服务。

5. 然后，我们通过引导根模块来启动该应用。 

6. Angular 在浏览器中接管、展现应用的内容，并根据我们提供的操作指令响应用户的交互。

   

#### **Angular应用中的8个主要构造块：**

1. 模块 (module)

2. 组件 (component)

3. 模板 (template)

4. 元数据 (metadata)

5. 数据绑定 (data binding)

6. 指令 (directive)

7. 服务 (service)

8. 依赖注入 (dependency injection)

   

<!-- tabs:end -->



------



## 二、Angular 理论知识

<!-- tabs:start -->

##### **模块**

1.    Angular 应用是模块化的，并且 Angular 有自己的模块系统，它被称为 Angular 模块或 NgModules。
2.    每个 Angular 应用至少有一个模块（根模块），习惯上命名为AppModule。
3.    Angular 模块（无论是根模块还是特性模块）都是一个带有@NgModule装饰器的类。
4.    装饰器是用来修饰 JavaScript 类的函数。 Angular 有很多装饰器，它们负责把元数据附加到类上，以了解那些类的设计意图以及它们应如何工作。
5.    NgModule是一个装饰器函数，它接收一个用来描述模块属性的元数据对象。其中最重要的属性是：
6.    declarations —— 声明本模块中拥有的视图类。 Angular 有三种视图类：组件、指令和管道。
7.    exports —— declarations 的子集，可用于其它模块的组件模板。
8.    imports —— 本模块声明的组件模板需要的类所在的其它模块。
9.    providers —— 服务的创建者，并加入到全局服务列表中，可用于应用任何部分。
10.    bootstrap —— 指定应用的主视图（称为根组件），它是所有其它视图的宿主。只有根模块才能设置bootstrap属性。
11.    Angular 提供了一组 JavaScript 模块。可以把它们看做库模块。
12.    每个 Angular 库的名字都带有@angular前缀。
13.    用 npm 包管理工具安装它们，用 JavaScript 的import语句导入其中某些部件。



##### **组件**

1. 组件负责控制屏幕上的一小块区域，我们称之为视图。
2. 我们在类中定义组件的应用逻辑，为视图提供支持。 组件通过一些由属性和方法组成的 API 与视图交互。



##### **模板**

1. 我们通过组件的自带的模板来定义组件视图。模板以 HTML 形式存在，告诉 Angular 如何渲染组件。



##### **元数据（Metadata）**

1. 元数据告诉 Angular 如何处理一个类。
2. 在TypeScript 中，我们用装饰器 (decorator) 来附加元数据。
3. @Component里面的元数据会告诉 Angular 从哪里获取你为组件指定的主要的构建块。
4. 模板、元数据和组件共同描绘出这个视图。
5. 其它元数据装饰器用类似的方式来指导 Angular 的行为。 例如@Injectzable、@Input和@Output等是一些最常用的装饰器。



##### **数据绑定**

1. 数据绑定的语法有四种形式。每种形式都有一个方向——绑定到DOM、绑定自DOM以及双向绑定。
2. 数据绑定的四种形式：插值表达式、属性绑定、事件绑定、双向数据绑定。
3. 双向数据绑定使用ngModel指令组合了属性绑定和事件绑定的功能。
4. 在双向绑定中，数据属性值通过属性绑定从组件流到输入框。用户的修改通过事件绑定流回组件，把属性值设置为最新的值。



##### **指令（directive）**

1. Angular 模板是动态的。当 Angular 渲染它们时，它会根据指令提供的操作对 DOM 进行转换。
2. 指令是一个带有“指令元数据”的类。在 TypeScript 中，要通过@Directive装饰器把元数据附加到类上。
3. 组件是一个带模板的指令；@Component装饰器实际上就是一个@Directive装饰器，只是扩展了一些面向模板的特性。
4. 除了组件这种类型的指令外，还有两种其他类型的指令：结构型指令和属性型指令。
5. 结构型指令和属性型指令往往像属性 (attribute) 一样出现在元素标签中， 偶尔会以名字的形式出现，但多数时候还是作为赋值目标或绑定目标出现。
6. 结构型指令通过在 DOM 中添加、移除和替换元素来修改布局。如内置指令：*ngFor、*ngIf。
7. 属性型指令修改一个现有元素的外观或行为。在模板中，它们看起来就像是标准的 HTML 属性，故名。如：ngModel。



##### **服务**

1. 服务是一个广义范畴，包括：值、函数，或应用所需的特性。
2. 典型的服务是一个类，具有专注的、明确的用途。它应该做一件特定的事情，并把它做好。
3. 服务没有什么特别属于 Angular 的特性。 Angular 对于服务也没有什么定义。 它甚至都没有定义服务的基类，也没有地方注册一个服务。
4. 即便如此，服务仍然是任何 Angular 应用的基础。组件就是最大的服务消费者。
5. 组件类应保持精简。组件本身不从服务器获得数据、不进行验证输入，也不直接往控制台写日志。 它们把这些任务委托给服务。
6. 组件的任务就是提供用户体验，仅此而已。它介于视图（由模板渲染）和应用逻辑（通常包括模型的某些概念）之间。 设计良好的组件为数据绑定提供属性和方法，把其 它琐事都委托给服务。



##### **依赖注入**

1. “依赖注入”是提供类的新实例的一种方式，还负责处理好类所需的全部依赖。大多数依赖都是服务。 Angular 使用依赖注入来提供新组件以及组件所需的服务。
2. Angular 通过查看构造函数的参数类型得知组件需要哪些服务。
3. 当 Angular 创建组件时，会首先为组件所需的服务请求一个注入器 (injector)。
4. 注入器维护了一个服务实例的容器，存放着以前创建的实例。 如果所请求的服务实例不在容器中，注入器就会创建一个服务实例，并且添加到容器中，然后把这个服务返回1. 给 Angular。 当所有请求的服务都被解析完并返回时，Angular 会以这些服务为参数去调用组件的构造函数。 这就是依赖注入。
5. 提供商用于创建并返回一个服务，通常是服务类本身。
6. 我们可以在模块或组件中注册提供商。通常会把提供商添加到根模块上，以便在任何地方使用服务的同一个实例。或者，也可以在@Component元数据中的providers属性中把它注册在组件层。把它注册在组件级表示该组件的每一个新实例都会有一个服务的新实例。
7. 依赖注入的要点：
   - 依赖注入渗透在整个 Angular 框架中，被到处使用。
   - 注入器 (injector) 是本机制的核心。
   - 注入器负责维护一个容器，用于存放它创建过的服务实例。
   - 注入器能使用提供商创建一个新的服务实例。
   - 提供商是一个用于创建服务的配方。
   - 把提供商注册到注入器。
   
   

##### **其他重要的Angular特性和服务**

1. 动画：用 Angular 的动画库让组件动起来，而不需要对动画技术或 CSS 有深入的了解。
2. 变更检测：变更检测文档会告诉你 Angular 是如何决定组件的属性值变化，什么时候该更新到屏幕， 以及它是如何利用区域 (zone) 来拦截异步活动并执行变更检测策略。
3. 事件：事件文档会告诉你如何使用组件和服务触发支持发布和订阅的事件。
4. 表单：通过基于 HTML 的验证和脏检查机制支持复杂的数据输入场景。
5. HTTP：通过 HTTP 客户端，可以与服务器通讯，以获得数据、保存数据和触发服务端动作。
6. 生命周期钩子：通过实现生命周期钩子接口，可以切入组件生命中的几个关键点：从创建到销毁。
7. 管道：在模板中使用管道转换成用于显示的值，以增强用户体验。
8. 路由器：在应用程序客户端的页面间导航，并且不离开浏览器。
9. 测试：使用 Angular 测试平台，在你的应用部件与 Angular 框架交互时进行单元测试。



##### **AppModule: 根模块**

1. Angular模块类描述应用的部件是如何组合在一起的。
2. 每个应用都至少有一个Angular模块，也就是根模块，用来引导并运行应用。常规名字是AppModule。
3. @NgModule装饰器将AppModule标记为 Angular 模块类（也叫NgModule类）。 @NgModule接受一个元数据对象，告诉 Angular 如何编译和启动应用。

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';
@NgModule({
  imports:      [ BrowserModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```



##### **imports 数组**

1. 每个浏览器中运行的应用都需要@angular/platform-browser里的BrowserModule。 所以每个这样的应用都在其根AppModule的imports数组中包含BrowserModule。
2. imports数组中应该只有NgModule类。不要放置其它类型的类。
3. JavaScript 的import声明允许你访问在其他文件中导出的符号，这样你可以在当前文件引用它们。
4. 模块的imports数组告诉 Angular 特定 Angular 模块的信息 — 用@NgModule装饰的类 — 应用需要它们来正常工作。



##### **declarations 数组**

1. 每个组件必须在且仅在一个NgModule类中声明。
2. 通过将其列到AppModule模块的declarations数组中，告诉 Angular 哪个组件属于AppModule。 在创建更多组件的过程中，逐步将它们添加到declarations中。
3. 指令和管道也必须被添加到declarations数组中。
4. 只有可以声明的——组件、指令和管道属于declarations数组中。不要将其他类型的类添加到declarations中。例如NgModule类、服务类、模型类。



##### **bootstrap 数组**

1. 通过引导根AppModule来启动应用。 在启动过程中，其中一步是创建列在bootstrap数组的组件， 并将它们每一个都插入到浏览器的DOM中。
2. 每个被引导的组件都是它自己的组件树的根。 插入一个被引导的组件通常触发一系列组件的创建并形成组件树。
3. 虽然你可以将多个组件树插入到宿主页面，但并不普遍。 大多数应用只有一个组件树，它们引导单一根组件。
   你可以为这个根组件取任何名字，但是大多数程序员将其取名为AppComponent。



##### **在main.ts中引导**

```javascript
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule }              from './app.module';

platformBrowserDynamic().bootstrapModule(AppModule);
```



1. 你可以为这个根组件取任何名字，但是大多数程序员将其取名为AppComponent。
2. 模块的bootstrap数组中提出根AppComponent， 创建该组件的实例，并将其插入到组件selector标识的元素标签中。
   

<!-- tabs:end -->
