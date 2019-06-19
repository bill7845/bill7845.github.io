---
layout: post
title: Jsp Ajax 활용
comments: true
categories: [Web/Jsp]
tags: [Web,Javascript,Jsp]
---
<br>

# <center> Jsp Ajax 활용 </center>

<br>

#### 1. Ajax 활용 calculate

<br>

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>Ajax 계산기</title>
<script type="text/javascript"
	src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>

<script type="text/javascript">

	$(function(){
		$('#btn').click(function(){

			$.ajax({
				data: $('form').serialize(),  // $('form').serialize을 통해 데이터 보내기  // form 아이디로도 가능
        //{ op1 : $('#op1').val() , op2 : $('#op2').val() , opr : $('#opr').val() },
				type: 'get',
				url : './jsp/calc-action.jsp',
				success: function(res){
					$('#result').text(res)
				},
				error : function(e){
					alert('에러'+e)
				},
				dataType : 'text'			  // 받아 올 데이터 타입		
			})

			return false;	// return false => 기존의 submit 이벤트 기능 막음
		})

	})

</script>

</head>
<body>

	<form action="./jsp/calc-action.jsp" method="get">
	<input name="op1" id='op1' size="3">
	<select name="opr" id='opr'>
		<option>+</option>
		<option>-</option>
		<option>*</option>
		<option>/</option>
		<option>%</option>
	</select>
	<input name="op2" id='op2' size="3">
	<input type="submit" id='btn' value=" = ">
	</form>
	<fieldset>
		<legend>실행결과</legend>
		<div id="result"></div>
	</fieldset>

</body>
</html>
```

<br>

* calc_action.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

// param => param일는 객체를 통해 전송받아온 json데이터에 접근
// param => 기본객체
${param.op1 }+${param.op2 }

```

<br>

* calc_form-json.html

> json 구조 처리하기

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>Ajax 계산기 JSON</title>
<script type="text/javascript"
	src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>

<script type="text/javascript">

	$(function(){
		$('#btn').click(function(){

			$.ajax({
				data: $('form').serialize(),
				type: 'get',
				url : './jsp/calc-action-json.jsp',
				success: function(res){
					$('#result').text(res.result);	// res.result => 받아온 json데이터에 접근
				},
				error : function(e){
					alert('에러'+e)
				},
				dataType : 'json'		// 받아 올 타입 json  // 이번엔 서버에서 진짜 json형식으로 전송되어짐			
			})

			return false;	// return false => 기존의 submit 이벤트 기능 막음
		})

	})

</script>		

</head>
<body>

	<form action="./jsp/calc-action.jsp" method="get">
	<input name="op1" id="op1" size="3">
	<select name="opr" id="opr" >
		<option>+</option>
		<option>-</option>
		<option>*</option>
		<option>/</option>
		<option>%</option>
	</select>
	<input name="op2" id="op2" size="3">
	<input type="submit" id='btn' value=" = ">
	</form>
	<fieldset>
		<legend>실행결과</legend>
		<div id="result"></div>
	</fieldset>

</body>
</html>
```

<br>

* calc-action-json.jsp

```javascript
<%@ page language="java" contentType="application/json; charset=UTF-8"
    pageEncoding="UTF-8"%>

    {
    	"op1":${param.op1},
    	"op2":${param.op2},
    	"opr": "${param.opr}",
    	"result":${param.op1 + param.op2}
    }

```

<br>

* IdForm.html

> Ajax 활용 아이디 중복체크 검사
> JDBC의 경우 원래는 JAVA(DAO)에서 따로 처리함

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>아이디 중복 검사</title>
<script type="text/javascript"
	src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>

<script type="text/javascript">
	$(function() {

		$('#id_check').click(function() {

			var data = { userid : $('#userinput').val() }

			$.ajax({
				type : 'post',
				data : data,
				url : "IdCheck.jsp",
				success : function(res) {
					if(res.trim() == "YES"){	// 공백처리 해주어야 함
						$('#idmessage').text("이미 사용중인 아이디입니다");

					}else{
						$('#idmessage').text("사용 가능한 아이디입니다.");
					}
				},
				dataType : 'text'
			})
		})

	})
</script>

</head>
<body>

	<input name="id" type="text" class="userinput" id='userinput' size="15" />
	<button type="button" id="id_check">중복체크</button>
	<br />
	<br />
	<div id="idmessage" style="display:show;"></div>

</body>
</html>
```

* IdCheck.jsp

```javascript
<%@ page contentType="text/xml; charset=utf-8" %>
<%@ page language="java" import="java.sql.*"%>

<%
String driver="oracle.jdbc.driver.OracleDriver";
String user="KIHYUK";
String pass="3927";
String dbURL="jdbc:oracle:thin:@192.168.0.216:1521:orcl";


	Class.forName(driver);
	Connection connection=DriverManager.getConnection(dbURL,user,pass);

	String sql = "select * from mem_team where ID='" + request.getParameter("userid")+"'";
	System.out.println(sql);
	Statement stmt = connection.createStatement();
	ResultSet rs = stmt.executeQuery(sql);		

	String result="NO";
	if (rs.next()){		
		result = "YES";
	}		
	out.print(result);
%>


```
