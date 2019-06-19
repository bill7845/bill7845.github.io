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

<br>

* Cart.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ page import="java.util.*" %>
<%@ page import="shop.cart.Goods" %>  // java 클래스 import
<%
	String id="";
	String name ="";
	int price=0;

	ArrayList<Goods> glist = null;

	request.setCharacterEncoding("utf-8");

	// 1. Form의 값(hidden값) 넘겨받기 ( id, name, price )
	id = request.getParameter("id");
	name = request.getParameter("name");
	price = Integer.parseInt(request.getParameter("price"));
	// 2. 세션의 cart 속성을 얻어온다.
	Object obj = session.getAttribute("cart");
	// 3. 만일 null이면 ArrayList 객체 새로 생성하고 그렇지 않으면 ArrayList 변수(glist)에 지정
	if(obj == null){ // 아직 구매하기를 누른항목이 없으므로 새로운 리스트 만들어줌
		glist = new ArrayList<Goods>();
	}else{
		glist = (ArrayList<Goods>)obj;  // glist를 ArrayList로 만들어준것????
	}
	// 4. 1번의 값들을 Goods 객체로 생성후 ArrayList 에 추가
	Goods good = new Goods(id,name,price);
	glist.add(good);   // arraylist에 객체가 들어간것.
	// 5. 세션에 cart 라는 이름에 Arrist를 저장
	session.setAttribute("cart",glist);


%>		 

<html>
<body bgcolor=white>
<%= name %> 을 구입하셨습니다.

<br><br><br>

<table>
<tr bgcolor="#e7a068"><th>상품명</th>
<th>가격</th></tr>

<%
		int n = glist.size();
		int sum = 0;
		for(int i=0; i < n; i++) {
			Goods goods = (Goods) glist.get(i);
			int gp = goods.getPrice();
			sum += gp;
%>
			<tr><td align="center"> <%= goods.getName() %> </td>
				<td align="right"> <%= gp %> </td></tr>
<%
		} 		 
%>

<tr bgcolor="#e7a068"><td colspan="2" align="right"> 총액 : <%= sum  %></td></tr>
</table>

<br/><br/>
[<a href="wshop.jsp">쇼핑하러 가기</a>]
[<a href="Buy.jsp">구입하기</a>]

</body>
</html>
```

<br>

* Buy.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ page import="shop.cart.Goods" %>
<%@ page import="java.util.*" %>

<%
	ArrayList<Goods> glist = null;

	request.setCharacterEncoding("utf-8");

	// 1. 세션에서 지정한 cart 속성값을 얻어와서 ArrayList 변수에 지정
	Object obj = session.getAttribute("cart");
	if(obj==null){
		return;
	}else{
    // 2. null 이면 리턴 그렇지 않으면 세션값 얻어오기
		glist=(ArrayList<Goods>)obj;
    // 3. 세션에서 속성을 제거한다
		session.removeAttribute("cart");
	}


%>		 

<html>		
<body bgcolor="white">
<table>
<tr bgcolor="#e7a068"><th>상품명</th>
<th>가격</th></tr>

<%
		int sum = 0;
		int n = glist.size();

		for(int i=0; i < n; i++) {
			Goods goods = (Goods) glist.get(i);
			int gp = goods.getPrice();
			sum += gp;

%>
			<tr><td align="center"> <%= goods.getName() %></td>
				<td align="right"><%= gp %></td>
			</tr>
<%
		} 	
%>
<tr bgcolor="#e7a068"><td colspan="2" align="right"> 총액 :  <%= sum %> </td></tr>
</table>

<br><br><a href="wshop.jsp">다시 쇼핑하기</a>
</body></html>

```
