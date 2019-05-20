---
layout: post
title: oop_MapCollection
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> MapCollection </center>
---

<br>

* __맵 컬렉션__
* __HashMap__
* __HashSet__

<br>

## 1. Map

<br>

> Map은 <key,value> 구성된 _객체_ 를 저장하는 구조
> key는 유일값이며 value는 중복이 가능하다(동일key로 추가시 기존 key 제거)

<br>

_MapCollection_ 을 구현하는 HashMap 클래스

```java
import java.util.HashMap;
import java.util.Scanner;

public class HashMapEx {

	public static void main(String[] args) {

		HashMap<String,String> map = new HashMap();	// <키 형식 , 벨류 형식> // HashMap 객체 선언

		map.put("kimjava", "1111"); // HashMap에 값추가 메서드 put()
		map.put("parkjava", "1234");
		map.put("leejava", "1234");
		map.put("kimjava", "999");	// 중복안된다. 따라서 앞의 kimjava/1111 은 지워지고 kimjava의 value는 999가 된다

    System.out.println(map); // {parkjava=1234 , leejava=1234, kimjava = 999}

```
<br>

```java
import java.util.HashMap;
import java.util.Scanner;

public class HashMapEx {

	public static void main(String[] args) {
		Scanner input = new Scanner(System.in);
		boolean stop = false;
		while(!stop) {
			System.out.println("아이디/패스워드 : ");
			System.out.println("아이디 입력 : ");
			String id = input.next();
			System.out.println("패스워드 입력 : ");
			String pw = input.next();

			if(map.containsKey(id)) { // id가 map의 key에 해당되는가?(map이 id라는 key값을 갖고있는가)
				if(map.get(id).equals(pw)) { //아이디와 같은 key의 값과 입력받은 비밀번호가 같은가	// equals로  주소값 비교?
					System.out.println("로그인 성공");
					break; // or boolean stop = true
				}else {
					System.out.println("비밀번호가 일치하지 않습니다");
					continue;
				}
			} else {
				System.out.println("존재하지 않는 아이디입니다");
				continue;
			}
		}
```
