---
layout: post
title: Basic_Array
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

# Array

* __Array basic__
* __정렬(버블정렬)__
* __동적배열__

## 1. 배열 선언과 초기화
> 배열의 선언
```{.java}
  int []arr = new int[5];  // int타입 배열의 선언  // 배열의 크기는 미리 선언해 두지 않아도 무방
```
```{.java}
  int []arr = new int{1,2,3,4,5}; // 배열의 선언과 초기화를 동시에
```

### 1.1 배열의 크기와 기본값
> 배열의 크기를 선언하고 값을 입력하지 않는것은 문제가 되지 않지만 배열의 크기를 넘어서는 값 입력은 불가능하다
```{.java}
  int []arr2 = new int[5];
  arr2 = {1,2,3,4,5,6}; // int형 5 크기의 배열에 값 6개 입력은 불가능
```

### 1.2 배열을 활용한 기본예제
> 배열을 활용한 성적 합산
> 입력받은 점수를 배열에 저장한 후 합산
> 배열에서 값을 하나씩 꺼내오는 방법
```{.java}
public static void main(String[] args) {

  // 성적 입력, 합산 출력
  // 학생수 입력받음

  int stu = 0;    // 학생수
  String score;   // 입력받은 점수 "/" 토큰으로 구분
  int[] score_arr = new int[3];   // 토큰으로 구분한 점수받음
  int total = 0;  
  Scanner input = new Scanner(System.in);

  System.out.println("학생수 입력 :");
  stu = input.nextInt();

  for (int i = 0; i < stu; i++) {   //입력한 학생수 만큼 반복
    System.out.println("점수 입력 :( / / )");
    score = input.next(); // 입력받은 점수를 score타입으로 전체받음
    StringTokenizer st = new StringTokenizer(score, "/");
    for (int j = 0; st.hasMoreTokens(); j++) {  //token이 false일 경우까지 반복
      score_arr[j] = Integer.parseInt(st.nextToken());
      total += score_arr[j];
    }
    System.out.println("total :" + total);
    System.out.println();
  }

}
```
> __추가__  
> class를 활용한 성적합산 업그레이드

```{.java}
public class Student {

	private String name; // 접근성을 위한 private 지정, setter 생성
	private int kor, eng, math;
	private int total;  
	private double avg;

	public int calTotal() {  //메서드
		total = kor+eng+math;   //전역변수 // setter접근 필요
		return total;
	}

	public double calAverage() {
		avg = (double)total/3;
		return avg;
	}

	// 멤버변수 출력하기 위한 메서드
	public String toString() {
		return name+"학생 총점:" + total + "/평균 :" + avg;
	}

	// setter
	// this.name => this 를 통해 class내의 전역변수 name에 대입된다.
	//=======================================================================================================================


	public void setName(String name) {
		this.name = name;
	}

	public void setKor(int kor) {
		this.kor = kor;
	}

	public void setEng(int eng) {
		this.eng = eng;
	}

	public void setMath(int math) {
		this.math = math;
	}

//end of class
//========================================================================

import java.util.Scanner;
import java.util.StringTokenizer;
public class Main {

	public static void main(String[] args) {

		// 배열 선언 + 객체 생성코드 각각 만들어줘야

		Scanner input = new Scanner(System.in);

		System.out.println("입력할 학생 수: ");
		int insert = input.nextInt();

		Student s[] = new Student[insert]; // 이 코드는 배열을 만든 코드일 뿐 class 객체를 만든것이 아니다. 따라서 객체생성 코드 만들어줘야함.
                                       // Student class 자료형의 배열이다 따라서, Student의 field를 사용한다 ??

		for (int i = 0; i < insert; i++) {
			s[i] = new Student(); // 객체 생성 코드 ******

			System.out.println(i+1 + "번 째 학생의 정보 입력 :(이름/kor/eng/math)");
			String str = input.next(); //여기서 nextLine 해버리면 첫번째 실행시 마지막 엔터값이 다음 실행의 첫번째로 넘어오기 때문에 next
			StringTokenizer st = new StringTokenizer(str,"/");


			while(st.hasMoreTokens()) {
				s[i].setName(st.nextToken());
				int a1 = Integer.parseInt(st.nextToken());
				s[i].setKor(a1);
        // 한줄로 축약 s[i].setKor(Integer.parseInt(st.nextToken());
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

<br>

> 배열에서 가장 큰 값 구하기
> 알고리

```{.java}
public static void main(String[] args) {

  //가장 큰 값 구하기

  int arr[] = new int[] {22,50,50,7,25,35}; //

  int max = arr[0];   // 첫번째 값 기준

  for (int i = 1; i < arr.length; i++) {  // 배열의 크기만큼 반복  //단, 첫번째값이 기준값이므로 두번째 값부터 시작
    if (max <= arr[i]) {  
      max = arr[i];   // 기준값이 그 다음 값보다 작거나 같은 경우 다음 값을 기준값으로 변경
    }
  }System.out.println(max);


}
```

## 2. 정렬(버블정렬)
> 버블정렬 알고리즘을 활용하여 배열값 정렬 시키기
> 동적 배열 활용한 합계 출력
```{.java}
public static void main(String[] args) {

		// 버블정렬

		int arr[] = {22,15,13,7,35,25};

		for(int i=arr.length-1; i>0; i--) {
			for (int j = 0; j < i; j++) {  
				if (arr[j] > arr[j+1]) {
					int temp = arr[j];
					arr[j] = arr[j+1]; // 맞바
					arr[j+1]=temp;  // 꾸기
				}
			}
		}

		for(int i=0; i < arr.length; i++) {
			System.out.print(arr[i]+"/");
		}
	}
```

## 3. 동적배열
> 배열이름.length와 배열이름[i].length의 차이를 구별
>
```{.java}
char[][] star = new char[4][]; // 동적 배열 선언

		// 값 지정
		for (int i = 0; i < star.length; i++) {
			star[i] = new char[i+1]; // 동적배열 star[i]의 크기 지정
			for (int j = 0; j < i+1; j++) { //star[i].length = 4
				star[i][j] = '*';
			}
		}

		// 출력
		for (int i = 0; i < star.length; i++) {
			for (int j = 0; j < star[i].length; j++) {
				System.out.print(star[i][j]);
			}
			System.out.println();
		}

//==============================================================================

// 동적 배열 합계 출력
int a[][] = new int[][] { { 3, -5, 12 }, { -2, 11, 2, -7 }, { 21, -21, -35, -93, -11 }, { 9, 14, 39, -98 } };

		int sum = 0;
		for (int i = 0; i < a.length; i++) {
			for (int j = 0; j < a[i].length; j++) {
				sum+= a[i][j];
			}System.out.println(sum);
		}
```
