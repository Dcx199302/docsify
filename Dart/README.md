# Dart

- 官网下载安装Dart(自行百度) 目前2.x

- 所有Dart项目都有：入口函数 

  - ```javascript
    main(){}
    ```



## 常量与变量

<!-- tabs:start -->

### **var**

```javascript
var a;
a = 10;

var b = 20;
print(a,b)
```



### **final**

```javascript
final c = 30;   //只能赋值一次,跟const 有区别的 
```



### **const**

```javascript
const d = 20;   //不能被修改
```



### dynamic : 动态的（或泛型）

```javascript
dynamic v = 20;
v = "javascirpt";

var list = new List<dynamic>();
list.add(1);
list.add('hello');
list.add(true)
```

<!-- tabs:end -->



## 数值型

<!-- tabs:start -->

### **Number**

``` javascript
void main() {
// int : 整型
int b = 20     //true
    b = 20.5   //false
    
// double : 浮点型
double c = 20.5   //true
       c = 20     //false
    
// num : 可以是整型、浮点型  
num a = 10;      //整型  true
    a = 12.5;    //浮点  true

abstract class int extends num { }   // 原理中：int 和 double 继承与 num  （abstract：抽象的）

//运算符： +  -  *  /   ~/   %   //加减乘除 取整、取余

//常用属性
isNaN   //是否为数字
isEven  //是否为偶数
isOdd   //是否为奇数
    
//常用方法
    abs()     //绝对值
    round()   //四舍五入
    floor()   //
    ....
}
```





### **String**

```javascript
void main(){
   	String str1 = 'hello';
    String str1 = "hello";
    String str1 = '''hello
    				world''';   //三个引号、换行字符串
    
    string str2 = 'hello  \n  world'   //  /n :  换行符
}
```



### **Boolean**

```javascript
bool isTrue = true;
```



### **List**

- 数组

```javascript
var list= [1,2,3];             //创建List
var list = const [1,2,3];	   //创建不可变的List、 列表的值不可改变
var list = new List();         //构造创建 
```



### **Map**

- 键值对

```javascript
//创建map
var obj = {'first':'dart','second':'java',1:true}; 

//创建不可变的map
var obj = const {'first':'dart','second':'java'};

//构造创建
var obj = new Map();
```



<!-- tabs:end -->



## 运算符

<!-- tabs:start -->

### **算术运算符**

```javascript
int a = 10;
int b = 2;

    print(a + b);
    print(a - b);
    print(a * b);
    print(a / b);
    print(a ~/ b);
    print(a % b);
        
    print(a++);
    print(++a);
    print(a--);
    print(--a);
```

### **关系运算符**

```javascript
int a = 5;
int b = 3;

	print(a == b);
	pirnt(a != b);
	print(a > b);
	print(a < b);
	print(a >= b);
	print(a <= b);
```

### **逻辑运算符**

```javascript
bool isTrue = true;
bool isFalse = false;
	print(!isTrue);
	print(isTrue && isFalse);   //且  false
	print(isTrue || isFalse);   //或  true
```

### **赋值运算符**

```javascript
//基础
int a = 10;   //赋值
int b = 2;
	a += b;
	a -= 2;
	a *= b;
	a /= b;     //double浮点类型  上面的数字影响会报错
	a ~/= b;
	a %= b;

int c;
	c ??= 10;  //10  c没有值的时候赋值
---------------------------------------
int c = 5;
	c ??= 10;   //5  c本身有值不赋值

//其他：位运算
```

### **三目运算符**

```javascript
condition ? expr1 : expr2;  三元运算符
```

### **??**

```javascript
expr1 ?? expr2    //expr1 为空时，使用第二个表达式expr2
```



<!-- tabs:end -->



## 流程控制

<!-- tabs:start -->

### **if-else**

```javascript
void main(){
    int score = 90;
    if(score > 90){
        print("游戏")
    }else if(score > 60){
        print("良好")
    }else{
        print("不及格")
    };
}
```



### **for**

```javascript
void main(){
    var list = [1,2,3,4];
    for(var i = 0;i < list.length; i++){
        print(++list[i])
    }
}
```



### **while**

```javascript
void main(){ 
    int count =0;
    
//while
    while(count < 5){
        print(count++);
    }
   
//do--while
    do{
        print(count--)
    }while(count > 0 && count < 5){
        
    }
    
   
}
```



### **break/continue**

- 终止循环break
- 跳出当前循环continue

```javascript
void main(){
    var list =[1,2,3,4];
    
//break
    for(var item in list){
        if(item == 2){
            break;
        }
        print(item);    // 1 
    };
//-----------------------------------------------
//continue
    for(var item in list){
        if(item == 2){
            continue;
        }
        print(item);  // 1 3 4
    };
    
}
```



### **switch...case**

- 比较类型：num、String、编译期常量、对象、枚举
- 非空case必须有一个break
- default 处理默认情况
- continue 跳转标签

```javascript
void main(){
  var a = 'a';
  switch (a) {
          
    case "ab":
      print('object');
      break;
          
    D:
    case "abc":
      print('object');
      break;
          
    case "abcd":
      print("跳转到其他标签");
      continue D;

    default:
      print("??????");
      break;
          
  }
}
```

<!-- tabs:end -->



## Function

<!-- tabs:start -->

### **function**

- 方法也是对象，并且有具体类型Function
- 返回值类型、参数类型都可以省略
- 箭头语法 ( ) => { };
- 返回值: 没有返回默认为null

```javascript
void main(List args){
    print(args);
    //return 返回值;
}

返回类型 方法名 (参数1,参数2){
    方法体...
    return 返回值
};
```

<!-- tabs:end -->

