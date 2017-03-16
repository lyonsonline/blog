---
layout: post
title: "Swift3进阶学习(3)"
date: 2017-03-03
excerpt: "对advanced swift学习记录"
tags: [IOS, Swift, 进阶]
comments: true
---
## 向前索引

> 因为单链表只支持向前索引,所以 列表属性有 first, 而没有 last.想得到 last 属性是一个O(n)的操作
>
> 对于属性来说要满足O(1)复杂度,也有例外比如`count`属性,在文档中`count`属性时间复杂度为 O(n),不过大多数集合都为`count`提供了 O(1)的实现.

## 双向索引

> **实现`index(before:)`**

`BidirectionalCollection`在前向索引增加了一个方法:获取上一个索引值得`index(before:)`.有这个方法就可以提供默认的`last`实现

```swift
extension BidirectionalCollection {
	/// 集合中的最后一个元素。
	public var last: Iterator.Element? {
		return isEmpty ? nil : self[index(before: endIndex)]
	}
}
```

String.CharacterView 是一个双向索引集合的例子.因为 Unicode 的原因(啥原因?)一个字符集合不能含有随机存取的索引.

## 随机存取索引

> **实现`index(_:offsetBy:)`和`distance(from:to:)`或者使用满足 Strideable的 index 类型(比如 Int)**



## MutableCollection

> 可变集合支持原地的元素修改,相比 Collection,mutableCollection 增加了一个`subscript`方法,必须提供 setter 方法
