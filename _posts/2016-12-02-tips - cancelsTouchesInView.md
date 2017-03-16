---
layout: post
title: "cancelsTouchesInView"
date: 2016-12-02
excerpt: "手势识别的属性,用来设置势被识别时触摸事件是否被传送到视图"
tags: [ IOS, Tips, Cocoa]
comments: true
---

>  A Boolean value affecting whether touches are delivered to a view when a gesture is recognized.When this property is true (the default) and the receiver recognizes its gesture, the touches of that gesture that are pending are not delivered to the view and previously delivered touches are cancelled through a touchesCancelled(_:with:) message sent to the view. If a gesture recognizer doesn’t recognize its gesture or if the value of this property is false, the view receives all touches in the multi-touch sequence.

*也就是说，可以通过设置这个布尔值，来设置手势被识别时触摸事件是否被传送到视图,*

  **当值为YES的时候，系统会识别手势，并取消触摸事件；为NO的时候，手势识别之后，系统将触发触摸事件.**

`cancelsTouchesInView`是`UITapGestureRecognizer`的属性

```objc
- (void)viewDidLoad {
    UIButton *button = [[UIButton alloc] initWithFrame:CGRectMake(0, 0, 100, 50)];
    button.backgroundColor = [UIColor colorWithRed:0.1 green:0.5 blue:0.4 alpha:1];
    [supView addSubview:button];
    [button addTarget:self action:@selector(btnAction:) forControlEvents:UIControlEventTouchUpInside];
    UITapGestureRecognizer *tap = [[UITapGestureRecognizer alloc]initWithTarget:self action:@selector(tapAction:)];
    tap.cancelsTouchesInView = NO;
    [button addGestureRecognizer:tap];
}

- (void)tapAction:(UITapGestureRecognizer *)sender {
    NSLog(@"tap");        
}

- (void)btnAction:(UIButton *)btn {
    NSLog(@"button");    
}
```

当*cancelsTouchesInView*为**NO**的时候，会分别触发*“tapAction:”*和*“btnAction:”*方法；而当*cancelsTouchesInView*为**YES**的时候，只会触发*“tapAction:”*方法。
