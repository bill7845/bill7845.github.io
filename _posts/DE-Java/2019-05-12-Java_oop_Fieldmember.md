---
layout: post
title: oop_변수
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

# Java variable

* __field__
* __전역변수와 지역변수__


## 1. field
> 필드 => 전역변수/멤버변수
> 필드는 클래스의 내부이면서 메서드의 외부에서 선언/정의 되어진다
> __필드는 선언만으로도 초기값을 가진다__
```{.java}

class field1 {
	// 필드
	int a;
	String str;

	// 생성자
	public field1(){
		str = "전역변수"; // str 초기화
	}

	// 메소드
	public void print(){
		int b;        // 지역변수 선언 // 지역변수는 초기값을 설정해주어야한다
		System.out.println(a);      // 출력 : 0 // 필드에서 선언되었음으로 초기값 할당받음
//  	System.out.println(b);       // 컴파일 에러
		String str = "지역변수";      // 지역변수 선언
		System.out.println(str);      // 출력 : 지역변수
		System.out.println(this.str);      // 출력 : 전역변수 // 메서드 내에서 전역변수 사용하기
	}
}

public class field_main{
	public static void main(String[] args) {

		field fv = new field1(); // 인스턴스 생성
		fv.print(); // 메소드 호출
	}
}

// [출처] [JAVA/자바] 필드(field) - 전역변수, 멤버변수|작성자 JOKER
```
> 위 코드에서 지역변수와 전역변수의 차이점에 주목하자
> 전역변수는 선언하는것만으로도 초기값을 할당받지만 지역변수의 경우는 선언과 초기화를 반드시 해주어야 한다
> 전역변수와 메서드내의 지역변수가 동일한 타입,이름일 경우, 메서드내에서는  해당 메서드의 지역변수가 우선순위로 호출된다 이경우 만약, 전역변수를 사용하고 싶다면 this를 붙여야한다
