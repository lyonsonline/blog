---
layout: post
title: "Swift3进阶学习(1)"
date: 2017-02-03
excerpt: "对advanced swift学习记录"
tags: [IOS, Swift, 进阶]
comments: true
---
1. 序列是可以无限的,集合不可以

2. 满足 sequence的协议

   `func makeIterator()->IteratorProtocal`

3. 满足IteratorProtocal协议

   `mutating func next()->Element?`

4. Sequence不保证被多次遍历,所以`first`属性只有在**集合类型**上出现,**序列**却没有

5. 在 Swift 3.0 中，编译器缺乏两个必要的特性:现在没有循环协议约束 (Sequence 会对自身进
   行引用)，也没有关联类型中的 where 语句支持

   ```swift
   // Swift 3.0 中无法编译
   associatedtype SubSequence: Sequence
   where Iterator.Element == SubSequence.Iterator.Element, SubSequence.SubSequence == SubSequence
   ```

6. 集合协议是建立在Sequence协议之上的.集合类型指的是那些稳定的序列,被多次遍历保持一致.

7. 遵守 ExpressibleByArrayLiteral 协议

   ```swift
   extension FIFOQueue: ExpressibleByArrayLiteral {
   	public init (arrayLiteral elements: Element...) {
   		self.init(left: elements.reversed(),right: []) }
   }			
   ```

8. 集合类型中的默认`Iterator`迭代器类型是 `IndexingIterator<Self>`
