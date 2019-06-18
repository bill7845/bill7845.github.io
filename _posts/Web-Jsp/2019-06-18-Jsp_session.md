---
layout: post
title: Jsp Session
comments: true
categories: [Web/Jsp]
tags: [Web,Javascript,Jsp]
---
<br>

# <center> Jsp Session </center>

<br>

#### 1. Session 생성 및 활용

<br>

* loginForm.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<!DOCTYPE html>
<html>
<head>
<title> 로그인창 </title>
</head>
<body>

<h3>로그인 확인하기 </h3>
<form action="LoginService.jsp" method="get">
사용자: <input name='User' type='text'><br/>
비밀번호: <input name='Pass' type='password'><br/>
<input type='submit' value='login'>
</form>

</body>
</html>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<!DOCTYPE html>
<html>
<head>
<title> 로그인창 </title>
</head>
<body>

<h3>로그인 확인하기 </h3>
<form action="LoginService.jsp" method="get">
사용자: <input name='User' type='text'><br/>
비밀번호: <input name='Pass' type='password'><br/>
<input type='submit' value='login'>
</form>

</body>
</html>
```

<br>

* LoginService.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<!DOCTYPE html>
<html>
<head>
<title> 로그인확인 </title>
</head>
<body>
<%

	// 실제로는 DB에서 가져와야하는 값
	String saveUser = "bill7845";
	String savePass = "3927";

	// 이전화면 폼에서 넘겨받는 값
	String user = request.getParameter("User");
	String pass = request.getParameter("Pass");

	// user, password가 같을 때 로그인 성공, 그렇지 않으면 로그인 실패
	if( ( user.equals(saveUser) ) && ( pass.equals(savePass) ) ){
		// #2. 세션에 "id"라는 이름에 변수 user 값을 저장
		session.setAttribute("id", user);  	/*user변수의 값 가져오기 */		/*session은 obj형태로 값을 가져옴  */
                                        // session 생성 메서드 setAttribute(key,value)
		// #1. 로그인 성공하면 바로 MainPage.jsp를 요청
		response.sendRedirect("MainPage.jsp");
	} else {

		// #1. 로그인에 실패하면 바로 LoginForm.jsp을 요청
		response.sendRedirect("LoginForm.jsp");
	}			
%>

</body>
</html>
```

<br>

* MainPage.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%


  //# 1."id"로 저장된 세션값을 얻어온다.
	Object obj = session.getAttribute("id");	/*session은 obj형태로 가져옴  */

  //# 2. 값이 null이라면 LoginForm.jsp로 페이지 이동
	if(obj==null){
		response.sendRedirect("LoginForm.jsp");
		return;
	}

  //# 3. null이 아니라면 String 형변환하여 변수에 지정
	String user = (String)obj;	/* 캐스팅 필요  */

%>

<!DOCTYPE html>
<html>
<head>
<title> 우리 페이지 </title>
</head>
<body>
	<h2> 이 페이지는 로그인을 하셔야만 볼 수 있는 페이지 입니다 </h2><br/><br/><br/>
	<%=user %>님, 로그인 중입니다.

</body>
</html>
```

<br>

#### 2. 세션 활용 장바구니

<br>

* wshop.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<html><head><title>우리 쇼핑 몰</title></head>
<body>
<h2>쇼핑 몰</h2>

<h3>가전 제품</h3>
<ul>
<li><a href='tv-samsung-1020.jsp'>삼성 R14 텔레비젼</a> </li>
<li><a href='ref-lg-2072.jsp'>LG 냉장고</a> </li>
</ul>
</body>
</html>
```

<br>

* ref-lg-2072.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<html>
<head><title>우리 쇼핑몰 </title></head>
<body>

<table><tr><td><img src='imgs/2072.gif' width='180'>

</td><td>

문을 자주 열어도, 음식을 많이 채워도,
역시 LG 싱싱특급~
- 용량 : 500L (냉장 : 360L, 냉동 : 140L)
- 신감각 가죽 무늬
- 더욱 효율적인 내부 공간
- 얼듯 말듯 싱싱고
- 유러피안 아치 디자인
- 레일 부착 분리형 생생 야채실
- CFC-FREE 환경 친화 설계
- 안전 강화 유리 선반
- 광촉매 파워 탈취
- 인체 공학적 설계
- 방음 보강으로 저소음 설계
- 초절전 설계
- 360。 이동용 회전 바퀴
- 색상 : 진미색
- 에너지 소비 효율 : 1등급
- 소비 전력 : 55 kwh/월
- 크기 : 831 x 1,785 x 699mm

</table>

663,600 원
<form action='Cart.jsp' method='post'>
<input type='hidden' name='id' value="2072">
<input type='hidden' name='name' value="LG 냉장고 R-B50CF">
<input type='hidden' name='price' value="663600">
<input type='submit' value="장바구니">
</form>
</body>
```

<br>

* tv-samsung-1020.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<html>
<head><title> 우리 쇼핑몰 </title></head>
<body>

<table><tr><td><img src='imgs/1020.jpg' width='180'>

</td><td>
^^상품설명^^
*14" 화면 명품 플러스
*절약형 절전 TV
*Dual스피커 채용의 고감각 디자인
(측면Ear Type)  
*초절전 버튼(대기 소비 전력 Zero)
*A/V 입력 단자: 후1
*다기능 간단 리모컨(VTR 조작기능)  
*크기: 380 X 325 X 381(mm)
</td></tr></table>

<pre>
[[ 특징 ]]
*절전 스위치를 내장한 초절전 TV:  
대기 소비전력을 0으로 낮추어서 TV 평균 사용 기간인
7년이 지나면 14인치 TV 1대를 구입할 수 있는 금액을
아낄 수 있습니다.  
(1일 6시간 시청기준, 월 500KW이상 사용 가정의 경우)  
(본 제품은 에너지 절약마크 획득 제품입니다 )  

*고감각 디자인:  
DUAL 스피커를 채용한 미려한 디자인으로 어디서나 잘
어울리는 고감각 디자인 제품입니다.  

*다기능 간단 리모컨 채용:  
TV와 VTR을 겸용으로 사용할수 있는 인체공학적 간단 리모컨을
채용하고 있습니다.


</pre>
147,000 원
<form method='post' action='Cart.jsp'>
<input type='hidden' name='id' value="1020">
<input type='hidden' name='name' value="삼성 TV CT 14R1">
<input type='hidden' name='price' value="147000">
<input type='submit' value="장바구니">
</form>

</body>
</html>

```
