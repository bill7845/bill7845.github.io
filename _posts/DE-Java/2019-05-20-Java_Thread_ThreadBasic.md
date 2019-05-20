---
layout: post
title: Thread_Basic
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> Thread </center>
---

<br>

* __Thread__


<br>

## 1. Thread

<br>

_직렬적인 프로세스의 처리 순서를 정하지 않고 동시에 실행시켜 "병렬적"으로 실행한다_

> 자바의 쓰레드를 이용하여 하나의 프로세스에서 여러 루틴을 가지고 동시에 실행 할 수 있다

<br>

### 1.1 Thread 클래스의 상속

<br>

> Thread 클래스를 상속받아 Thread를 구현하는 방법
> run()메서드를 오버라이딩하여 main에서 start()메서드 통해 구현

```java
public class Ex2_ThreadTest {

	public static void main(String[] args) {

		MakeCar1 mc1 = new MakeCar1("차틀 만들기");
//		mc1.run();
		mc1.start(); // start() 호출 -> run() 호출됨

		MakeCar1 mc2 = new MakeCar1("도색");
//		mc2.run();
		mc2.start();

		System.out.println("프로그램 끝");
	}

}

class MakeCar1 extends Thread{	// Thread 클래스 상속

  String work;

	public MakeCar1(String work){  // 생성자
		this.work = work;
	}

	public void run() {	// run메서드 오버라이딩
		for(int i=0; i<5; i++) {
			System.out.println(work +"작업중");

			try {	// 눈으로 확인하기 위해서
				Thread.sleep(500);  // 5초내로 끝냄
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
}
```

<br>

#### 1.1.1 Thread Join

<br>

> 쓰레드 조인을 이용하여 메인메서드에서 실행시킨 쓰레드가 종료되기 전에 메인메서드가 종료되는 것을 막을 수 있다
> 실행시킨 쓰레드가 동작이 끝날 때 까지 기다린다

```java
import java.util.ArrayList;
import java.util.Random;
public class ThreadTest extends Thread {
	// index 변수를 추가해서 스레드가 동작시에 해당 변수를 증가시키도록 할겁니다.
	private static int index = 0;

	private int id = -1;
	public ThreadTest(int id){
		this.id = id;
	}
	public void run(){
		System.out.println( id + "번 쓰레드 동작 중..." );
		Random r = new Random(System.currentTimeMillis());
		try {
			long s = r.nextInt(3000); // 3초내로 끝내자.
			Thread.sleep(s); // 쓰레드를 잠시 멈춤
			index++; // index 변수를 증가시킵니다.
		} catch (InterruptedException e) {
			e.printStackTrace();
		}

		System.out.println( id + "번 쓰레드 동작 종료..." );
	}

	public static void main(String[] args) {

		System.out.println("Start main method.");

		ArrayList<Thread> threadList = new ArrayList<Thread>();

		for(int i = 0 ; i < 10 ; i++ ){
			ThreadTest test = new ThreadTest(i);

			test.start(); // 이 메소드를 실행하면 Thread 내의 run()을 수행한다.
			threadList.add(test); // 생성한 쓰레드를 리스트에 삽입
		}

		for(int i = 0 ; i < threadList.size(); i++){
			try {
				threadList.get(i).join(); // 쓰레드의 처리가 끝날때까지 기다립니다.
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}

		System.out.println("current Index: "+ index); // index의 값을 반환합니다.
		System.out.println("End main method.");
	}
}

// 코드출처 : https://jdm.kr/blog/69
```

<br>

#### 1.1.2 Thread Synchronized

<br>

> 쓰레드 간의 공통으로 사용하는 객체를 동기화하는방법
> 동기화된 객체는 쓰레드간의 동시접근이 불가능하다
> synchronized => lock

```java
import java.util.ArrayList;
import java.util.Random;
public class ThreadTest extends Thread {

	private static int index = 0;

	private int id = -1;
	public ThreadTest(int id){
		this.id = id;
	}
	public void run(){
		System.out.println( id + "번 쓰레드 동작 중..." );
		Random r = new Random(System.currentTimeMillis());
		try {
			long s = r.nextInt(3000); // 3초내로 끝내자.
			Thread.sleep(s); // 쓰레드를 잠시 멈춤
			setIndex();  // 메서드 추가
		} catch (InterruptedException e) {
			e.printStackTrace();
		}

		System.out.println( id + "번 쓰레드 동작 종료..." );
	}

	public synchronized static void setIndex(){  // 쓰레드간의 객체 동기화 위한 synchronized method
		index++; // index 변수를 증가시킵니다.
	}

	public static void main(String[] args) {

		System.out.println("Start main method.");

		ArrayList<Thread> threadList = new ArrayList<Thread>();

		for(int i = 0 ; i < 10 ; i++ ){
			ThreadTest test = new ThreadTest(i);

			test.start(); // 이 메소드를 실행하면 Thread 내의 run()을 수행한다.
			threadList.add(test); // 생성한 쓰레드를 리스트에 삽입
		}

		for(int i = 0 ; i < threadList.size(); i++){
			try {
				threadList.get(i).join(); // 쓰레드의 처리가 끝날때까지 기다립니다.
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}

		System.out.println("current Index: "+ index); // index의 값을 반환합니다.
		System.out.println("End main method.");
	}
}

//코드출처 https://jdm.kr/blog/69
```

<br>

```java
class Count {

	int i;

	synchronized void increment() {	// 첫번째 쓰레드가 접근해서 첫번째 작업을 끝낼때까지 다른 쓰레드가 접근 못함
		i++;
	}

	/* void increment(){	// 메서드의 내용이 길 경우 synchronized를 위에처럼 붙여버리면 너무 느려짐 따라서 필요한 부분에만 synchronized 붙일수 있음
	 * 	synchronized(this){ // 단, 공유할 객체를 물고 들어가야함 없으면 자기자신(this)
	 * 		i++;
	 * 	}
	 *}
	 */

}

class ThreadCount extends Thread{
	Count cnt;

	public ThreadCount(Count cnt) {  // 생성자
		this.cnt = cnt;
	}

	public void run() {  // run 오버라이딩
		for(int i=0; i<100000000; i++) {
			cnt.increment();
		}
	}
}

public class Ex7_Synch {

	public static void main(String[] args) {
		Count cnt = new Count();

		ThreadCount tc1 = new ThreadCount(cnt);
		tc1.start();

		ThreadCount tc2 = new ThreadCount(cnt);
		tc2.start();

		// join() 통해서 쓰레드가 끝날때가지 기다림		// 이 경우 i를 서로 공유하고 있으므로 원하는 결과 안나옴 따라서 자원공유하면서 쓰레드 하기위해서는-> i에 lock걸어줘야 함	//
		try {
			tc1.join();	// tc1이 끝날때까지 메인 못끝내게
			tc2.join();
		} catch (InterruptedException e) {
			e.printStackTrace();
		}

		System.out.println("i값 =="+cnt.i);
	}

}
```
