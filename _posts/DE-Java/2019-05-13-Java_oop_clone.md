---
layout: post
title: oop_Clone
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> clone & equals </center>
---

<br>

* __clone__
* __객체 clone__
* __equals__

<br>

## 1. clone?

<br>

> 얇은 복사를 통한 복사는 기존 객체의 __주소값__ 을 복사한것이다 따라서, 새로운 객체가 생성된 것이 아니다
> 새로운 객체가 생성된 것이 아니므로 __복사된 주소값__ 에 어떠한 수정사항이 발생한다면 해당 주소를 참조하고있는 모든 객체에 수정사항이 적용된다
> 객체의 주소값만 복사하는것이 아닌 메모리 자체를 복사하기 위해 object method인 clone메서드를 사용한다
> clone메서드는 메모리 자체를 복사하는것이기 때문에 복사와 동시에 객체가 생성된다

```java

import java.util.Arrays;

public class CloneEx {

	public static void main(String[] args) {

		String [] array = {"안녕","헬로우","올라","곤니찌와"};

		String [] copy = array;	// 얇은 복사	// copy는 array의 주소값만을 갖고있음
//		String [] copy = array.clone(); // 깊은 복사 	// clone통해서 주소값이 아니라 메모리 자체를 복사하여 객체가 새로만들어짐
//		System.out.println(Arrays.toString(array));
//		System.out.println(Arrays.toString(copy));

		copy[1] = "Hello";
//		copy[2] = "Hola";

		System.out.println(Arrays.toString(array));
		System.out.println(Arrays.toString(copy));
	}

}

```

<br>

## 2. equasls
