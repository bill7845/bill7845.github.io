---
layout: post
title: Jsp Cookie
comments: true
categories: [Web/Jsp]
tags: [Web,Javascript,Jsp]
---
<br>

# <center> Jsp Cookie </center>

<br>

#### 1. Jsp 쿠키 생성 및 활용

<br>

* 로그인 폼 생성 및 입력받은 데이터 송신

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
<form action="02_LoginService.jsp" method="post"> // 02_LoginService.jsp에 연결 //post 방식으로 전송
사용자: <input name='user' type='text'><br/>
비밀번호: <input name='pass' type='password'><br/>
<input type='submit' value='login'>
</form>

</body>
</html>
```

<br>

* 로그인 확인
* 받아온 데이터와 DB의 값 비교

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
	// 이전화면 폼에서 넘겨받는 값
	String user = request.getParameter("user");
	String pass = request.getParameter("pass");

	// 실제로는 DB에서 가져와야하는 값
	String saveUser = "bill7845";
	String savePass = "3927";

	// user, password가 같을 때 로그인 성공, 그렇지 않으면 로그인 실패
	if( ( user.equals(saveUser) ) && ( pass.equals(savePass) ) ){

		//#############
		// 1. 로그인 성공 시 쿠키생성
		Cookie c = new Cookie("user","bill7845");
		// 2. 쿠키속성 지정 ( 선택 )
		c.setMaxAge(1*60*60);
		// 3. 응답으로 쿠키전송
		response.addCookie(c);    // 쿠키 전송 메서드 addCookie()
%>

	<h2> <%= user %>님, 성공적으로 로그인하셨슴다...</h2>
	<p> <a href="02_MainPage.jsp"> 들어가기 </a>

<%
	} else {

%>

	<h2> 로그인에 실패했슴다...</h2>
	<p> <a href="02_LoginForm.jsp"> 되돌아가기 </a>

<%
	}			
%>

</body>
</html>
```

<br>

* 발생된 쿠키를 얻어오기 (* 배열로 얻어와야함)

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<!DOCTYPE html>
<html>
<head>
<title> 우리 페이지 </title>
</head>
<body>

<%
	String user = null;
	//##########
	// 1. 요청을 통해 전송된 쿠키들을 얻어오기
	Cookie c[] = request.getCookies();
	// 2. 내가 지정한 이름의 쿠키를 찾기
	for(int i=0; c!=null && i <c.length; i++){  // shortcurcuit로직 활용!!
		if((c[i].getName()).equals("user") ){  // 쿠키 발생시 key:user value:bill7845로 지정해둠
      // 3. 해당하는 그 쿠키의 값을 얻어와 변수에 저장
			out.write(c[i].getValue() +"님 접속 중");
			user = c[i].getValue();
		}
	}

	if(user == null){
		response.sendRedirect("02_LoginForm.jsp");
	}

%>

	<h2> 이 페이지는 로그인을 하셔야만 볼 수 있는 페이지 입니다 </h2><br/><br/><br/>
	<%= user %>님, 로그인 중입니다.


</body>
</html>
```
