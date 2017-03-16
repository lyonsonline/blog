---
layout: post
title: "associatedtype"
date: 2016-11-21
excerpt: "记录它们的适用范围"
tags: [IOS, 内存, weak, unowned]
comments: true
---
swift中的协议采用的是"Associated Types"的方式来实现泛型功能的，通过`associatedtype`关键字来声明一个类型的占位符作为协议定义的一部分，swift的协议不支持下面的定义方式:

```swift
protocol GeneratorType {
    public mutating func next() -> Element?
}
```



而是应该使用这样的定义方式:

```swift
protocol GeneratorType {
    associatedtype Element
    public mutating func next() -> Self.Element?
}
```



在Swift中，class,struct,enums都可以使用参数化类型来表达泛型的，只有在协议中需要使用associatedtype关键字来表达参数化类型。
