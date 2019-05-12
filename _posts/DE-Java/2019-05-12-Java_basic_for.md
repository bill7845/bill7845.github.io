---
layout: post
title: Basic_반복분
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

<br>

# <center> 반복문 </center>
---

<br>

* __for 기본 예제__

<br>

## 1. for 예제

<br>

> 문장 입력받은 후 거꾸로 출력

```java
Scanner input = new Scanner(System.in);
System.out.println("문장입력 :");

String msg = input.nextLine();
int length = msg.length();

for ( int i=length-1 ; i>=0 ; i-- ) { // length-1
  System.out.print(msg.charAt(i));
  }
```
