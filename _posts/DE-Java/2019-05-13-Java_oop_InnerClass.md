---
layout: post
title: oop_InnerClass
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> InnerClass </center>
---

<br>

* __Inner Class__
* __내부클래스 객체 생성__
* __내부클래스 메서드 접근(static)__

<br>

## 1. 내부클래스 객체 생성

<br>

> 내부클래스를 사용하는 이유는 내부클래스는 외부클래스의 모든 자원에 접근 가능하기 때문이다 <br> 내부클래스를 사용하기 위해서는 <br>

```
outer o = new outer(); //외부 클래스 객체 생성
Inner in = o.new Inner();
```
>먼저, 외부클래스 객체를 생성 후 내부클래스 객체를 조건에 맞춰 생성한다 <br> 즉, 내부클래스를 외부클래스 객체생성없이 독단적으로 사용할 수 없다

<br>

### 1.1 내부클래스 메서드 접근(static)

<br>

> 만약, 내부클래스에 static이 부여되어있다고 하여도 이는, 내부클래스 객체가 메모리에 올라가는것이 아닌 단지 외부클래스에게 있어 static변수 취급을 가능하게 해주는것에 불과하다 <br>

> 내부클래스는 외부클래스의 멤버라고 생각해야한다. 따라서 클래스임에도 static이 부여될 수 있는것이다 <br> 내부클래스에 static이 부여된다고 하더라도 내부클래스 객체를 생성(new)해주어야 하지만 내부클래스의 static member변수가 존재 한다면 기존의 접근법처럼 Outer.Inner.변수명으로 접근이 가능하다

```java
package note_oop;

import note_oop.Outer.Inner;

class Outer {

	int value = 10; 	// 전역변수

	static class Inner { 	// 내부클래스	//static
		int value = 20;		// 내부클래스 전역변수

		public void bb() {	// 내부클래스 메서드
			int value = 30;

			System.out.println(value); // 30	// 내부클래스 -> 내부클래스 메서드 지역변수
			System.out.println(this.value); // 20	// 내부클래스 전역변수
//			System.out.println(Outer.this.value); // 10		// 내부클래스에서 외부클래스 전역변수 접근법
		}
	}
}

public class InnerClassExam {
	public static void main(String[] args) {
		Inner i = new Outer.Inner();	// 내부클래스 객체만들기 //static
		i.bb();
	}
}
```
