# 使用Typescript

## 一、基础类型

<!-- tabs:start -->



#### **基础**

```javascript
// var [变量名] : [类型] = 值;
a:any					任意值
a:number				数值类型(可以是二进制、八进制...等)
a:string				字符
a:boolean				true 和 false
a:null					对象缺失
a:undefined				初始化变量为一个未定义的值
:void					函数无返回值
function hello(): void {
    alert("Hello Runoob");
}
```

#### **数组**

```javascript
// 在元素类型后面加上[]
let arr: number[] = [1, 2];
// 或者使用数组泛型
let arr: Array<number> = [1, 2];
```

#### **元组**

```javascript
//有顺序的数组
let x: [string, number];
x = ['Runoob', 1];    // 运行正常
x = [1, 'Runoob'];    // 报错
```

#### **枚举**

```javascript
enum Color {Red, Green, Blue};
let c: Color = Color.Blue;
console.log(c);    // 输出 2
```

<!-- tabs:end -->



## 二、断言Assertion（不清楚）

- 类型断言： 允许变量从一种类型 更改为 另外一种类型

```javascript
语法格式：
// <类型>值
// 或 
// 值 as 类型

实例:
<number> <any>:
    var str = '1' 
    var str2:number = <number> <any> str   //str、str2 是 string 类型
    console.log(str2)

//React中只能使用as,<number> <any>这种写法会冲突
as: 
    a:string = "1"
    b:number = this.a as unknown as number;
    b:number = this.a as any as number;
```

























## 三、

<!-- tabs:start -->

#### **类**

```typescript

```



#### **类型推断**

```javascript
```



#### **类型擦除**

```javascript
```



#### **接口**

```javascript
```



#### **枚举**

```javascript
```



#### **Mixin**

```javascript
```



#### **泛型编程**

```javascript
```



#### **名字空间**

```javascript
```



#### **元组**

```javascript
```



#### **Await**

```javascript
```



#### **模块**

```javascript
```



#### **lambda匿名函数的箭头语法**

```javascript
```



#### **可选参数以及默认参数**

```javascript
```



#### **类型批注和编译时类型检查**

```javascript
```



<!-- tabs:end -->





