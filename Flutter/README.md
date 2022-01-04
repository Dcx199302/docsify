# Flutter

### 一、文件描述

- Flutter入口文件 lib/main.dart

```javascript
//fultter开发的基础包
import 'package:flutter/material.dart';

<!-- main 入口函数 -->
void main(){
    runApp(
    	Center(
        	child:Text('hello world',textDirection:TextDirection.ltr)
        ),// Center
    )
}
```

- pubspec.yaml ：依赖配置文件，类似node_module依赖配置
