---
layout: post
title: [basic] 클래스를이용한 계산기/class배열
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

# class를 이용한 계산기 / class 배열

* __class를 이용한 캡슐화__
* __private 멤버변수 접근법__
* __do~while 활용__
* __배열을 활용한 클래스__

## 1. Class 1
### 1.1 class 설계
> 접근성 설정 위해 class 멤버변수는 private로 설정
> private로 설정된 멤버변수에 접근하기 위한 settter 메서드
> 계산기의 각 기능을 하는 메서드들
```{.java}
public class CalculatorTest {


	private int num1;
	private int num2;
	private int result;

	// num1,2 result는 멤버변수 따라서 아래 메서드들에서 따로 받아오는값 입력해주지 않아도 됨 (e_method Ex02_인자와반환4 참고)

	public int getAddition() {
		result = num1 + num2;
		return result;
	}

	public int getSubtraction() {
		result = num1 - num2;
		return result;
	}

	public int getMultiplication() {
		result = num1 * num2;
		return result;
	}

	public double getDivision() {
		result = num1/num2;  //casting
		return result;
	}


	//=================================================================================================================
	// setter
	public void setNum1(int num1) {
		this.num1 = num1;
	}

	public void setNum2(int num2) {
		this.num2 = num2;
	}

	//=================================================================================================================
	// getter

	public int getNum1() {
		return num1;
	}

	public int getNum2() {
		return num2;
	}
```



### 1.2  main code
> do~while문 활용

```{.java}
import java.util.*;
public class CalculatorTest_Main {

	public static void main(String[] args) {


		CalculatorTest cal = new CalculatorTest();   // cal이라는 변수명을 가진 CalculatorTest클래 객체 선언
		char contin;
		do {
		Scanner input = new Scanner(System.in);

		System.out.println("숫자 입력 :");
		int input_1 = input.nextInt();
		cal.setNum1(input_1);     //

		System.out.println("숫자 입력 :");
		int input_2 = input.nextInt();
		cal.setNum2(input_2);   // class의 private변수에 접근하기 위한 setter메서드 호출

    // class내부에 선언되어진 계산기능 메서드 호출
		System.out.println("덧셈 : "+cal.getAddition());  
		System.out.println("뻴셈 : "+cal.getSubtraction());
		System.out.println("곱셈 : "+cal.getMultiplication());
		System.out.println("나눗셈 : "+cal.getDivision());

		System.out.println("계속 하시겠습니까? : Y/N");
		System.out.println();

		Scanner input_contin = new Scanner(System.in);
		contin = input_contin.nextLine().charAt(0);
		}while ( contin == 'Y' | contin =='y');
```

<br>

## 2. 배열을 활용한 class
> 배열선언과 클래스 객체 선언을 각각 해줘야함에 주의
> 만약, 반복문에 의해 만들어진 s[0],[s1],[s2]의 값을 계속 저장하고 싶다면?
```{.java}
public class Main {

	public static void main(String[] args) {

		// 배열 선언 + 객체 생성코드 각각 만들어줘야

		Scanner input = new Scanner(System.in);

		System.out.println("입력할 학생 수: ");
		int insert = input.nextInt();

		Student s[] = new Student[insert]; // 이 코드는 배열을 만든 코드일 뿐 class 객체를 만든것이 아니다. 따라서 객체생성 코드 만들어줘야함.

		for (int i = 0; i < insert; i++) {
			s[i] = new Student(); // 객체 생성 코드
														// s라는 클래스객체에 new Student 생성자에 의해 s[0],s[1],s[2]...의 값들이 하나씩 class method에 의해 정의됨

			System.out.println(i+1 + "번 째 학생의 정보 입력 :(이름/kor/eng/math)");
			String str = input.next(); //여기서 nextLine 해버리면 첫번째 실행시 마지막 엔터값이 다음 실행의 첫번째로 넘어오기 때문에 next
			StringTokenizer st = new StringTokenizer(str,"/");


			while(st.hasMoreTokens()) {
				s[i].setName(st.nextToken());
				int a1 = Integer.parseInt(st.nextToken());
				s[i].setKor(a1);
				int a2 = Integer.parseInt(st.nextToken());
				s[i].setEng(a2);
				int a3 = Integer.parseInt(st.nextToken());
				s[i].setMath(a3);
			}

			s[i].calTotal();
			s[i].calAverage();

		}

		for (int i=0; i<insert; i++) {
			System.out.println(s[i].toString());
		}
	}
```
