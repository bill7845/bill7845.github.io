---
layout: post
title: oop_Set
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> Set </center>
---

<br>

* __Set__
* __HashSet__
* __TreeSet__
* __LinkedHashSet__

<br>

## 1. HashSet

<br>

> set은 순서를 신경쓰지 않고 데이터를 저장한다
> 순서가 필요없고 중복은 불허한다

```java
import java.util.HashSet;

public class HashSetEx {

	public static void main(String[] args) {

		HashSet list = new HashSet();
		list.add("사자");
		list.add("호랑이");
		list.add("코끼리");
		list.add("토끼");
		list.add("고양이");
		list.add("고양이");	// 중복 값 넣으면 알아서 피해줌

		System.out.println(list);	//set은 순서를 저장하지 않는다	// 중복값 들어가지 않는다
	}
}
```

<br>

> HashSet 활용

```java
public class HashSetLotto {

	public static void main(String[] args) {

		// 중복을 피하는 HashSet 이용하여 lotto 중복없이 출력

		HashSet<Integer> lotto = new HashSet<Integer>();

		while(lotto.size() < 6){	// for(i=0; i<6 ; i++) 를 사용하였을 경우 중복값 발생 시 5개만 출력되기 때문에 while 사용
			int su = (int)(Math.random()*45)+1;
			lotto.add(su);
		}
//		System.out.println(lotto);

		// 정렬까지
		ArrayList<Integer> li = new ArrayList<Integer>(lotto);	// set -> ArrayList
		Collections.sort(li);	// collections.sort 에 인자로 list만 들어올수 있음 set안됨
		System.out.println(li);
	}

}
```
