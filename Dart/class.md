# 面对对象

- 对象继承于Object类
- new可以省略

## 类与对象1

<!-- tabs:start -->

### **类与对象**

- 属性默认会生成`getter`和`setter`方法
- 使用`final`声明的属性只有`getter`
- 属性和方法通过`.`访问
- 方法不能被重载
- dart 2.x 后声明属性需要加上`late`关键字。用于静态检查
  1. 显式声明一个非空的变量、不初始化
  2. 延迟初始化变量

```javascript
class Person{
    String name;
    int age;
    final String address;  //只读的，不能修改
    
    viod work(){
        print("name is $name, Age is $age ,he is working....")
    };
    void work(int a){};  //报错、已经定义过了work方法、方法不能被重载
}

void main(){
    var person = new Person()；
    person.name = "Tom";   //设置值
    person.age = 20;	   //设置值
    print(person.age);     //获取值
    person.work(); 		   //调用方法
    
    person.address = "china"  //error 错误、设置final属性的不能修改
}
```



### **类及成员可见性**

- Dart中可见性以`library(库)`为单位的
- 默认情况下、每个dart文件就是一个库
- 使用`_ `  `下划线`表示库的私有性，私有的无法`import`使用
- 属性、方法、类、对象均可以`私有`
- 使用`import`导入库

```javascript
//person.dart
class Person {
  late String name;
  late int age;
  late final String address; //只读的，不能修改
  work() {
    print("name is $name, Age is $age ,he is working....");
  }
}

--------------------------------------------------------library的分离和导入--------
//index.dart
import 'person.dart';

void main() {
  var person = new Person();
  person.name = "Tom"; //设置值
  person.age = 20; //设置值
  print(person.age); //获取值
  person.work(); //调用方法
}

```



### **计算属性**

- dart的类的`属性`默认会生成`getter`和`setter`方法
- 计算属性：手动写`getter`或`setter`
- 计算属性、不存储值

```javascript
/**
  * 矩形的类 Rectangele 
  * 包括宽高、计算面积的方法
  * late : 迟的、延迟初始化变量
  *
  // */
class Rectangele {
  late num width, height;      //----- 属性

  // 这是通过---方法---得到面积
  num area() {
    return width * height;
  }

			---------------------------------
  // 使用---getter---得到面积
  num get area2 {  				  //简写 num get area2 => width * height;
    return width * height; 
  }

  // 使用---setter---计算宽度
  set area2(value) {
    width = value / 20;
  }
}

----------------------------------------------
void main() {
  var rect = new Rectangele();

  rect.height = 20;
  rect.width = 10;

  print(rect.area()); //200  方法
  print(rect.area2); //200   值
}

```



### **构造方法**

- 如果没有自定义构造方法、则会有个默认构造方法
- 构造方法不能被`重载` （重复的意思）
- 如要写多个构造方法需要使用`命名构造方法`

```javascript
//dart文件
class Person {
  late String name;
  late int age;
  late final String gender;

  work() {
    print("working....");
  }

  // Person的构造方法
  Person(String name, int age, String gender) {
    this.name = name;
    this.age = age;
    this.gender = gender;
  }

  //构造方法的语法糖, 简写
  // Person(this.name, this.age, this.gender);
  // Person(this.name, this.age) {
  //   print(name);
  // }
}

void main() {
  // 定义了构造方法、需要根据方法传值
  var person = new Person("Tom", 20, "男");
  person.name = "Tom";
  person.age = 20;
  print(person.gender);
}
```



### **命名构造方法**

- 实现多个`构造方法`的方法

```javascript
class Person {
  late String name;
  late int age;

  //构造方法的语法糖, 简写
  Person(this.name, this.age);

  //重写（重载构造方法会报错）
  // Person(this.name, this.age);  //error

  //使用对象点属性的方法可以写
  Person.withName(String name) {
    this.name = name;
  }
}

void main() {
  // 使用Person构造方法创建
  var person = new Person("Tom", 20);
  person.name = "Tom";

  // 使用Person.withName 构造方法创建
  var person2 = new Person.withName("点属性的");
  print(person2.name);
  // print(person2.age); //字段“age”尚未初始化。
}
```



### **常量构造方法**

- 如果类是不可变状态、可以把对象定义为编译时常量
- 感觉好像没啥意义

```javascript
class Person {
//1.将所有的值都设置成final
  final String name;
  final int age;
//2.构造函数使用const 定义
  const Person(this.name, this.age);
}

void main() {
  const person = const Person("name", 18);
  print(person.age);
}
```



#### **工厂构造方法**

- 类似于设计模式中的`工厂模式`
- 在构造方法前添加关键词`factory`实现一个工厂构造方法
- 在工厂构造方法中可`返回对象`
- 不熟、了解一下工厂模式

