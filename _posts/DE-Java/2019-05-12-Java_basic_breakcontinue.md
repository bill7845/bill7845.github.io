---
layout: post
title: Basic_break & continue
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

<br>

# <center> break & continue </center>
---

<br>

* __break__
* __continue__
* __label__

<br>

## 1. break

```java
for(int i=0; i<2; i++) {
  for(int j=0; j<3; j++) {
    if(j==1) break; // j 반복문 탈출 후 i반복문 실행
    System.out.println("<"+i+","+j+">");
  }
  System.out.println("DATA");
}
```

<br>

## 2. continue

<br>

```java
for(int i=0; i<2; i++) {
  for(int j=0; j<3; j++) {
    if(j==1) break; // 해당 조건 건너 뛴 후 j반복문 이어 실행
    System.out.println("<"+i+","+j+">");
  }
  System.out.println("DATA");
}
```

<br>

## 3. label을 통한 제어

<br>

> break label의 경우 해당 반복문이 속해있는 모든 반복문을 벗어난다

```java
END :   //labe 선언
for(int i=0; i<2; i++) {
  for(int j=0; j<3; j++) {
    if(j==1) break END;   // j,i 반복문 모두 break
    System.out.println("<"+i+","+j+">");
  }
  System.out.println("DATA");
}
```

<br>

> continue label의 경우 해당 반복문이 속해있는 반복문의 끝 직전? 으로 이동

```java
END :
for(int i=0; i<2; i++) {
  for(int j=0; j<3; j++) {
    if(j==1) continue END;   // j반복문 나간 후 i 반복문 끝의 직전으로 감
    System.out.println("<"+i+","+j+">");
  }
  System.out.println("DATA");
//여기}

// 즉, "DATA"출력 부분 실행 안됨
```
