---
layout: post
title: Basic_DoWhile
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

<br>

# <center> Do While </center>
---

<br>

* __Do While 개념__
* __활용 예제__

<br>

## 1. Do while

<br>

>do 구문 무조건 실행 후 while문 조건문 가서 조건이 True이면 다시 do실행
>주로 __무조건 한번은 실행해야 하는 경우__  do~while사용

<br>

>기본 구조
> do의 실행문은 무조건 한번은 실행되게 된다

```java
do{
  실행문
}while(조건);   // while의 조건이 T이면 다시 do를 실행
```

<br>

##2 DO while 활용 예제

<br>

> 구구단 출력

```java
do {
	int i = 1;
	while (i <= 9) {
		System.out.printf("%d X %d=%d \n", dan, i, dan * i);
		i++;
	}
	System.out.println("Y/y ??");
	result = input_2.next().charAt(0);

}while (result == 'Y' | result == 'y'); // do while 에서는 ; 붙여야함
```
