---
layout: post
title: Thread_Runnable
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> Thread Runnable Interface </center>
---

<br>

* __Runnable Interface__


<br>

## 1. Interface 구현을 통한 Thread

<br>

> run메서드를 갖고있는 Runnalble Interface 구현
> Thread 클래스 상속을 통한 방법과 달리 start()메서드가 없다
> 별도의 Thread 생성 후 Runnable 인터페이스를 인자로 넘겨주어야 함

```java
/* Runnable Interface */
class foo implements Runnable{  // Runnable Interface
	@Override
	public void run() {   // run메서드 오버라이딩
		// do something...
	}
}
```

<br>

```java
package thread.basic;

public class Ex2_RunnableTest {

	public static void main(String[] args) {

//		MakeCar2 mc1 = new MakeCar2("차틀 만들기");    // 인터페이스 구현
//		Thread t1 = new Thread(mc1);	// 인터페이스 객체를 Thread 인자로
//		t1.start(); // start() 호출 -> run() 호출됨  //Runnable Interface를 인자로 갖고있는 thread이므로 start()메서드
//		
//		MakeCar2 mc2 = new MakeCar2("도색");
//		Thread t2 = new Thread(mc2);
//		t2.start();

//		Thread t2 = new Thread(new MakeCar2("도색"));	1단계 축약형

		new Thread(new MakeCar2("도색")).start(); // 2단계 축약형 ****
		new Thread(new MakeCar2("차틀만들기")).start();

		System.out.println("프로그램 끝");
	}

}

class MakeCar2 implements Runnable{	// Runnable 인터페이스 구현

	String work;

	public MakeCar2(String work){  // 생성자
		this.work = work;
	}

	public void run() {	// run메서드 오버라이딩
		for(int i=0; i<5; i++) {
			System.out.println(work +"작업중");

			try {	// 눈으로 확인하기 위해서
				Thread.sleep(500);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
}

```

## 2. Runnable VS Thread

<br>

> Thread 클래스 상속의 경우 다른 클래스 상속이 불가능하며, Runnable Interface구현의 경우 run메서드 구현만 해주면 되고 다른 클래스 상속이 가능하다
