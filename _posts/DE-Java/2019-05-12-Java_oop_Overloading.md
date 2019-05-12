---
layout: post
title: [oop] Overloading
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

#  Overloading

* __method Overloading__
* __constructor Overloading__

## 1. Overloading
> 1개의 클래스에서 동일한 이름의 메서드(혹은 생성자)를 여러개 정의하는것을 의미
>오버로딩이 성립하기 위해서는 동일한 메서드 이름과 __매개변수의 자료형,개수,순서 를 다르게 설정하여야 한다__

<br>

_오버로딩을 왜 사용하는가?_
> 오버로딩을 사용함으로써 동일한 기능을 하는 메서드로 부터(메서드는 단 하나의 리턴값을 가질 수 있다) 다양한 리턴값을 반환시킬 수 있게 된다
> 생성자 오버로딩 또한, 다양한 입력값(매개변수)을 통한 초기화를 위해 사용된다

<br>

```{.java}
// 생성자 오버로딩을 통한 초기화

public class OverloadingEx02 {
	// 전역변수
	String name;
	String company = "apple";
	String model = "iPhone7";
	String number = "비공개";

	// 생성자
	public OverloadingEx02(String name) {
		this.name = name;
	}
	// 생성자 오버로딩
	public OverloadingEx02(String name, String number) {
		this.name = name;
		this.number = number;
	}
	// 메소드
	public void print() {
		System.out.println("이름 : " + name + "\n회사/모델명 : " + company + "/" + model
				+ "\n전화번호 : " + number);
	}

  public static void main(String[] args) {

    // 인스턴스를 각각 생성하여 초기화
		OverloadingEx02 ol = new OverloadingEx02("joker"); // 첫번째 생성자 호출
		ol.print();
		System.out.println();
		OverloadingEx02 ol2 = new OverloadingEx02("bat", "010-0101-1234"); // 두번째 생성자 호출
		ol2.print();
	}
}

//[출처] [JAVA/자바] 메소드/생성자 오버로딩(Overloading)|작성자 JOKER

```
