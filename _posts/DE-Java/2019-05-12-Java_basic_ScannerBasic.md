---
layout: post
title: [basic] Scanner
comments: true
categories: [Development Environment/Java]
tags: [Java]
---


# Scanner basic

* __Scanner__
* __Scanner 활용 실습__

## 1. Scanner
> 사용자로부터 값을 직접 입력받고 싶은경우 Scanner를 사용한다
```{.java}
Scanner aa = new Scanner(System.in);
System.out.println("값 입력 : ")
int input = input.next();

System.out.println("입력받은 값은 : "+input);
```

<br>

### 1.1 Scanner에서 값을 입력받는 형식의 종류
* next
* nextLine
* next와 nextLine 섞어 사용할 경우 문제점
* nextInt
> next와 nextLine의 차이점

<br>

>next의 경우 개행문자,공백을 무시하고 출력한다
```{.java}
Scanner aa = new Scanner(System.in);
System.out.println("입력 :"); // input 안 녕 하 세 요
String a = aa.next();
System.out.println(a); // return 안
```

<br>

> nextLine는 한 라인을 그대로 출력 한다
```{.java}
Scanner aa = new Scanner(System.in);
System.out.println("입력 :"); // input 안 녕 하 세 요
String a = aa.nextLine();
System.out.println(a); // return 안녕하세요
```


<br>

> nextInt는 정수값을 출력한다
```{.java}
Scanner aa = new Scanner(System.in);
System.out.println("입력 :"); // input 12345
String a = aa.next();
System.out.println(a); // return 12345
```

<br>
### 1.2  next와 nextLine을 섞어 사용할 경우 오류
```{.java}
Scanner input = new Scanner(System.in);

String input_1 = input.next(); // 가나다라 입력
System.out.println("next() = "+input_1); // return 가나다라

String input_2 = input.nextLine();
System.out.println("nextLine() ="+input_2); // 아무것도 출력하지 않음
```

<br>

### 1.3 char type을 Scanner으로 받아오기 (charAt)
> char을 받아오는 Scanner 형식은 존재하지 않는다.
> 따라서 우선, String형식으로 받아 온 후 'charAt(index)' 메서드를 통해 맨 앞을 추출해주어야 한다.
> 이때 단순히 char -> String 로의 casting을 통한 형변형을 하지 않는 이유는 참조형은 기본형으로의 변환이 불가능 하기 때문이다.
```{.java}
System.out.println("문자 하나 입력 :");
char ch = input.next().charAt(0); // charAt(index num)
System.out.println("입력받은 값 = "+ch);
```

<br>

## 2. Scanner 활용 실습
> 1~100 사이의 세 정수 A,B,C의 값을 입력받아 두번째로 큰 정수를 출력하라

```{.java}
Scanner input = new Scanner(System.in);

System.out.println("A = ");
int A = input.nextInt();

System.out.println("B = ");
int B = input.nextInt();

System.out.println("C = ");
int C = input.nextInt();

if (A<1 && A>100 || B<1 && B>100 || C<1 && C>100){
    System.out.print("입력 범위 초과");
}else if (A > B && B > C){
    System.out.print("return :"+B);
}else if (B > A && A > C){
    System.out.print("return :"+A);
}else if (B > C && C > A){
    System.out.print("return :"+C);
}else {
    System.out.print("Error(동일 숫자X");
  }
```
