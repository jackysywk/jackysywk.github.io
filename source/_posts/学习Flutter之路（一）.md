---
title: 学习Flutter之路（一）
date: 2025-04-10 11:58:06
tags:
- Flutter
category: Flutter
---

## 

不知道你有没有开发前端或者手机APP的经验，我感觉很多人想学习Flutter 也是被他的流行度和双OS通用所吸引，相信一开始很多人被很多新的词汇被搞懵，譬如MaterialApp, Scaffolding, Stateless, Stateful Widget

（先不说被环境配置搞懵，自行百度/ 谷歌 / ChatGPT / DeepSeek就能解决）

## 配置环境后，需要关注什么

首先，我从学习Python, C#, Java, 甚至HTML 来做的对比
在程序执行， 总有一堆代码我们在刚学习时， 有些代码可以忽略不管
### Python

```
def main():
    print("Hello, this is the main function!")
    
if __name__ == "__main__":
    main()
```
### Java
```
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, this is the main method!");
    }
}
```
### HTML
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>HTML 5 Boilerplate</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <script src="index.js"></script>
  </body>
</html>
```

我自己刚学习编程 / 学习一们新的语言，都会把这些不影响学习先忽略，敲简单代码时可以忽略不看。

反正我从来没了解过meta name="viewport" 是什么意思，道理一样。

所以相对应的Flutter 代码是一下这句**可以理解成 boilerplate**的代码

```
import 'package:flutter/material.dart'
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold( //<----- 你要关注的东西
        appBar: AppBar(title: Text('My Flutter App')),
        body: Center(
          child: Text('Hello World'),
        ),
      ),
    );
  }
}
```

你所需要关注的是 Scaffold 类的使用方法
[https://api.flutter.dev/flutter/material/Scaffold-class.html](https://api.flutter.dev/flutter/material/Scaffold-class.html)

![Scaffold作用](/images/scaffolding.jpg)
图片来源： [https://livebook.manning.com/concept/flutter/scaffold](https://livebook.manning.com/concept/flutter/scaffold)

## 需要关注的Scaffold 参数
Scaffold类中有很多参数，因为我是妥妥的20/80 信奉者，我只关注AppBar, drawer, endDrawer 等等图中的东西。其他的参数，需要用的时候再查。

### 下期预告
介绍Stateless 和 Stateful Widget 然后创造一个简单的APP。