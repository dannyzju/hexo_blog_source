---
title: RxJava极简入门
date: 2016-08-30 01:02:51
tags: 
- RxJava
- Android
---

RxJava是在Android开发者中非常热门的函数库。刚上手会感觉比较难理解，但一旦理解了它，你会感觉开启了一扇全新的大门。网上关于RxJava的文章很多，这里也只是略窥门径，对其有个最最基本的概念。

### 1. RxJava是什么?
先来看看别的开发者怎么说的：
>“RxJava is a library of code used to handle data using a push and pull mechanism. Just like a notification on your phone, some data will be pushed to a receiver of that data. It’s a different way to think about existing coding patterns you know.” 

RxJava官网上的定义:
>A library for composing asynchronous and event-based programs using observable sequences for the Java VM.

### 2. RxJava基本模型
RxJava最核心的两个东西是Observables（被观察者，事件源）和Subscribers（观察者）。Observables发出一系列事件，Subscribers处理这些事件。这里的事件可以是任何你感兴趣的东西，如触摸事件，web接口调用返回的数据等等。
这里我们以一个简单的Todo List的app为例来解释RxJava的基本工作原理。
首先假设我们有一个todo list：
```java
    toDoList = {"Sweep", "Mop", "Vacuum"};
```

第一步先创建一个Observable: 
```java
Observable.just(todoList) 
```
这里用了just方法创建了一个Observable，表示了Observable 每次会发(emit)出todoList中的一项。

接下来是subscribe Observer, 代码和注释如下：
```java
Subscription s = Observable.just(todoList)
.subscribe(new Observer<Todo>() { //Type is the data type being emitted
    @Override
    public void onNext(Todo t) {
        //onNext is called for each item emitted.
    }

    @Override
    public void onCompleted() {
        //onCompleted is called when the Observable has no more items to admit
    }

    @Override
    public void onError(Throwable e) {
        //onError is called if an error occurs.
    }
    //It is important to note that onCompleted and onError are only ever called once.
    //And after they are called, onNext will not be called again.
});
```

调用subscribe方法会返回一个Subscription的对象, 有了它我们可以在关闭app的时候unsubscribe, 比如:
```java
...
@Override
protected void onDestroy() {
    super.onDestroy();
    s.unsubscribe();
}
...
```

以上就是RxJava的基本模型。

RxJava中包含了一些非常有用的类，可以使得在特定情况下代码写起来更简单。
比如说有时候我们并不需要onCompleted和onError的callback，只想知道Observable是否发出了item。这种情况下我们只需要在subscribe方法中传入一个Action1对象即可。
```java
Observable.just(todoList)
.subscribe(new Action1<Todo>() {

    @Override
    public void call(Todo todo) {
        //Get called for each item emitted.
    }
});
```

#### 参考
- [RxJava Home](https://github.com/ReactiveX/RxJava/wiki)
- [RxMarbles](http://rxmarbles.com)
- [Grokking RxJava, Part 1: The Basics](http://blog.danlew.net/2014/09/15/grokking-rxjava-part-1/)
- [Grokking RxJava, Part 2: Operator, Operator](http://blog.danlew.net/2014/09/22/grokking-rxjava-part-2/)
- [Grokking RxJava, Part 3: Reactive with Benefits](http://blog.danlew.net/2014/09/30/grokking-rxjava-part-3/)
- [Grokking RxJava, Part 4: Reactive Android](http://blog.danlew.net/2014/10/08/grokking-rxjava-part-4/)
- [更上一层楼－Android研发工程师高级进阶](https://www.gitbook.com/book/asce1885/android-rd-senior-advanced/details)