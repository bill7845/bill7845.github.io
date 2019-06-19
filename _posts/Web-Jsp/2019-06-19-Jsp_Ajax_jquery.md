---
layout: post
title: Jsp Jquery Ajax
comments: true
categories: [Web/Jsp]
tags: [Web,Javascript,Jsp]
---
<br>

# <center> Jquery Ajax </center>

<br>

#### 1. Jquery 통한 Ajax 구현

<br>

> Jquery는 Ajax 기본으로 구현 가능
> json(객체) 형식 사용

* 01_ajax_get_csv.jsp   // get방식 csv 데이터

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<script  type="text/javascript"  src="libs/jquery-1.9.1.min.js"> </script>

<script type="text/javascript">
	$(function(){

		var data = { cate : 'book', name : 'hong'};	 // 무조건 json형식으로(객체 형식으로)
		$.get("01_server.jsp",data,parseData);
    //get방식 전송	//jquery는 ajax 기본으로 사용가능 	// $.get("보내줄 위치","보낼 데이터","실행 할 함수","받아올 데이터 타입")
	});


  // 함수의 경우
	function parseData(strText){
    var ary = strText.split('|');   // 자바스크립트는 배열자동으로 잡아줌. 즉, ary에 strText 데이터 split되어 들어오므로 배열됨.  // |기준으로 분할되어 배열에 저장됨
		for(var i=0; i<ary.length; i++){
			var param = ary[i].split('=');	// '=' 기준으로 다시한번 split
			if(param[0].trim() == 'cate'){	// trim() 공백제거 해줘야함
				$('#cate').val(param[1]);
			}
			if(param[0].trim() == 'name'){
				$('#name').val(param[1]);
			}
		}
	}

</script>

</head>


<body>
서버로부터 넘겨받은 데이터<br/>
첫번째 데이터 : <input type="text" name="" id="cate"/><br/>
두번째 데이터 : <input type="text" name="" id="name"/><br/>
</body>
</html>

```

<br>

* 01_server.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>


<%
	// 1. 이전 화면에서 넘겨받은 데이타
	String cate = request.getParameter("cate");
	String name = request.getParameter("name");

	// 2. 다시 화면으로 보낼 데이터 구성
	cate="서버로부터"+cate;
	name="from_server_"+name;
	out.write("cate="+ cate+"|name=" + name);

%>    
```

<br>

* 02_ajax_post_csv.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
	<script  type="text/javascript"  src="libs/jquery-1.9.1.min.js"> </script>
<script type="text/javascript">
	$(function(){

		var data = { cate : 'book', name : 'hong'};	// 무조건 객체형식으로

		// 축약형
		$.post("02_server.jsp",data,parseData);	 
		//post방식 전송  //jquery는 ajax 기본으로 사용가능 	// $.get("보내줄 위치","보낼 데이터","실행 할 함수","받아 올 데이터 형식") // 받아 올 데이터 형식 기본값 =csv

	});

	function parseData(strText){
		var ary = strText.split('|');   // 자바스크립트는 배열자동으로 잡아줌. 즉, ary에 strText 데이터 split되어 들어오므로 배열됨.  // |기준으로 분할되어 배열에 저장됨
		for(var i=0; i<ary.length; i++){
			var param = ary[i].split('=');	// '=' 기준으로 다시한번 split
			if(param[0].trim() == 'cate'){	// trim() 공백제거 해줘야함
				$('#cate').val(param[1]);
			}
			if(param[0].trim() == 'name'){
				$('#name').val(param[1]);
			}
		}
	}

</script>

</head>


<body>
서버로부터 넘겨받은 데이터<br/>
첫번째 데이터 : <input type="text" name="" id="cate"/><br/>
두번째 데이터 : <input type="text" name="" id="name"/><br/>
</body>
</html>

```

<br>

* 02_server.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%
	// 1. 이전 화면에서 넘겨받은 데이타
	String cate = request.getParameter("cate");
	String name = request.getParameter("name");

	// 2. 다시 화면으로 보낼 데이터 구성
	cate="서버로부터"+cate;
	name="from_server_"+name;
	out.write("cate="+ cate+"|name=" + name);
%>    

```

<br>

* 04_ajax_post_json.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
	<title></title>
	<script  type="text/javascript"  src="libs/jquery-1.9.1.min.js"> </script>
<script type="text/javascript">

	$(function(){

		var param = { cate : 'hello' , name :'hong'};

		$.ajax({
			type : 'post',
			data : param,
			url : "04_server.jsp",
			success : function (resText){	// javascript에서는 함수도 객체다(함수리터럴)
				var obj = {};
				obj = eval('(' + resText +")");
				$('#cate').val(obj.first);
			}
			// datatype => 받아올 데이터 형식이 json아님, 지정안해주면 기본으로 csv  (04_server.jsp 있는 내용들은 json처럼 보이게 해놓은것)
		});


		/* 	 함수리터럴에 의해 그냥 바로 넣어버림
		function parseData(){
			var obj = {};
			obj = eval('(' + resText +")");
			$('#cate').val(obj.first);
		}
		*/

	})

</script>
</head>

<body>
서버로부터 넘겨받은 데이터<br/>
첫번째 데이터 : <input type="text" name="" id="cate"/><br/>
두번째 데이터 : <input type="text" name="" id="name"/><br/>
</body>
</html>

```

<br>

* 04_server.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%	// 1. 이전 화면에서 넘겨받은 데이타
	String cate = request.getParameter("cate");
	String name = request.getParameter("name");

	// 2. 다시 화면으로 보낼 데이터 구성
	String result ="";

	result += "{";
	result += "'first' : "+ "'changed_"+cate+"_by_server" +"',";
	result += "'second' : "+ "'from_"+name+"_server'";
	result += "}";
	System.out.println(result);
	out.write(result);
%>
```
