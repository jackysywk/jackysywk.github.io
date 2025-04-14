---
title: 学习Flutter之路（二）- Widgets
date: 2025-04-14 15:55:27
tags:
- Flutter
category: Flutter
---

## 前言

上次说道新建项目后，你只需要先关注 main 函数 下面的 Material App 和 Scaffold 函数，按照Scaffold class 的 文档, 你可以设置AppBar属性和 bottomNavigationBar的属性, 大部分APP都用到这两个组件，我就利用以上的属性和Widget 构建了一个 简单小作业。

![Preview](images/学习Flutter之路（二）-Widgets/AppPreview.png)

## 小工具推荐

敲代码之前想向大家介绍一个小工具 [Flutlab](https://flutlab.io/)， 这个网页可以在不配置flutter环境下，提供一个编程环境，我自己使用免费版就在任何地方学习Flutter 代码

![Flutlab](images/学习Flutter之路（二）-Widgets/flutlab.png)

## Widgets
Stateful Widgets 和 Stateless Widgets 是Flutter 中两个基本的Widget 类型，他们主要的区别在于是否需要管理状态。在了解之前，先说什么是Stateless Widgets。

### Stateless Widget
顾名思义，Stateless Widget是无状态，你可以先定义variable 让Widgets 显示，但是这个variable 就在APP运行时无法改变（无法靠Widget自身改变，但可以依靠父组件改变，先不展开）。

```
import 'package:flutter/material.dart';

class HomePage extends StatelessWidget {
  final String text;

  const HomePage({Key? key, required this.text}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Center(
        child: Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text(text),
      ],
    ));
  }
}
```

我的Widget 的构造函数有个Text 的变量，都是在Widget 被调用时创建的，在我的APP中 这个变量是HOME
![Stateless Widget](images/学习Flutter之路（二）-Widgets/home.png)

然后可以加上一个显示图片
```
import 'package:flutter/material.dart';

class HomePage extends StatelessWidget {
  final String text;

  const HomePage({Key? key, required this.text}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Center(
        child: Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Image.asset(
          "assets/test.jpeg",
          width: 650, // 指定寬度
          height: 400, // 指定高度
          fit: BoxFit.contain,
        ), // 控制圖片如何填充指定的空間),
        Text(text),
      ],
    ));
  }
}
```
就变成上面Preview 的样子

### Stateful Widgets
我的理解是，Stateful Widgets 有一些方法让开发者调用，目的去改变Stateful Widgets 的状态，例如setState()方法

我这个简单小作业APP的Stateful Widget就是 下面的导航栏
```
// 先定义组件类
class MainScaffold extends StatefulWidget {
  @override
  _MainScaffoldState createState() => _MainScaffoldState();
}

// 再定义组件的状态

class _MainScaffoldState extends State<MainScaffold> {
  int _selectedIndex = 0;

  // 不同頁面的列表
  final List<Widget> _pages = [
    HomePage(text: 'HOME'), // 其他组件， 可以是Stateful 可以是Stateless
    ProfilePage(text: "Profile") 
  ];

  // 定义方法去改变组件的状态
  void _onItemTapped(int index) {
    setState(() {
      _selectedIndex = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('My App'),
      ),
      body: _pages[_selectedIndex], // 顯示當前選中的頁面***

      bottomNavigationBar: BottomNavigationBar(
        items: const <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            icon: Icon(Icons.home),
            label: 'Home',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.person),
            label: 'Profile',
          ),
        ],
        currentIndex: _selectedIndex,
        onTap: _onItemTapped,
      ),
    );
  }
}
```
导航栏会根据用户按钮输入，去改变_selectIndex 变量，从而改变body，变换_pages 列表返回的 其他页面class
这样就能轻松实现 导航栏 和页面切换功能。


![Profile Page](images/学习Flutter之路（二）-Widgets/navbar.png)

### 小结
| | Stateless Widget | Stateful Widget |
|---|---|---|
| 狀態管理 | 無內部狀態 | 通過State 對象管理 |
| 重建機制 | 只有外部傳入參數變化才重建 | setState被調用 或父組件重建時重建 |
| 性能 | 較高 | 較低 |
| 生命週期 | 只有build的方法 | 有多個生命週期方法，initState, createState... |
| 代碼結構 | Single Class | Double Class |

### 预告

虽然目前你可以表面上理解成 Stateful / Stateless 就是有状态和无状态的组件类，但是在实际开发上，Stateless Widget 经常包含着多个 Stateful Widget， 做到不同状态变脸encapsulation 的效果，这个不难理解。

但是，Flutter中也有一个常见的设计模式，叫做「状态提升」或者「容器-内容模式」，即使利用Stateful Widget 包含着一个Stateless Widget，Stateful Widget 的代码只专注管理状态，把状态变量传入Stateless Widget， Stateless Widget的代码只专注UI渲染的部分，透过这个模式，Stateless Widget 也可以改变。

到实际操作，就会遇到这种大量互相嵌套的代码，下期就讲讲这种设计模式。