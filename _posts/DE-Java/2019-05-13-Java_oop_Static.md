---
layout: post
title: oop_Static
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> Static </center>
---

<br>

* __Static__
* __Static을 사용하는 경우와 이유__
* __Static Method__

<br>

[참고사이트](https://vaert.tistory.com/101).

<br>

## 1.static을 사용하는 이유와 사용해야 하는 경우

<br>

### 1.1
>클래스를 설계할 때, 멤버변수 중 모든 인스턴스에 공통적으로 사용해야하는 것에 static을 붙인다.
>인스턴스를 생성하면, 각 인스턴스들은 서로 독립적기 때문에 서로 다른 값을 유지한다. <br>경우에 따라서는 각 인스턴스들이 공통적으로 같은 값이 유지되어야 하는 경우 static을 붙인다.

<br>

### 1.2
 >static이 붙은 멤버변수는 인스턴스를 생성하지 않아도 사용할 수 있다<br>
 static이 붙은 멤버변수(클래스변수)는 클래스가 메모리에 올라갈때 이미 자동적으로 생성되기 때문이다.

<br>

###1.3
>static이 붙은 메서드(함수)에서는 인스턴스 변수를 사용할 수 없다<br>
static이 메서드는 인스턴스 생성 없이 호출가능한 반면, 인스턴스 변수는 인스턴스를 생성해야만 존재하기 때문에... <br>static이 붙은 메서드(클래스메서드)를 호출할 때 인스턴스가 생성되어있을수도 그렇지 않을 수도 있어서 static이 붙은 메서드에서 인스턴스변수의 사용을 허용하지 않는다. (반대로, 인스턴스변수나 인스턴스메서드에서는 static이 붙은 멤버들을 사용하는 것이 언제나 가능하다. 인스턴스변수가 존재한다는 것은 static이 붙은 변수가 이미 메모리에 존재한다는 것을 의미하기 때문이다.)

<br>

### 1.4
>메서드 내에서 인스턴스 변수를 사용하지 않는다면, static을 붙이는 것을 고려한다<br>
메서드의 작업내용중에서 인스턴스 변수를 필요로 한다면, static을 붙일 수 없다. 반대로 인스턴스변수를 필요로 하지 않는다면,<br> 가능하면 static을 붙이는 것이 좋다. 메서드 호출시간이 짧아지기 때문에 효율이 높아진다. (static을 안붙인 메서드는 실행시 호출되어야할 메서드를 찾는 과정이 추가적으로 필요하기 때문에 시간이 더 걸린다.)

<br>

### 1.5
> 클래스 설계시 static의 사용지침<br>
먼저 클래스의 멤버변수중 모든 인스턴스에 공통된 값을 유지해야하는 것이 있는지살펴보고 있으면, static을 붙여준다<br>작성한 메서드 중에서 인스턴스 변수를 사용하지 않는 메서드에 대해서 static을붙일 것을 고려한다.

<br>

> 일반적으로 인스턴스변수와 관련된 작업을 하는 메서드는 인스턴스메서드(static이 안붙은 메서드)이고 <br> static변수(클래스변수)와 관련된 작업을 하는 메서드는 클래스메서드static이 붙은 메서드)라고 보면 된다

<br>

```java
class Card {
  String kind ;                           // 카드의 무늬 - 인스턴스 변수
  int number;                            // 카드의 숫자 - 인스턴스 변수
  static int width = 100 ;             // 카드의 폭 - 클래스 변수
  static int height = 250 ;            // 카드의 높이 - 클래스 변수
}

class CardTest{
  public static void main(String args[]) {

    System.out.println("Card.width = " + Card.width); //static member // class 명 접근
    System.out.println("Card.height = " + Card.height);

    Card c1 = new Card(); // 객체 생성
    c1.kind = "Heart";
    c1.number = 7;

    Card c2 = new Card(); // 객체 생성
    c2.kind = "Spade";
    c2.number = 4;

    System.out.println("c1은 " + c1.kind + ", " + c1.number + "이며, 크기는 (" + c1.width + ", " + c1.height + ")" );
    System.out.println("c2는 " + c2.kind + ", " + c2.number + "이며, 크기는 (" + c2.width + ", " + c2.height + ")" );      
    System.out.println("이제 c1의 width와 height를 각각 50, 80으로 변경합니다.");  
    c1.width = 50;  // static member 값 변경
    c1.height = 80; // static member 값 변경

    System.out.println("c1은 " + c1.kind + ", " + c1.number + "이며, 크기는 (" + c1.width + ", " + c1.height + ")" );
    System.out.println("c2는 " + c2.kind + ", " + c2.number + "이며, 크기는 (" + c2.width + ", " + c2.height + ")" );
  }
}

// 출처: https://vaert.tistory.com/101 [Vaert Street]
```

<br>

## 2. static 메서드

<br>

_어떤 경우에 메서드에 static을 부여하여야 하는가_
>클래스는 인스턴스 멤버와 그에 관련된 메서드들의 집합이다 만약 클래스의 메서드에서 인스턴스 변수를 사용하지 않는다면 <br>즉, 매개변수를 입력받는 메서드의 경우 static을 붙여주어 classmethod화 시켜준다
> 인스턴스 멤버를 사용하는 메서드의 경우에는 static을 부여하는 것이 불가능하다 => static메서드에서 인스터스변수 사용 불가능

```java
class MyMath2 {

  long a, b;

  // 인스턴스변수 a, b를 이용한 작업을 하므로 매개변수가 필요없다
  long add() {       return a + b; }
  long subtract() {       return a - b; }
  long multiply() {       return a * b; }
  double divide() {       return a / b; }


  // 인스턴스변수와 관계없이 매개변수만으로 작업이 가능하다  => static 부여
  static long add(long a, long b) {       return a + b; }
  static long subtract(long a, long b) {       return a - b; }
  static long multiply(long a, long b) {       return a * b; }
  static double divide(double a, double b) {       return a / b; }

}



class MyMathTest2 {

public static void main(String args[]) {

    // 클래스 메서드 호출
    System.out.println(MyMath2.add(200L, 100L));
    System.out.println(MyMath2.subtract(200L, 100L));
    System.out.println(MyMath2.multiply(200L, 100L));
    System.out.println(MyMath2.divide(200.0, 100.0));


    MyMath2 mm = new MyMath2(); // 인스턴스 메서드 호출 위한 객체 생성
    mm.a = 200L;  // 인스턴스 멤버변수 초기화
    mm.b = 100L;  // 인스턴스 멤버변수 초기화

    // 인스턴스메서드는 객체생성 후에만 호출이 가능함.
    System.out.println(mm.add());
    System.out.println(mm.subtract());
    System.out.println(mm.multiply());
    System.out.println(mm.divide());

}

// 출처: https://vaert.tistory.com/101 [Vaert Street]

```
