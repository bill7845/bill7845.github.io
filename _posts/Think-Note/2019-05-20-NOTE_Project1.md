---
layout: post
title: 플레이데이터 팀프로젝트1
comments: true
categories: [Think/Note]
tags: [Project]
---
<br>

# <center> Pos 시스템 구축 팀프로젝트 </center>
---

<br>

## 1. 프로젝트 개요 및 사용자 요구사항

<br>

#### 1.1 목적
<p> POS(Point-of-Sale) 시스템을 구축하여 효율적 매출관리를 지원하며, 고객 경험을 개선하고 비즈니스 운영을 간소화 </p>

<br>

#### 1.2 사용자

> 종업원, 관리자

<br>

## 2. 기능

* 판매
* 매출관리
* 재고관리

<br>

## 3. DB모델 설계

![Alt text](/assets/img/erd.png)

<br>

#### 3.1 기능구현
> 관리자/종업원 로그인 구현 <br>
> 로그인 결과에 따라 관리자/종업원(재고,매출 탭 안보이게) <br>
> 매출관리는 판매 결과에 따라 DB에서 SQL문으로 결과만 출력 <br>

<br>

## 4. 구현 화면 & 코드

<br>

#### 4.1 판매탭 버튼별 기능

```java

// String ame = "0001";
// String latte = "0002";
// String moca = "0003";
// String lemon = "0004";
// String bagel = "0005";
// String milk = "0006";
// String cake = "0007";
// String water = "0008";
// String beer = "0009";

// ArrayList list = new ArrayList() ;  // 제품버튼 클릭시 제품 고유번호(String)를 받는 ArrayList

public void actionPerformed(ActionEvent ev) {	// 액션 리스너
  if (ev.getSource() == bAmericano) {
    list.add(ame);  // 버튼 클릭시 해당 제품 고유번호 list에 추가
    p_List(ame);  
  }else if(ev.getSource() == bCafelatte) {
    list.add(latte);  // 버튼 클릭시 해당 제품 고유번호 list에 추가
    p_List(latte);
  }else if(ev.getSource() == bCafemoca) {
    list.add(moca); // 버튼 클릭시 해당 제품 고유번호 list에 추가
    p_List(moca);
  }else if(ev.getSource() == bLemonade) {
    list.add(lemon);  // 버튼 클릭시 해당 제품 고유번호 list에 추가
    p_List(lemon);
  }else if(ev.getSource() == bBagel) {
    list.add(bagel);  // 버튼 클릭시 해당 제품 고유번호 list에 추가
    p_List(bagel);
  }else if(ev.getSource() == bMilk) {
    list.add(milk); // 버튼 클릭시 해당 제품 고유번호 list에 추가
    p_List(milk);
  }else if(ev.getSource() == bCake) {
    list.add(cake); // 버튼 클릭시 해당 제품 고유번호 list에 추가
    p_List(cake);
  }else if(ev.getSource() == bWater) {
    list.add(water);  // 버튼 클릭시 해당 제품 고유번호 list에 추가
    p_List(water);
  }else if(ev.getSource() == bBeer) {
    list.add(beer); // 버튼 클릭시 해당 제품 고유번호 list에 추가
    p_List(beer);			
  }else if(ev.getSource() == bPayment) {  // 결제버튼 클릭시 작동
    int i = JOptionPane.showConfirmDialog(null, "적립 하십니까?");  // showConfirmDialog로 예/아니오( int 0 or 1) 값 받기
    if (i == 0) { // "예" 선택시
      String memberNum = JOptionPane.showInputDialog(null,"회원번호를 입력 하세요");  // 회원번호(String)값 입력받기
      MemberNum(memberNum);	// 회원번호 입력 메서드 실행
      Payment(); // 결제 메서드 실행
      JOptionPane.showMessageDialog(null, "결제 진행합니다..1");
      JOptionPane.showMessageDialog(null, "결제완료");
    } else if (i == 1) {  // "아니오" 선택시
      Payment();  // 결제 메서드 실행
      JOptionPane.showMessageDialog(null, "결제 진행합니다..2");
      JOptionPane.showMessageDialog(null, "결제완료");

    }
  }
}

```

<br>

#### 4.2 판매탭 기능별 method 구현

<br>

* 비회원 결제 메서드

