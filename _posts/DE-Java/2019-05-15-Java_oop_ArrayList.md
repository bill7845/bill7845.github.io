---
layout: post
title: oop_ArrayList
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> ArrayList </center>
---

<br>

* __동적배열 ArrayList__
* __향상된 for문 활용__

<br>

## 1. 동적배열

<br>

_크기가 정해져 있지 않은 동적배열 ArrayList_

> ArrayList는 크기가 정해져 있지않으며 기본적으로 Object 타입의 자료형을 갖는다
> ArrayList에도 자료형을 지정할 수 있으며 반복문등으로 값을 뽑아내기 위해서는 자료형을 지정해주어야 한다

```java
ArrayList<String> list = new ArrayList<String>();	 //String자료형을 갖는 동적배열
list.add("사자"); // listname.add를 통해 값 입력
list.add("호랑이");
list.add("코끼리");
list.add("토끼");
list.add("고양이");
// list.add(3);	//

for (int i = 0; i < list.size(); i++) {
  String str = (String)list.get(i);
  // list의 값을 반환하기 위한 get메서드는 기본적으로 object형을 반환하기 때문에 casting 필요
  System.out.println(str);
}

// 향상된 for문
for(String str : list){
  System.out.println(str);
}

		System.out.println(list);

		list.set(2, "dog");	// 값 변경 => list.set(index,value)
		System.out.println(list);

		list.remove(4);	// 값 제거 => list.remove(index)
		System.out.println(list);

		Collections.sort(list);	//	Collections 라는 클래스
		System.out.println(list);

		for (String str : list) {	// 향상 된 for 문 쓰려면 자료형 정해줘야함
			System.out.println(str);
		}

```

<br>

``` java
import java.util.ArrayList;

import javax.swing.text.html.HTMLDocument.Iterator;

public class ArrayListEx2 {

	public static void main(String[] args) {

		ArrayList<Student> re = method(); //static메서드 접근  //반환 된 Arraylist받기 위한 동일 자료형 변수 설정

    for(Student o : re){
      System.println(o);
    }
  }

	static ArrayList method() {  //ArrayList 반환 메서드
		Student a = new Student("홍길자", 20);
		Student b = new Student("홍길숙", 30);
		Student c = new Student("홍길동", 40);
		ArrayList<Student> list = new ArrayList<Student>();	// string,int 둘다 반환 타입을 클래스로 줘버림
		list.add(a);  // Student타입 a객체가 동적배열에 추가 됨
		list.add(b);
		list.add(c);
		return list;  // ArrayList 반환
	}
}

class Student {
	String name;
	int age;

	public Student(String name, int age) {
		this.name = name;
		this.age = age;
	}

	public String toString() {
		return name + "학생은" + age + "세입니다";
	}
}

```
