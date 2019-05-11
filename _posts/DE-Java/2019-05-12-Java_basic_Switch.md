---
layout: post
title: Java Switch
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

# Switch

* __Switch 개념__
* __Switch 활용__

## 1. Switch 개념
> switch는 int/long/char/String(정수형/문자/문자열)의 type만 가능하다
> __default가 마지막에 있는 경우가 아니라면 default도 break 달아줘야함에 주의__
> default는 고정이 아니라 그외의 값을 의미함
> __break가 붙어있지 않은 case에서 조건이 성립한다면 그 아래에 조건들은 무조건 실행한다__
```{.java}
swith(변수){      
case A : 명령어A; break;
case B : 명령어B; break;
case C : 명령어C; break;
default : 그 외 명령어;
  }
```

<br>

### 1.1 Switch 활용 예제
```{.java}
String id = "940622-1300136";
char local = id.charAt(8);

String home = "";

switch(local) { // local 변수 char로 받은것에 주의
case '0' : home="서울"; break;
case '1' : home="인천/부산"; break;
case '4' : home="경기"; break;
case '9' : home="제주"; break;
default: home = "한국인";
}
```