```javascript
class Logger {
  final String name;
  static final Map<String, Logger> _cache = <String, Logger>{};  // 这里使用了泛型

/**
 * factory：工厂
 * 使用了工厂构造方法后、需要有返回值。且不能为null
 */
  factory Logger(String name) {
    return _cache.putIfAbsent(name, () => Logger._internal(name));
  }

  Logger._internal(this.name);
}
```



<!-- tabs:end -->



## **类和对象2**

<!-- tabs:start -->

### **初始化列表**

- 没搞懂

```javascript
class Person {
  late String name;
  late int age;

  late final String gender;
  Person(this.name, this.age, this.gender);

  Person.withMap(Map map)
      : gender = map["gender"],
        name = map["name"] {
    age = map["age"];
  }
}

void main() {
  Map map = {"name": "devil", "gender": "男", "age": 18};
  var person1 = Person.withMap(map);
  print(person1.name);
  print(person1.age);
}
```



### **静态成员**

- 使用关键字`static`实现`类级别的`变量和函数。不再属于对象级别
- 静态成员不能访问非静态成员、非静态成员可以访问静态成员
- 类中的常量需要使用 `static const`声明

```javascript
 class Page {
  // 静态属性
  static int currentPage = 1;
  //static const int currentPage = 1;  定义静态常量

// 静态的方法 - 不可以访问静态属性
  static void scrollDown() {
    currentPage = 1;
    print("下滑");
  }

// 非静态的方法 - 可以访问静态属性
  void scrollUp() {
    currentPage++;
    print("上滑");
  }
}

void main() {
  var page = new Page();

//对象无法访问  false
  // page.scrollDown();
  // page.currentPage;

//类可以访问  true
  Page.scrollDown();
  print(Page.currentPage);
}

```



### **对象操作符**

- 挺好用的

```javascript
class Person {
  late String name;
  late int age;

  void work() {
    print("work....");
  }
}

void main() {
  var person;
  person = "";
  person = new Person();

  // 对象判断一：类型转换、可以提示属性
  (person as Person).work();          //类型转换

 --------------------------------------------------
  // 对象判断二   is / is!			 //指定类型
  // if (person is Person) {
  //   person.work();
  // }
 
 --------------------------------------------------   
 //级联操作 .. 两个点
 var person3 = new Person();
    person3..name = "tome"
           ..age = 20
           ..work();
    
 //或者 
    person3..name = "tome"..age = 20..work();
}
```



### **对象call方法**

- 如何类实现了`call()`方法，则该类的对象可以作为方法使用

```javascript
class Person {
  late String name;
  late int age;

// 1. 注册call 方法
  String call(String name, int age) {
    return "Name is $name,Ang is $age";
  }
}

void main() {
  //2. new 对象
  var person = new Person();

  // 2.因为有call, 可以将person对象当成方法调用
  print(person("张三", 18));
}

```

<!-- tabs:end -->



## 面向对象编程2

<!-- tabs:start -->

### **继承**

- 继承，继承中的构造方法
- 使用关键字`extends`继承一个类
- 子类会继承父类可见的属性和方法，不会继承构造方法
- 子类能够复写父类的方法、`getter`和`setter`
- 单继承、多态性

```javascript
//person.dart  父类
class Person {
  late String name;
  late int age;
  late String _birthday = "2020.1.1";

  bool get isAdult => age > 18;

  void run() {
    print("Person run.....");
  }
}
```



```javascript
//mian.dart  子类导入父类并继承使用

import 'person.dart';

class Student extends Person {
  void study() {
    print("Student study ...");
  }

  @override //可写可不写,覆写父类方法（重写）  提示作用
  bool get isAdult => age > 15;

  @override //多个覆写
  void run() {
    // super.run(); //super : 在子类里面  调用 父类的方法
    print("Student");
  }
}

main() {
  var study = new Student();
  study.study();
  study.name = "Tom";
  study.age = 16;

  print(study.isAdult);

  study.run();

  // Person 的 私有属性无法导入
  // study._birthday = '10'; //error
}
```



```javascript
  //多态
	Person study = new Student();   //只能使用父类的方法属性
	Student study = new Student();	//可以使用父类和自己的属性方法
```



### **继承的构造方法**

- 子类的`构造方法默认`会调用`父类`的`无名无参`构造方法
- `有名有参`或`有参`的构造方法需要手动 super调用。 IDE会提示

```javascript
class Person {
  late String name;

  // 默认构造方法 -- 无名无参的
  // Person() {
  //   print("继承会默认调用的方法");
  // }

  Person(this.name); //1.无名有参 - 构造方法
  // Person.withName(this.name); //1.有名有参 - 构造方法
}

class Student extends Person {
  late int age;

  // 2.需要显式的调用父类方法中的 一种
  Student(String name) : super(name); //调用无名称的
  // Student(String name) : super.withName(name);    //调用有名称的
}

main() {
  // var student = new Student("张三"); //  print("调用了方法");
}
```



### **执行顺序**

