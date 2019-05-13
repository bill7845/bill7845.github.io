---
layout: post
title: ObJect Class
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> ObJect Class </center>
---

<br>

* __toString__
* __clone__
* __equals__

<br>

## 1. toString

<br>

> obj class의 메서드 toString()
> 객체가 가지고 있는 정보나 값들을 문자로 리턴해주는 메서드
> 오버라이딩(재정의)하여 사용가능

```java
/**
 * 최고 조상 클래스 Object의 toString() 메서드
 * toString() 출력시 : 클래스명@hashcode 값으로 출력해준다
 */
public class ToString {
    public static void main(String[] args) {
        Pen p = new Pen("모나미" , "검정" , 1);
//      System.out.println(p); // 참조변수 호출시 .toString() 자동호출
//      System.out.println(p.toString()); //위의 코드와 같다.


//      toString() 을 재구현해서 실행하면
//      [제품 : 모나미, 색상 : 검정 , 두께 : 1 ] 다음과 같이 나온다.
        System.out.println(p);


    } // end of main
} // end of class

class Pen{
    String name = ""; // 제품 이랑
    String color = ""; // 색
    int boldWidth; // 굵기

    public Pen() {
    }

    public Pen(String name, String color, int boldWidth) {
        super();
        this.name = name;
        this.color = color;
        this.boldWidth = boldWidth;
    }

    @Override // obj 메서드를 재정의하여 사용
    public String toString() {  
        // TODO Auto-generated method stub
        return "[제품 : " + name + ", 색상 : " + color + " , 두께 : " + boldWidth + " ] " ;
    }
}

// 출처: https://zzdd1558.tistory.com/139 [신입 개발자]
```

<br>

## 2. clone

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

## 3. equals

<br>

> equals 메서드를 오버라이딩하지않고 사용하면 객체의 주소값만을 비교함

```java
class Student {
  String hakbun , name;

	public Student(String hakbun, String name) {
		this.hakbun = hakbun;
		this.name = name;
	}
}

public class EqualsEx {

	public static void main(String[] args) {

		Student a = new Student("130173","홍길동");
		Student b = new Student("153243","박기혁");

		if (a.equals(b)) {    // a,b는 서로가 각각의 객체이므로 서로 다른 주소값을 갖고 있다
			System.out.println("동일인");
		} else {
			System.out.println("다른학생");  // return 다른학생
		}
}
}
```

<br>

_equals 오버라이딩_

```java
class Student {
  String hakbun , name;

	public Student(String hakbun, String name) {
		this.hakbun = hakbun;
		this.name = name;
	}

  public boolean equals(Object obj) {	  // equals 오버라이딩   //매개인자 obj는 메인에서 a.equals(b)로 호출하고 있음
  Student other = (Student)obj; // 다운캐스팅?	 
  if(hakbun.equals(other.hakbun)) return true;  // other.hakbun => b의 학번
  else return false;
  }

  public String toString(){   //toString 오버라이딩
    return "[" +hakbun+ "]" + name;
  }
}

public class EqualsEx {

	public static void main(String[] args) {

		Student a = new Student("130173","홍길동");
		Student b = new Student("153243","박기혁");

		if (a.equals(b)) {    // a,b는 서로가 각각의 객체이므로 서로 다른 주소값을 갖고 있다
			System.out.println("동일인");
		} else {
			System.out.println("다른학생");  // return 다른학생
		}
}
}
```
