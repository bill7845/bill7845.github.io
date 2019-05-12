---
layout: post
title: oop_상속
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

# 상속

* __상속__
* __상속과 생성자__
* __오버라이딩__

##  1. 상속
> 상속을 통해 부모 클래스의 필드와 메서드를 자식 클래스에서 사용가능하다
> 단, 여러 부모클래스를 갖는 다중상속은 불가능하다 (? 이중상속??)
```{.java}
class A {
	String aField = "클래스 A 필드";
	public void aMethod() {
		System.out.println(aField);
		// System.out.println("A : "+ bField); // 컴파일 에러(자식 필드 사용 불가)
	}
}

class B extends A {
	String bField = "클래스 B 필드";
	public void bMethod() {
		System.out.println(aField); // 부모 클래스 필드 사용
		System.out.println(bField); // 본인 클래스 필드 사용
		// System.out.println("B : "+cField); // 컴파일 에러(자식 필드 사용 불가)
	}
}

class C extends B { // 부모의 부모 클래스까지 상속받음
	String cField = "클래스 C 필드";
	public void cMethod() {
		System.out.println(aField); // 조부모 클래스 필드 사용
		System.out.println(bField); // 부모 클래스 필드 사용
		System.out.println(cField); // 본인 클래스 필드 사용
	}
}

public class SuperSubEx01 {
	public static void main(String[] args) {
		System.out.println("----------A----------");
		A a = new A();
		a.aMethod(); // 본인 메소드 사용
		// a.bMethod(); // A(부모) 객체로 B(자식) 메소드 접근 불가
		System.out.println("----------A----------");
		System.out.println("----------B----------");
		B b = new B();
		b.aMethod(); // 부모 메소드 사용
		b.bMethod(); // 본인 메소드 사용
		// b.cMethod(); // B(부모) 객체로 C(자식) 메소드 접근 불가
		System.out.println("----------B----------");
		System.out.println("----------C----------");
		C c = new C();
		c.aMethod(); // 조부모 메소드 사용
		c.bMethod(); // 부모 메소드 사용
		c.cMethod(); // 본인 메소드 사용
		System.out.println("----------C----------");
	}
}
[출처] [JAVA/자바] 상속의 개념 및 부모/자식 클래스|작성자 JOKER
```

<br>

_개발자 입장에서 상속
1. 부모클래스 멤버로 있는 경우 => 그냥 호출
2. 부모 클래스에 없는 경우  => 추가
3. 부모 클래스에 있는데 수정이 필요한 경우 => overriding을 통한 수정_

<br>

### 1.1 상속과 생성자
> 부모클래스의 필드와 메서드를 상속받기 전에 우선, 부모 인스턴스가 생성되어야 한다 단, 생성자는 될 수 없으며 자식인스턴스가 생성될 때 자동으로
__부모클래스의 기본 생성자가 호출된다__
> 만약 부모클래스에서 기본생성자 외에 매개변수를 갖는 생성자가 있다면 이는 자식클래스에서 자동호출되지 않으며 자식클래스 생성자에서 super()를 통해 호출해주어야 한다

```{.java}
class SuperClass {  // 부모클래스
	public SuperClass(String str){ // 매개변수를 갖는 부모클래스 생성자
		System.out.println(str + "호출");
	}
}

class SubClass extends SuperClass{  // 자식클래스
	public SubClass() { // 자식 생성자  // 자식생성자에서 부모클래스 생성자 호출 super()
		super("부모 생성자 "); // 부모 생성자 호출
		System.out.println("자식 생성자 호출");
	}
}

public class InheritanceConstructorEx01 {
	public static void main(String[] args) {
		SubClass sc = new SubClass(); // 자식 인스턴스 생성
	}
}

[출처] [JAVA/자바] 상속에서의 생성자|작성자 JOKER
```
<br>

## 2. Overriding

_상속에 의한 메서드 오버라이딩_

> 자식클래스에서는 부모클래스의 필드와 메서드를 물려받게되는데 자식클래스에서는 부모클래스의 메서드를 __재정의__ 하여 사용할 수 있다
> 메서드 오버라이딩 조건 : __메소드 이름, 리턴 타입, 매개변수의 갯수,순서,자료형 동일__
> 만약 오버라이딩 된 메서드에서 부모의 메서드를 그대로 호출하고 싶은 경우 super.메서드이름을 이용하면 된다
```{.java}

class Woman{ //부모클래스

    public String name;
    public int age;

    public void info(){
        System.out.println("여자의 이름은 "+name+", 나이는 "+age+"살입니다.");
    }
}

class Job extends Woman{ //Woman클래스(부모클래스)를 상속받음 :

    String job;

    public void info() {//부모(Woman)클래스에 있는 info()메서드 오버라이딩
        super.info(); // 부모메서드를 그대로 호출함
        System.out.println("여자의 직업은 "+job+"입니다.");
    }
}

public class OverTest {

    public static void main(String[] args) {

        Job job = new Job();

        //변수 설정
        job.name = "유리";  // 상속에 의한 접근
        job.age = 30;
        job.job = "프로그래머";

        //호출
        job.info();

    }
}
<!-- 출처: https://private.tistory.com/25 [공부해서 남 주자] -->

```
