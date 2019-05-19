---
layout: post
title: Java 자료구조 Stack Queue
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> 자료구조 </center>
---

<br>

* __Stack__
* __Queue__

<br>

## 1. Stack

<br>

```java
//		Last In First Out 구조의 Stack
//    Push,pop

		Stack stack = new Stack();
		stack.push("A");	// stack 에 추가 push
		stack.push("B");
		stack.push("C");

		while(!stack.isEmpty()) {	// isEmpty() - 비었는지 확인
			System.out.println(stack.pop());	// pop - 하나씩 뽑음(LIFO)
		}
//		System.out.println(stack.pop()); // 비어있으면 예외발생
```

<br>

## 2. Queue

<br>

> FIFO 구조의 Queue
> Queue는 Interface다. 따라서 객체생성x => Queue를 구현한 class를 사용하여 객체를 생선한다

```java
//		Queue - FIFO(First in first out)
//		Queue queue = new Queue();	// Queue는 인터페이스이다. 따라서 객체생성 x // Queue를 구현한 class를 사용해 객체생성
		Queue queue = new LinkedList();	// queue를 구현한 LinkedList class
		queue.offer("가");
		queue.offer("나");
		queue.offer("다");
		while(!queue.isEmpty()) {
			System.out.println(queue.poll()); 	// queue에서 하나씩 뽑아오는 poll
		}
```