```java
public void InsertPayment1(ArrayList payment) throws Exception {  //판매탭에서 입력받은 제품 고유번호를 인자로

  Connection con = DriverManager.getConnection(url, user, pass);  // oracle 연결 객체 생성
  PreparedStatement st2 = null; // 연결통로

  for (int i = 0; i < payment.size(); i++) {  // ArrayList에 담겨있는 제품의 개수 만큼 반복문 실행
      String sql2 ="INSERT INTO SELL  (SELLNO, ENO, PNO, SELLCOUNT, SELLDATE)   VALUES  (SEQ_SELLNO.nextval,'A1111',   '"+payment.get(i)+"'  , 1, sysdate)"  ;    // 받아온 제품리스트를 제품 고유번호에 따라 연결된 DB에 입력하는 sql문장
      st2 = con.prepareStatement(sql2);

      st2.executeUpdate();  // 연결 실행
    }
  con.commit();
  st2.close();
  con.close();
}
```

<br>

* 회원번호 method

```java
// 받아온 회원번호를 판매모델의 전역변수로 설정해줌

String memberNum;

public void InsertMemberNum(String memberNum) throws Exception {
  this.memberNum = memberNum;
}
```

<br>

* 회원결제 method

```java

public void InsertPayment(ArrayList payment) throws Exception { //판매탭에서 입력받은 제품 고유번호를 인자로

		Connection con = DriverManager.getConnection(url, user, pass);
		PreparedStatement st2 = null;
		PreparedStatement st3 = null;
		PreparedStatement st4 = null;

    // Sell 테이블 sql
		for (int i = 0; i < payment.size(); i++) {  // ArrayList에 담겨있는 제품의 개수 만큼 반복문 실행
				String sql2 ="INSERT INTO SELL  (SELLNO, CNO , ENO, PNO, SELLCOUNT, SELLDATE)   VALUES  (SEQ_SELLNO.nextval, ?, 'A1111',   '"+payment.get(i)+"'  , 1, sysdate)"  ;  // 받아온 제품리스트를 제품 고유번호에 따라 연결된 DB에 입력하는 sql문장

				st2 = con.prepareStatement(sql2);
				st2.setString(1,memberNum); // 1번째 ?에 회원번호(전역변수로 설정 된 회원번호) 입력

				st2.executeUpdate();  
				st2.close();

        // 마일리지 sql
        // 회원가입되어있는 CUSTOMER테이블의 고객 마일리지 업데이트
				String sql3 = "UPDATE CUSTOMER SET CSTAMP = (select * from (SELECT (sum(P.PPRICE *0.05) over(partition by CNO)) MILIEGE FROM PRODUCT P, SELL S WHERE (P.PNO = S.PNO) AND CNO = ?)where rownum = 1) WHERE CNO = ?";

				st3 = con.prepareStatement(sql3);

				st3.setString(1, memberNum);  // 1번째 ?에 회원번호(전역변수로 설정 된 회원번호) 입력
				st3.setString(2, memberNum);  // 2번째 ?에 회원번호(전역변수로 설정 된 회원번호) 입력

				st3.executeUpdate();
				st3.close();

			// 원재료sql
      // 판매 제품에 따라 해당 제품의 원재료 차감
				String sql4 = "UPDATE ORIGINAL SET OCOUNT= OCOUNT-1 WHERE ONO = (SELECT O.ONO FROM PRODUCT P , ORIGINAL O WHERE (P.ONO = O.ONO) AND PNO = '"+payment.get(i)+"')";

				st4 = con.prepareStatement(sql4);

				st4.executeUpdate();
				st4.close();
			}
		con.commit();
		con.close();
	}
```

<br>

* 판매탭 화면목록 출력 method

```java
public ArrayList PaymentList(String pno) throws Exception { //

  con = DriverManager.getConnection(url, user, pass);
  PreparedStatement st = null;
  ResultSet rs = null;

  // 판매탭에서 입력 받아 온 제품 고유번호에 맞게 DB에서 정보를 Select
  String sql = "SELECT PNO pno, PNAME pname,  PPRICE price FROM PRODUCT WHERE PNO = ? "  ;

  ArrayList data = new ArrayList(); // select해온 정보를 입력받을 ArrayList data 생성
  st = con.prepareStatement(sql);
  st.setString(1, pno); // sql문의 1번째 ?에 판매탭에서 입력받아온 제품고유번호 입력
  rs = st.executeQuery();

  if(rs.next()) { // data에 제품번혼,제품이름,가격을 차례로 입력받음
    data.add(rs.getString("pno"));  
    data.add(rs.getString("pname"));
    data.add(rs.getInt("price"));
  }

  rs.close();
  st.close();
  con.close();
  return data;
}
```