- `父类的构造方法`会在`子类构造方法体`开始执行前的位置调用
- 如果有`初始化列表`，`初始化列表`会在`父类构造`方法`之前`执行。 看前面的`初始化列表`

```java
.....省略前面Person
    
class Student extends Person {
  late int age;

  final String gender;
  // 2.需要显式的调用父类方法中的 一种
  Student(String name, String ggg)
      : gender = ggg,
        super(name); //调用无名称的
  // Student(String name) : super.withName(name);    //调用有名称的
}

main() {
  var student = new Student("张三", "GGG"); //  print("调用了方法");
}
```



### 抽象类

- 抽象类使用`abstract`表示，不能直接被实例化
- 抽象方法不用`abstract`修饰、无实现
- 抽象类可以没有抽象方法

```javascript
//例子：
abstract class Person {
    void run();   //抽象类的方法都是 - 抽象方法 
}

void main() {
    //抽象类 abstract class Person 不能被实例化
  var person = new Person(); //error 错误
}
```

- 有`抽象方法的类` 一定得 `声明成抽象类`
- 抽象类不能被实例化、但是`可以被继承`

```javascript
//abstract :抽象类
abstract class Person {
  void run();
}

//继承于抽象类
class Student extends Person {
  @override //覆写抽象类的抽象方法成 普通方法
  void run() {
    print("object");
  }
}

void main() {
  var person = new Student();
  person.run();
}
```

### **接口**

- 类和接口是统一的。`类就是接口`

```javascript
//使用抽象类作为接口更合适  abstract : 抽象的
abstract class Person {
  void run() {}
}

//使用implements : 实现
class Student implements Person {
  @override
  void run() {
    print("Student run.....");
  }
}
```

- 没个类都`隐式的定`义了一个包含`所有实例成员`的`接口`
- 如果是`复用已有类`的实现，使用继承`(extends)`
- 如果只是使用已有类的外在行为，使用接口 `(implements)`

```javascript
class Person {
  late String name;
  int get age => 18;

  void run() {
    print("Person run ...");
  }
}

//使用继承
// class Student extends Person {}

// 使用接口   需要重写 Person 所有的属性和方法   //系统会生成所有  @override
class Student implements Person {
  @override
  late String name;

  @override
  int get age => 15;

  @override
  void run() {}
}

void main() {
  var person = new Student();
}
```



### **Mixins**

- Mixins`类似`于多继承，是在`多类继承`中`重用`一个类代码的方式
- 作为Mixin的类，`不能有显示声明构造方法` 
- 只能继承至`Object` 
- 使用`implements`接口实现的可以使用`Mixins`
- 使用`with`链接一个或多个类

```javascript
class A {
  void a() {
    print("A.a()...");
  }
}

class B {
  void b() {
    print("A.b()...");
  }
}

class C {
  // C(){},  //显式的构造方法，有名，有参都不行
    
  void c() {
    print("A.c()...");
  }
}

class E extends C {}  //已经继承过除了Object的类。不能使用mixins混入

/**
 * 需求：同时拥有A、B、C三个类的方法
 * class D extends A,B,C {}   //false  dart并不支持多继承
 * 使用 Mixins 的 with  ---- 需要先继承一个A才能使用with B、C
 * 如果A、B、C类中有重复的属性或方法: 使用最后Mixins混入的方法、 C>B>A
 */

class D extends A with B, C {}
```

- 简写

  ```javascript
  //一下两种写法是一样的
  //class E = A with B, C;
  //class E extends A with B, C {}
  ```



### **操作符重写**

##### 很骚的东西、用到再学吧

- 覆写操作符需要在类中定义

  ```javascript
  返回类型 operator 操作符(参数1,参数2,...){
                    实现体...
                    return 返回值
  }
  ```

- 如果需要覆写`==`号,还需要覆写对象的`hashCode getter`方法

```javascript
//可以覆写的操作符：
< > <= >= - + / ~/ * % | & << >> [] []= ~ ==  ......
```



<!-- tabs:end -->



### 枚举&泛型

<!-- tabs:start -->

### **枚举**

- 使用关键字`enum`定义一个枚举
- 常用于代替常量，控制语句等
- 枚举特性
  - index 从 0开始，依次累加
  - 不能指定原始值

```javascript
// 季节
enum Season { spring, summer, autumn, winter }

void main() {
  var currentSeason = Season.autumn; //打印 7-9 月

  print(currentSeason.index);  //index从 0开始,不能指定值
    
  switch (currentSeason) {
    case Season.spring:
      print("1-3月");
      break;
    case Season.summer:
      print("4-6月");
      break;
    case Season.autumn:
      print("7-9月");
      break;
    case Season.winter:
      print("10-12月");
      break;
    // default:
  }
}
```



### **泛型**

- Dart中类型是可选的，可使用`泛型限制类型`

```javascript
```





<!-- tabs:end -->