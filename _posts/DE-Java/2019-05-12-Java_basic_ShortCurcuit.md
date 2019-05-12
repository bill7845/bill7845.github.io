---
layout: post
title: [basic] ShortCurcit&삼항연산자
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

# ShortCurcuit & 삼항 연산자

* __shortcurcuit logic__
* __삼항 연산자__

## 1. ShortCurcuit logic
> 일반논리에 적용되는 숏서킷 로직
> &&,||의 연산자는 선행조건이 False이면 뒤 조건은 무조건 실행하지 않는다.
> 숏서킷 로직의 혼동을 피하기 위해 & , |(이진논리)을 주로 사용한다.
```{.java}
int a = 3;
if( a>3 && ++a>3) {
  System.out.println("조건만족"); // 출력여부 F
}
System.out.println("A="+a);  // a=?

if(a>1 || ++a>3) {
System.out.println("조건만족2");
}
System.out.println("A="+a);
```

## 2. 삼항 연산자
> (조건)? A : B 의 형태를 가지며 조건이 true 이면  A실행 false이면 B실행
> 자주 사용되지는 않으나 단순한 if~else문을 단축시킬수 있음
```{.java}
int score = 81;
String result = (score>=80)? "합격" : "불합격" ;
System.out.println("result");
```

<br>

### 2.1 중첩 삼항 연산자
> 삼항 연산자도 중복형태로 사용 가능
> (조건1)? T : (조건2)? T : (조건3)? T : F ... 의 형태로 중첩 가능
> 중첩 삼항 연산자 예시
```{.java}
Scanner input = new Scanner(System.in);

System.out.println("first_num :");
int first_num =  input.nextInt();
System.out.println("second_num :");
int second_num = input.nextInt();

int max = (first_num > second_num)? first_num : second_num;
System.out.println("큰 수:" +max);
```
