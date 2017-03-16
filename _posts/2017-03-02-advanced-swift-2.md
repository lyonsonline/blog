---
typora-copy-images-to: ./advance-swift学习笔记(2)/images
---

- 字典的索引值不是Key,是`DictionaryIndex`类型

  > `DictionaryIndex`是一个指向字典内部缓存区的不透明的值

- 字典索引下标访问返回值不是字典键值返回的可选值.返回的是一个确定值

  ```swift
  struct Dictionary {
     ...
     subscript(key: Key) -> Value? //返回可选值
  }
  protocol Collection {
     subscript(position: Index) -> Element {get}//返回确定值
  }
  ```

  ​ `Element`返回的是一个元组:`(key: Key, value: Value)`,而下标键值索引返回的是`Value?`是可选值

- 索引值是一个只存存描述元素位置所需最小信息的简单值.尽可能不持有对集合的引用.集合通常不能分辨索引的归属(是否是其他同种类型集合的索引)比如数组:

  ```swift
  let numbers = [1,2,3,4]
  let squares = numbers.map { $0 * $0 }
  let numbersIndex = numbers.index(of: 4)! // 3 squares[numbersIndex] // 16
  ```

  类似String.Index

  ```swift
  let hello = "Hello"
  let world = "World"
  let helloIdx = hello.startIndex
  world[helloIdx] // W
  ```

  > 在切片上会大量应用这个技术

- swift2与swift3中对索引遍历有所改变,

  - swift2中索引可以自己进行步进移动`someIndex.successor()`
  - swift3中交给集合来完成`collection.index(after: someIndex)`

  > 在原来自己管理的索引模型中,索引值必须持有对集合的引用,在集合被迭代修改时造成不必要的复制,浪费性能.

- 满足`Comparable`

  1. 实现`<`
  2. 实现`==`(继承自`Equatable`)

- 切片

  > 切片和原集合共享缓存区,直到集合和切片都销毁时,内存才会被释放.
  >
  > Apple警告⚠️:切片只能当做临时计算
  >
  > ![20170306list释放(/Users/lyonseric/Library/Mobile Documents/com~apple~CloudDocs/Note/advance-swift学习笔记(2)/images/20170306list释放(1).png)](/Users/lyonseric/Library/Mobile Documents/com~apple~CloudDocs/Note/20170306list释放(1).png)在list中因为ARC的存在,当没有引用时,节点自动释放,注意的是list后面的节点不会释放
  >
  > ![20170306list释放(/Users/lyonseric/Library/Mobile Documents/com~apple~CloudDocs/Note/advance-swift学习笔记(2)/images/20170306list释放(2).png)](/Users/lyonseric/Library/Mobile Documents/com~apple~CloudDocs/Note/20170306list释放(2).png)

- 在`Collection`协议上的拓展协议

  - `BidirectionalCollection` 支持前向,后向遍历的集合
  - `RandomAccessCollection` 支持高效随机存取索引遍历的集合
  - `MutableCollection` 支持下标赋值的集合
  - `RangeReplaceableCollection` 支持将任意子范围的元素用别的集合元素替换的集合

  ​
