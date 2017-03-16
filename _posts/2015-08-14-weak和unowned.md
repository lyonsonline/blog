---
layout: post
title: "weak 与 unowned"
date: 2015-08-14
excerpt: "记录它们的适用范围"
tags: [IOS, 内存, weak, unowned]
comments: true
---

- weak对应optional，unowned 对应 implicitly unwrapped optional
- weak,unowned定义的变量都是弱引用类型，用于打破循环引用
