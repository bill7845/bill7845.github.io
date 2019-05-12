---
layout: post
title: [basic] 반복분
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

# 반복문

* __for 기본 예제__


## 1. for 예제
> 문장 입력받은 후 거꾸로 출력
```{.java}
Scanner input = new Scanner(System.in);
System.out.println("문장입력 :");

String msg = input.nextLine();
int length = msg.length();

for ( int i=length-1 ; i>=0 ; i-- ) { // length-1
  System.out.print(msg.charAt(i));
  }
```
