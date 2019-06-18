---
layout: post
title: Jsp DB Connection
comments: true
categories: [Web/Jsp]
tags: [Web,Javascript,Jsp]
---
<br>

# <center> Jsp DB connect </center>

<br>

#### Jsp DB 연결

<br>

* 기본 폼

```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8" />
  <title> 회원가입 </title>

  <link rel="stylesheet" href="css/base.css" type="text/css" media="screen"  />  
  <link rel="stylesheet" href="css/form.css" type="text/css" media="screen"  />  
 <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<!--   <script src="../../lib/jquery-3.4.1.min.js" type="text/javascript" charset="utf-8"></script> -->
  <script src="./js/jquery.validate.js" type="text/javascript" charset="utf-8"></script>
  <script src="./js/scripts.js"type="text/javascript" ></script>

</head>
<body>
  <div id="container">
    <div id="content">
      <div id="signup">
        <h2>회원 가입</h2>
        <form action="member.jsp">   // member.jsp와 연결
          <div>
            <label for="name">이름:</label>
            <input name="name" id="name" type="text"/>
          </div>
          <div>
            <label for="email">이메일:</label>
            <input name="email" id="email" type="text"/>
          </div>
          <div>
            <label for="website">웹사이트 URL:</label>
            <input name="website" id="website" type="text"/>
          </div>
          <div>
            <label for="password">암호:</label>
            <input name="password" id="password" type="password" />
          </div>
          <div>
            <label for="passconf">암호 확인:</label>
            <input name="passconf" id="passconf" type="password" />
          </div>

		<div class="stats">
          <h2 class="title"> 모든 항목에 동의해야 합니다. </h2>
          <input class='agree' name="agree" type="checkbox"/>(가)조항<br/>
          <input class='agree' name="agree" type="checkbox"/>(나)조항<br />
          <input class='agree' name="agree" type="checkbox"/>(다)조항<br />
          <input class='agree' name="agree" type="checkbox"/>(라)조항<br />
          <input class='agree' name="agree" type="checkbox"/>(마)조항<br />
          <hr/>
          <input class="check-all" name="agree" type="checkbox" /><span>위 조항 모두</span>
          <br/>				
        </div>

        <div>
           <input type="submit" value="보내기" />
        </div>


		</form>
      </div>

    </div>

 </div>
</body>
</html>
```

<br/>

* member.jsp

```javascript
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.Connection"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%
	request.setCharacterEncoding("utf-8");

	String name = request.getParameter("name");
	String email = request.getParameter("email");
	String website = request.getParameter("website");
	String password = request.getParameter("password");

	// 1. 드라이버 로딩
	String driver = "oracle.jdbc.driver.OracleDriver";
	String url = "jdbc:oracle:thin:@192.168.0.216:1521:orcl";
	String user = "KIHYUK";
	String pass = "3927";

	Connection con = null;
	PreparedStatement st = null;

	Class.forName(driver);

	//2. 연결객체 얻어오기
	con = DriverManager.getConnection(url,user,pass);

	// 3. sql 문장 만들기
	String sql = "INSERT INTO MEM(name,email,url,pass) VALUES(?,?,?,?)";
	// 4. 전송 객체 얻어오기
	st = con.prepareStatement(sql);
	st.setString(1,name);
	st.setString(2,email);
	st.setString(3,website);
	st.setString(4,password);
	st.executeUpdate();

%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

<h2>정보 수정</h2>

        <form action="Updatemember.jsp">  // Updatemember.jsp와 연결

          <div>
            <label for="name">이름:</label>
            <input name="name" id="name" type="text" value="<%=name %>"/>
          </div>
          <div>
            <label for="email">이메일:</label>
            <input name="email" id="email" type="text" value ="<%=email %>" readonly/>
          </div>
          <div>
            <label for="website">웹사이트 URL:</label>
            <input name="website" id="website" type="text" value="<%=website %>"/>
          </div>
          <div>
           <input type="submit" value="수정하기" />
       	  </div>

		</form>

</body>
</html>
```

<br>

* Updatemember.jsp

```javascript
<%@page import="java.sql.DriverManager"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="java.sql.Connection"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

    <%

request.setCharacterEncoding("utf-8");

	String name = request.getParameter("name");
	String website = request.getParameter("website");
	String email = request.getParameter("email");


	// 1. 드라이버 로딩
	String driver = "oracle.jdbc.driver.OracleDriver";
	String url = "jdbc:oracle:thin:@192.168.0.216:1521:orcl";
	String user = "KIHYUK";
	String pass = "3927";

	Connection con = null;
	PreparedStatement st = null;

	Class.forName(driver);

	//2. 연결객체 얻어오기
	con = DriverManager.getConnection(url,user,pass);

	// 3. sql 문장 만들기
	String sql = "UPDATE MEM SET name = ?, url = ? WHERE email = ?";
	// 4. 전송 객체 얻어오기
	st = con.prepareStatement(sql);
	st.setString(1,name);
	st.setString(2,website);
	st.setString(3,email);
	st.executeUpdate();


    %>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

</body>
</html>
```
