---
layout: post
title: Basic_연산자
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

<br>

# <center> 연산자 활용 </center>
---

<br>

* 연산자

<br>

## 1. 연산자를 활용한 예제

<br>
> 1.문자 입력받기  
> 2.(1) 대문자인지 출력  (2)대문자인지 소문자인지 그 외인지 출력

```java
Scanner input = new Scanner(System.in);
System.out.println("문자 하나 입력:");
char ch = input.next().charAt(0);

System.out.println("입력값 = "+ch);

if (ch>='A' & ch<='Z') {
  System.out.println("대문자");
}else if (ch>='a' && ch<='z') {
  System.out.println("소문자");
}
```
