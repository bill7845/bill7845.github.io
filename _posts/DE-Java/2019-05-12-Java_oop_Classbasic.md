---
layout: post
title: Java Class
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

# Class

* __Class 개념__
* __Class 변수와 메서드__


## 1. class란?
>동일한 자료형만을 담을 수 있는 '배열'과는 달리 class는 서로 다른 자료형의 변수뿐만 아니라 메서드 또한 담을 수 있다
> 따라서 class를 활용하여 꼭 필요한 부품(메서드,변수)들을 서로 연관되어 있는것끼리 묶어 중복없이 class에 저장할 수 있게되고 이를 "capsulation"이라 한다
> 이는, 코드의 불필요한 중복을 피하고 "재활용성"을 높힌다
```{.java}
// Student class
public class Student {

	String name;
	int kor, eng, math;
	int total;
	double avg;

	int calTotal() { // class안의 메서드
		total = kor+eng+math;
		return total;
	}

	double calAverage() { //class안의 메서드
		avg = (double)total/3;
		return avg;
	}


}
```
```{.java}
//main
public static void main(String[] args) {

  Student s = new Student(); // class 선언

  s.name = "홍길동"; // class 객체 접근법
  s.kor = 100;
  s.eng = 88;
  s.math = 77;
  System.out.println("총점 :"+s.calTotal());
```
## 2. class 객체 생성 및 접근
> class를 생성한 후 이를 main에서 호출하여 변수에 담는 과정
> 즉, 변수에 실제로 메모리를 적재하는 과정
> 아래의 코드를 보면 s라는 변수는 __Student라는 클래스를 자료형으로 가지며__ new라는 생성자에 의해 Student class에 의해 생성된 객체를 뜻 한다.
> 즉 클래스를 만든다는 것은 __사용자 정의 데이터 타입을 만드는 것과 같은 의미다__
```
  Student s = new Student();
```

<br>

> 생성된 객체를 통해 클래스 멤버변수에 접근하는 방법은
```
  s.name = "홍길동"; // 객체이름.클래스멤버변수
  s.kor = "100";
```

## 3. class 변수와 메서드
> 클래스 내부에서도 변수와 메서드를 선언할 수 있다
> 아래의 코드를 보면, class내에서 a,b,basic의 변수가 선언되어있고 static의 유무차이가 존재한다
```{.java}
class Calculator {
int a = 50;
int b = 50;
static int basic;

public void sum_1(int c , int d){    // method 1
    re = a + b + c + d;
    System.out.println(re);
  }

public void sum_2(int a, int b){    //ethod 2    // a,b,basic 3가지 인자가 필요하지만 baisc은 static로 설정해두었다
  re = a + b + basic;
  System.out.println(re);
  }
}

//============================================================================================================

public class main_class { // main

    public static void main(String[] args) {


    Calculator cal = new Calculator();  // 객체 생성
    //cal.a = 10;   // 이런식으로 접근하여 클래스 변수의 값을 수정가능
    //cal.b = 30;   // 클래스내부에 초기값이 정해져있는 경우에 초기값을 수정하기 위해서?

    Calculator.basic = 30;  // static basic을 통한 함수명 접근  // 객체 생성하지 않아도 접근 가능

    cal.sum_1(30,40);   // 변수명은 상관없다고 알고 있었으나 클래스 내부에서 선언된 int a,b의 경우 그대로 클래수내부 메서드에 대입된다. 따라서 30,40은 c,d로 대입된다
    cal.sum_2(100,300);   


}
```
> 위 코드를 보면 클래스 멤버변수로 a,basic은 초기값을 설정해 두지 않았고 b는 초기값을 20으로 주었다. sum_1메서드에서 인자값을 1개만 입력받도록 한다면 main에서 호출된 메서드(인자)에 의한 값 한가지와 클래스멤버변수에서 설정된 초기값에 의해 실행이 된다
> sum_2메서드의 인자 값으로 int a,b를 받아온다고 설정해놓았다. 그런데 이 경우 cal.sum_2(100,300)은 cal.a = 100, cal.b=300 과 같은 의미 아닌가?
> 두 코드의 의미가 다른 이유는 sum_2메서드는 무조건 int a,b의 인자를 받는다고 설정해 놓았다. 따라서 cal.a,cal.b를 통해 a,b값을 변경하더라도 sum_2메서드는 메서드 실행시 입력 된 인자값에 의해 실행 될 것이다

<br>

>
