---
layout: post
title: Basic_예외처리
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

<br>

# <center> try catch 예외처리 </center>
---

<br>

* __오류와 예외__
* __Try Catch__

<br>

## 1 에러와 예외

<br>

> error => 심각한 오류
> except => 심각하지 않은 오류

```java
	try{
		//예외 발생 구문
	}catch(){
	 	//예외가 발생한 후의 구문
	}finally{
	 	// 예외 발생 여부 상관없이  무조건 실행 구문
		}
```

<br>

_사용예시_

```java
String str[]= {"맛점","우산","즐거운 화요일"};

		try{
			for(int i=0; i <str.length+1; i++) {
				System.out.println(str[i]);
				}
		System.out.println("예외가 발생할 여지가 있는 구문");
		return; 	// return을 사용해도 finally는 출력
		}catch (Exception ex) {
			System.out.println("예외 발생"+ ex.getMessage()); // or ex.toString
			ex.printStackTrace();
		}finally {
			System.out.println("무조건 실행 구문");
		} // connecton 닫는 부분
		System.out.println("프로그램 정상 종료");
		}
```

<br>

## 2. 범용 예외 처리

<br>

```java
// java에서는 외부프로그램 시 무조건 예외처리

		FileInputStream  fis = null; //변수 선언 바깥에서

		try {
			fis = new FileInputStream("abc.txt");
			System.out.println("파일 연결");
			fis.read(); //

		} catch (FileNotFoundException e) { // 범용적인 예외처리 구문 Exception e // or 구체적 상황에 따른 예외 처리
			System.out.println("파일 없는 예외 :"+e.getMessage());

		} catch (IOException e) {
			System.out.println("입출력 예외:" + e.getMessage());

		} catch(Exception e) { // 범용예외처리 // 범용예외처리 구문은 맨 마지막에 넣어줘야 한다
			System.out.println("그 외 예외처리");

		}finally { //닫아주는 과정 // finally 구문에 있는 문장들은 예외여부와 상관없이 무조건 실행하는데 대표적으로 파일스트림, 네트워크 스트림, 디비의 커넥션 등을 닫을 때 사용한다
			try{ fis.close(); } catch (Exception ex) {}
		}
	}
```

<br>

## 3. throws Exception

<br>

>메서드의 예외를 메인으로 반환

```java
//		readFile(); //메서드만 호출할 경우 메서드에서 발생한 예외 처리 못해서 아래처럼 try/catch 해줌

		try{
			readFile();
			System.out.println("파일 처리");
		}catch (Exception ex) {
			System.out.println("예외 발생");
		}
	}

	// 메소드 내에서 예외가 발생한 경우 메소드 뿐만 아니라 main에서의 메소드 실행까지 정상 처리가 되지 않는다 이에 물론 메소드 내부에서 예외처리를 할 수 있지만,
	// 해당 메소드가 main으로 값을 반환할 경우  메인에서는 예외처리가 되어있지 않기 때문에

	static void readFile() throws Exception  { // 예외를 메서드를 호출한곳으로 반환한다
		FileInputStream fis = new FileInputStream("xxx.txt");
		System.out.println("파일연결");


//====================================================================================================

//
try {
  readArray();
} catch (Exception ex) {
  System.out.println("예외 발생:" + ex.getMessage());
}
System.out.println("정상종료");

} // end of main

// 오류가 어떤 부분에서 발생하였는지 명확히 파악하기 위해

static void readArray() throws Exception  { //여기 throws 에는 s붙음
String str[] = {"우리는 한 배","공부","자격증공부"};
try {
for(int i=0; i<=str.length; i++) {
  System.out.println(str[i]);
}
}catch(Exception ex) { // 예외처리해준 후,
  throw new MyException(); //throw 통해 예외를 일부로 발생시킨다. 발생 된 예외는 throws에 의해 main으로 넘어간다. 그 후 main에서 해당 예외를 catch // 여기서는 s안붙음
}
}
	}

//====================================================================================

// 예외를 따로 class화 시킴
public class MyException extends Exception { // extends Exception => Exception이라는 class를 상속한다.

	//예외 만들기


	public String getMessage(){
		return "우리가 자주 실수하는 예외";
	}
}
```
