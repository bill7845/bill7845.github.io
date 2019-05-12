---
layout: post
title: Basic_DataType
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

<br>

# <center> Data Type </center>
---

<br>

* __기본형__
* __참조형__
* __String__
* __임시값을 활용한 swap__
* __Data 형변환 방법__

<br>

## 1. 기본형 데이터

<br>

> 문자형(char),정수형(int),실수형(double),논리형(boolean)
> 기본형 DataType에서는 생성자를 필요로 하지 않는다

```java
char a = 'A';  // char type의 경우 ''
int b = 7;
double c = 7.1;  // float으로 사용할수 있지만 주로 double형식으로 사용
boolean d = True;
```

<br>

> char과 int type의 경우  아스키값에 의해 변환될수 있음에 주의

```java
char a = '1'; // return 65
int b = 'a'; // return 97
```

<br>

> data type이 맞지 않게 선언을 하더라도 크기가 큰 type에 작은 type을 대입하는것은 문제가 없다
> 반대의 경우, casting을 통해 해결한다

```java
double db = 100;
System.out.println("db값 : " +db);

int in = (int)100.1; // casting
System.out.println("in 값 :"+in);
```

<br>

## 2. 참조형 데이터
> 문자열(String), 클래스(class), 배열(array)
> 참조형의 경우에는 반드시 new 연산자를 이용하여 메모리 할당

<br>

> 단, String type의 경우에는 생성자를 이용하지 않아도 된다.
> String의 경우 new 연산자에 의해 생성된 객체에 값이 저장된다는것에 주의

```java
String a = "abc";
String b = "abc";

if (a == b){
  System.out.println("같다");
}else {
  System.out.println("다르다"); // return 다르다
}
```

<br>

> 만약 값만을 비교하고 싶다면 equals()를 사용하여 객체의 주소가 아닌 값을 비교할수 있다

```java
if(a.equals(b)) { // a와 b의 값이 같은가?
  System.out.println("이름이 같다"); //return 이름이 같다.
}else {
  System.out.println("이름이 다르다");
}
```

<br>

## 3. String
> 독특한 String 문법들

<br>

### 3.1 equals()
>String type의 데이터의 값을 비교하는 방법

```
String str = "안녕하세요";
aa = str.substring(0,2);

if (aa.equals("안녕"){
  System.out.println("t"); //return
}else{
  System.out.println("f");
}

```

<br>

### 3.2 String & Token

<br>

> String type의 값을 Token을 기준으로 다루는 방식
> Token은 사용자 지정 ?
> StringTokenizer / hasMoreTokens / nextToken

```
String str = "독도는 대한민국의 아름다운 섬입니다";
StringTokenizer st = new StringTokenizer(str); //조건 지정이 없으면 공백 기준
//StringTokenizer st = new StringTokenizer(str,"+-*/"); // 사용자 지정 기준

while(st.hasMoreTokens()) { //hasMoreTokens()도 token사용자 지정 가능
System.out.println(st.nextToken()); //nextToken
```

<br>

## 4. 임시값을 활용한 swap

<br>

> 임시값을 만들어 값을 swap하는 방법
> 이와 같은 방법은 주로 반복문과 같이 활용한다

```java
int temp = kor; //임시저장값 temp
kor = eng;
eng = temp;
System.out.println("국어 :"+kor + ",영어:"+eng);
System.out.printf("국어 : %d, 영어: %d", kor,eng);
```

<br>

## 5. Data 형 변환 방법

<br>

> casting을 통한 변환이 불가능한경우의 형변환 법
> 계속 추가

<br>

### 4.1 String -> int로의 형변환

<br>

> 참조형인 Str타입은 기본형으로의 casting이 불가능하다
> 따라서 이 경우 특정 메서드를 사용하여야 한다
> 'Interger class'

```java
String id = "940622-1300133";
char sung = id.charAt(7);
Calendar c = Calendar.getInstance();
int year = c.get(Calendar.YEAR);

String age_1 = id.substring(0,2); // Str값으로 받아온 age_1
int age_2 = Integer.parseInt(age_1); //Integer.parseInt(value)을 통한 변환

int age = 0;
if (sung == '1' | sung == '2') {
  age = year - (1900+age_2) +1;
  System.out.println("당신의 나이는"+age);
}else if (sung == '3' | sung =='4') {
  age = year - (2000+age_2) +1;
  System.out.println("당신의 나이는"+age);
}
```
