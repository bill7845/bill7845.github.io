---
layout: post
title: oop_다형성
comments: true
categories: [Development Environment/Java]
tags: [Java]
---
<br>

# <center> 다형성 </center>
---

<br>

* __다형성__
* __다형성 활용__

<br>

## 1. 다형성이란?

<br>

> 다형성이란 같은 자료형에 여러가지 객체를 대입하여 다양한 결과를 얻는것을 말한다
> 즉, 하나의 자료형(타입)으로 여려 결과를 얻어낼 수 있고 이는 "객체의 부품화"를 만들 수 있다
> 상속,인터페이스 구현,업캐스팅,오버라이딩을 통해 다형성을 구현한다

```java
import java.util.Scanner;

interface OverWatch { // 인터페이스  => 인터페이스의 모든 메서드는 abstract => 반드시 오버라이딩(재정의)
	void name(); // 추상 메소드
	void lClick(); // 추상 메소드
	void rClick(); // 추상 메소드
	void shiftButton(); // 추상 메소드
	void eButton(); // 추상 메소드
	void qButton(); // 추상 메소드
}

class Mei implements OverWatch { // 인터페이스 구현 클래스
	public void name() { // 오버라이딩
		System.out.println("이름 : 메이");
	}
	public void lClick() { // 오버라이딩
		System.out.println("좌클릭 : 냉각총");
	}
	public void rClick() { // 오버라이딩
		System.out.println("우클릭 : 고드름 투사체");
	}
	public void shiftButton() { // 오버라이딩
		System.out.println("shift : 급속 빙결");
	}
	public void eButton() { // 오버라이딩
		System.out.println("e : 빙벽");
	}
	public void qButton() { // 오버라이딩
		System.out.println("q : 눈보라(궁극기)");
	}
}

class Reaper implements OverWatch { // 인터페이스 구현 클래스
	public void name() { // 오버라이딩
		System.out.println("이름 : 리퍼");
	}
	public void lClick() { // 오버라이딩
		System.out.println("좌클릭 : 헬파이어 샷건");
	}
	public void rClick() { // 오버라이딩
		System.out.println("우클릭 : 없음");
	}
	public void shiftButton() { // 오버라이딩
		System.out.println("shift : 망령화");
	}
	public void eButton() { // 오버라이딩
		System.out.println("e : 그림자 밟기");
	}
	public void qButton() { // 오버라이딩
		System.out.println("q : 죽음의 꽃(궁극기)");
	}
}

class Mccree implements OverWatch { // 인터페이스 구현 클래스
	public void name() { // 오버라이딩
		System.out.println("이름 : 맥크리");
	}
	public void lClick() { // 오버라이딩
		System.out.println("좌클릭 : 피스키퍼");
	}
	public void rClick() { // 오버라이딩
		System.out.println("우클릭 : 모든 총알 발사");
	}
	public void shiftButton() { // 오버라이딩
		System.out.println("shift : 구르기");
	}
	public void eButton() { // 오버라이딩
		System.out.println("e : 섬광탄");
	}
	public void qButton() { // 오버라이딩
		System.out.println("q : 황야의 무법자(궁극기)");
	}
}

public class PolymorphismEx01 {
	public static void main(String[] args) { // main 메소드
		OverWatch ow; // 인터페이스 객체 선언
		System.out.println("플레이할 캐릭터 번호 선택(1. 메이, 2. 리퍼, 3. 맥크리)");
		Scanner sc = new Scanner(System.in); // 스캐너 객체
		int n = sc.nextInt();
		if(n==1){
			ow = new Mei(); // 업캐스팅
		}else if(n==2){
			ow = new Reaper(); // 업캐스팅
		}else{
			ow = new Mccree(); // 업캐스팅
		}
// 선택한 조건에 따라서 부모 객체로 자식 메소드 사용(하나의 타입으로 다양한 결과를 얻어냄 / 다형성)
		ow.name();
		ow.lClick();
		ow.rClick();
		ow.shiftButton();
		ow.eButton();
		ow.qButton();
	}
}

// [출처] [JAVA/자바] 다형성(polymorphism)의 개념/의미/예제|작성자 JOKER
```
