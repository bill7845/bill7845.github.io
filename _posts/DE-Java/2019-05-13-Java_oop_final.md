---
layout: post
title: oop_final
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> final </center>
---

<br>

* __final__
* __final 활용__

<br>

## 1. final이란?

<br>

> 파이널이란 "더 이상 변경이 불가능"이란 의미를 가진다
> _필드(전역변수)_,_메서드_,_클래스_ 에 부여 가능
> 필드에 가장 많이 사용되며 final이 붙은 필드는 __수정이 불가능하다__

<br>

> class에도 final이 선언될 수 있으며 final class는 즉, 오버라이딩 불가 -> 부모클래스가 될수 없음을 의미한다
> final이 붙은 메서드는 자식클래스에서 오버라이딩이 불가능하다 -> 즉, final과 abstract는 같이 사용할 수 없다

```java
class Parent { // class 에 final 붙일수도 있음 // 즉, 클래스 수정이 불가능 -> 자식이 오버라이딩 못함 -> 부모클래스가 될수 없다

	String field = "부모님꺼"; //여기에 final 붙이는 순간 자식에서도 변경 불가능 // final String field;

	public void job() { // 여기에 final 붙이는 순간 자식에서도 변경 불가능 // 즉, 오버라이딩 안되게 막아버림 // 결국 final 과 abstract 같이 못쓴다
		System.out.println("부모님께서 장만");
	}
}

class Child extends Parent {
	Child() {
		field = "내꺼임";
	}

	public void job() {
		System.out.println("물려받아 탕진");
	}
}

//==============================================================================================

public class Test {

	public static void main(String[] args) {

		// final -
		// final field - 값 변경 x
		// final method - 오버라이딩 불가
		// final class - 상속불가

		Parent p = new Child();
		System.out.println(p.field);
		p.job();
	}

}

```
