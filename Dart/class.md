# 面对对象

- 对象继承于Object类
- new可以省略

# 类与对象1

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









<!-- tabs:end -->

----

<!-- tabs:start -->





<!-- tabs:end -->