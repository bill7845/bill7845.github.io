---
layout: post
title: oop_인스턴스 멤버와 This
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

<br>

# 인스턴스 멤버와 this
---

<br>

* __인스턴스 멤버__
* __this__
* __this()__

<br>

## 1. 인스턴스 멤버와 this

<br>

> 인스턴스 멤버란 인스턴스가 가지고 있는 필드멤버,필드메서드를 의미한다 <br> this를 사용하는 이유는 필드 멤버(전역변수)와 매개변수(지역변수)를 명확히 구분하기 위해 사용한다 <br> this.a = a;에서 this를 붙여줌으로써 앞의 a는 멤버변수 뒤의 a는 매개변수(지역변수)라는것을 구분시켜준다 <br>매개변수와 필드의 변수명이 다를 경우는 this를 쓰지 않아도 상관없다. 하지만 소스코드가 복잡해지고 변수가 많아지면 관리하기가 힘들기 때문에 필드와 매개변수를 동일하게 정의하고 this.로 구분하는 것이 편리하다<br>
<!-- [출처] [JAVA/자바] 인스턴스 멤버 및 this의 의미|작성자 JOKER -->

```java

import java.util.Scanner;

public class InstanceMemberEx02 {
	int a, b; // 필드

	public InstanceMemberEx02(int a, int b){ // 생성자(매개변수)
		this.a = a; // this.a는 필드 / a는 매개변수를 의미
		this.b = b; // this.b는 필드 / b는 매개변수를 의미
	}

	public void sum(){ // 메소드
		int sum = 0; // 초기값
		if(a<b){
			for(int i = a; i<= b; i++){
				sum += i; // 누적합 / sum = sum + i;
			}
		}else{
			for(int i = b; i<= a; i++){
				sum += i; // 누적합 / sum = sum + i;
			}
		}
		System.out.println(sum);
	}

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("2개의 정수 입력");
		int a = sc.nextInt();
		int b = sc.nextInt();
		InstanceMemberEx02 im = new InstanceMemberEx02(a, b);
		im.sum();
	}
}
// [출처] [JAVA/자바] 인스턴스 멤버 및 this의 의미|작성자 JOKER
```

<br>

## 2. this()

<br>

> 자기 자신의 다른 생성자를 호출
> 생성자에서만 사용가능, 맨 윗줄에 사용

```java

public class InstanceMemberEx03 {
	String year;
	String month;
	String day;

  //생성자 1 // 생성자 3 호출하여 중복 제거
	public InstanceMemberEx03(String year) {
		this(year, null, null);
	}

  //생성자 2 // 생성자3 호출하여 중복 제거
	public InstanceMemberEx03(String year, String month) {
		this(year, month, null);
	}

  //생성자 3 에서 필드변수 = 매개변수 정의
	public InstanceMemberEx03(String year, String month, String day) {
		this.year = year;
		this.month = month;
		this.day = day;
	}

	public static void main(String[] args) {
		InstanceMemberEx03 im1 = new InstanceMemberEx03("2017년");
		System.out.println(im1.year);
		InstanceMemberEx03 im2 = new InstanceMemberEx03("2017년", "3월");
		System.out.println(im2.year + im2.month);
		InstanceMemberEx03 im3 = new InstanceMemberEx03("2017년", "3월", "13일");
		System.out.println(im3.year + im3.month + im3.day);
	}
}
// [출처] [JAVA/자바] 인스턴스 멤버 및 this의 의미|작성자 JOKER
```
