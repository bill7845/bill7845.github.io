---
layout: post
title: oop_Reference 형변환
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> Reference </center>
---
<br>
* __UpCasting__
* __DownCasting__

<br>

_레퍼런스 형 변환_
> 상속,인터페이스 부모 자식간에 레퍼런스 타입의 형변환

<br>

## 1. UpCasting
>부모는 자식객체의 멤버에 접근할 수 없었지만 Upcasting을 통해 부모의 객체로 자식 객체의 멤버를 사용할 수 있게 됨 __단, 부모가 갖고 있는 멤버 한정__

<br>

_UpCasting 첫번째 방법_
```
childClass ch = new childClass();
Parents pa = ch;  // 업캐스팅 , 자식 객체명 앞에 (부모타입) 붙어야하나 생략가능
```

<br>

_UpCasting 두번째 방법_
```
parents pa = new childClass();  // 부모타입 객체명 = new 자식타입

```

<br>

_예제_
```java
class Animal { // super 클래스
	String name;

	public void name() {
		name = "동물";
		System.out.println("Animal = " + name);
	}
}
//=======================================================
class Dog extends Animal { // Animal 클래스 상속
	public void name() { // 오버라이딩
		name = "강아지";
		System.out.println("Dog = " + name);
	}

	public void dMethod() { // Dog 메소드
		System.out.println("반려동물");
	}
}
//=======================================================
class Lion extends Animal { // Animal 클래스 상속
	public void name() { // 오버라이딩
		name = "사자";
		System.out.println("Lion= " + name);
	}
}
//=======================================================
class Yorkshire extends Dog { // Dog 클래스 상속
	public void name() { // 오버라이딩
		name = "요크셔테리어";
		System.out.println("Yorkshire = " + name);
	}
}
//=======================================================
public class RefCasting {

	public static void main(String[] args) {
		Dog d1 = new Dog();
		Animal a1 = (Animal) d1; // 업캐스팅 / 부모타입 생략 가능
		a1.name(); // 출력 : 강아지
		// a1.dMethod(); // 자식 클래스에만 있는 메소드로, 부모 객체로 호출 불가

		Lion l1 = new Lion();
		Animal a2 = l1; // 업 캐스팅
		a2.name(); // 출력 : 사자

		Animal a3 = new Yorkshire(); // 업 캐스팅
		a3.name(); // 출력 : 요크셔테리어
	}
}
//=======================================================
// <!-- [출처] [JAVA/자바] 레퍼런스(reference) 형 변환(업 캐스팅, 다운 캐스팅)|작성자 JOKER -->
```

<br>

## 2. DownCasting
> 부모 타입을 자식 타입으로 변환하는 것을 의미한다
> 업 캐스팅시에 부모타입에 없는 멤버의 경우 사용이 불가능했다 자식타입의 멤버가 필요할 경우 다운캐스팅을 통해 자식타입 멤버를 사용해준다
> 자주 사용되지는 않으나, 조건은 부모타입으로 업캐스팅 한 후 다시 자식타입으로 다운캐스팅 해야한다
> 다운캐스팅의 경우 자료형 생략 불가능
```
 Parents pa = ch;   // 1. 선행조건 업캐스팅
 Child Ch = Child(pa);  //2. 다운캐스팅  //자료형 생략불가 //자식타입 자식객체 = 자식타입(부모객체);
```

<br>

_예제_
```java
class SmartPhone { // 슈퍼 클래스
	public void name(){
		System.out.println("스마트폰");
	}
}

class Apple extends SmartPhone { // 서브 클래스
	public void name() { // 오버라이딩
		System.out.println("회사명 : 애플");
	}
	public void iPhone(){
		System.out.println("모델 : 아이폰");
	}
}

class Samsung extends SmartPhone{ // 서브 클래스
	public void name() { // 오버라이딩
		System.out.println("회사명 : 삼성");
	}
	public void galaxy(){
		System.out.println("모델 : 갤럭시");
	}
}

public class RefCastingEx02 {

	public static void main(String[] args) {
		Apple a1 = new Apple();
		SmartPhone sp1 = a1; // 업캐스팅
		sp1.name();
//		sp1.iPhone(); // 자식 메소드 사용 불가
		a1 = (Apple)sp1; // 다운 캐스팅
		a1.iPhone();

		SmartPhone sp2 = new Samsung(); // 업캐스팅
		sp2.name();
//		sp2.galaxy(); // 자식 메소드 사용 불가
		Samsung s1 = (Samsung)sp2; // 다운 캐스팅
		s1.galaxy();

		Apple a2 = (Apple) new SmartPhone(); // 다운 캐스팅
		a2.name(); // 예외 발생(다운 캐스팅을 하기 위해서는 업 캐스팅이 선행 되어야 함.)
	}
}

// [출처] [JAVA/자바] 레퍼런스(reference) 형 변환(업 캐스팅, 다운 캐스팅)|작성자 JOKER
```
