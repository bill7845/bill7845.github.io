---
layout: post
title: Jsp Ajax_Get&Post
comments: true
categories: [Web/Jsp]
tags: [Web,Javascript,Jsp]
---
<br>

# <center> Jsp Ajax Get방식 Post방식 </center>

<br>

####  Ajax 개념

<br>

> javascript로 개념확인
> 서버에서 데이터를 변환,수정할때마다 화면 계속 새로고침 (데이터만 수정한게 아니라 화면 전체 다 새로고침해줌)
> 즉, request,response에 대해 계속 화면이 새로 수정됨  => 기본적인 웹  => 일부만 수정되도 새로고침되므로 비효율적
> ajax 방식을 통해서 해결
> get 방식과 post방식 차이점

* 01_ajax_get_csv.jsp

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title></title>
<script>
	var xmlHttp;
	window.onload = function() {
		// 1. 브라우저에 따른 XMLHttpRequest생성하기.
		xmlHttp = new XMLHttpRequest();

		// 2. 요청에 대한 응답처리 이벤트 리스너 등록.

		xmlHttp.onreadystatechange = on_ReadyStateChange; // 6번에 함수만들어놓음  // 응답에 따라 함수 호출될것임

		// 3.서버로 보낼 데이터 생성.

		var data = "cate=book&name=hong";   // parameter 활용 데이터전송  

		//###########################################################
		// 4. GET방식으로 데이터 보내기, 응답은 비동기로 클라이언트<->서버간의 연결 요청준비.

		xmlHttp.open("GET", "01_server.jsp?" + data, true); // xmlHttp.open("전송방식","위치",비동기통신 여부)

		// 5. 실제 데이터 전송.
		xmlHttp.send(null); //get방식을 보냈기 때문에 null값 해줘도 됨

		//####			
		// T. 동기/비동기 실행 테스트를 위한 부분.
		alert("전송 시작!");
	}

	// 6.응답처리.
	function on_ReadyStateChange() {
		if (xmlHttp.readyState == 4) {
			if (xmlHttp.status == 200) { // 정삭적으로 응답한 상태
				//alert('서버에서 보낸 데이터:' + xmlHttp.responseText) // responseText
        parseData(xmlHttp.responseText);  // xmlHttp.responseText => 서버에서 out.write한 데이터 가져옴(화면에 찍힌 데이터?)
			} else {
				alert('에러');
			}
		}
	}

	//##################################################
	//7. CSV포맷  데이터 처리.
	function parseData(strText) {
    var ary = strText.split('|');  // 자바스크립트는 자동배열. 즉, ary에 strText 데이터 split되어 들어오므로 배열됨.
                                  // |기준으로 분할되어 배열에 저장됨
    for(var i=0; i<ary.length; i++){
        var param = ary[i].split('=');	// '=' 기준으로 다시한번 split
        if(param[0].trim() == 'cate'){	// trim() 공백제거 해줘야함
            document.getElementById('cate').value = param[1]
        }
        if(param[0].trim() == 'name'){
            document.getElementById('name').value = param[1]
        }
      }
	}
</script>
</head>

<body>
	서버로부터 넘겨받은 데이터
	<br /> 첫번째 데이터 :
	<input type="text" name="" id="cate" />
	<br /> 두번째 데이터 :
	<input type="text" name="" id="name" />
	<br />
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
	cate = "서버에서" +cate+ "변경";
	name = "변경된" +name;

	out.write("cate="+cate+ " | name="+name);  


%>    

```

<br>

* ajax_post_csv.jsp

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
	<title></title>
	<script>
		var xmlHttp;
		window.onload=function(){
			// 1. 브라우저에 따른 XMLHttpRequest생성하기.
			xmlHttp = new XMLHttpRequest();

			// 2. 요청에 대한 응답처리 이벤트 리스너 등록.
			xmlHttp.onreadystatechange = on_ReadyStateChange;

			// 3.서버로 보낼 데이터 생성.
			var data = "cate=book&name=hong";

			//###########################################################
			// 4. POST 방식으로 데이터 보내기, 응답은 비동기로 클라이언트<->서버간의 연결 요청준비.
			xmlHttp.open("POST", "02_server.jsp", true);		// post방식은 데이터 도착할 파일명만
			xmlHttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");  // 한글처리 위해

			// 5. 실제 데이터 전송.
			xmlHttp.send(data);  // post방식은 여기서 데이터 넣어서 보내줌


			//####			
			// T. 동기/비동기 실행 테스트를 위한 부분.
			alert("전송 시작!");
		}


		// 6.응답처리.
		function on_ReadyStateChange(){
			if (xmlHttp.readyState == 4) {
				if (xmlHttp.status == 200) { // 정삭적으로 응답한 상태
					//alert('서버에서 보낸 데이터:' + xmlHttp.responseText) // responseText
					parseData(xmlHttp.responseText);
				} else {
					alert('에러');
				}
			}
		}

		//#################################################
		//7. CSV포맷  데이터 처리.
		function parseData(strText){
			var ary = strText.split('|');   // 자바스크립트는 배열자동으로 잡아줌. 즉, ary에 strText 데이터 split되어 들어오므로 배열됨.  // |기준으로 분할되어 배열에 저장됨
			for(var i=0; i<ary.length; i++){
				var param = ary[i].split('=');	// '=' 기준으로 다시한번 split
				if(param[0].trim() == 'cate'){	// trim() 공백제거 해줘야함
					document.getElementById('cate').value = param[1]
				}
				if(param[0].trim() == 'name'){
					document.getElementById('name').value = param[1]
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

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
	<title></title>
	<script>
		var xmlHttp;
		window.onload=function(){
			// 1. 브라우저에 따른 XMLHttpRequest생성하기.
			xmlHttp = new XMLHttpRequest();

			// 2. 요청에 대한 응답처리 이벤트 리스너 등록.
			xmlHttp.onreadystatechange = on_ReadyStateChange;

			// 3.서버로 보낼 데이터 생성.
			var data = "cate=book&name=hong";

			//###########################################################
			// 4. POST 방식으로 데이터 보내기, 응답은 비동기로 클라이언트<->서버간의 연결 요청준비.
			xmlHttp.open("POST", "02_server.jsp", true);		// post방식은 데이터 도착할 파일명만
			xmlHttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");  // 한글처리 위해

			// 5. 실제 데이터 전송.
			xmlHttp.send(data);  // post방식은 여기서 데이터 넣어서 보내줌


			//####			
			// T. 동기/비동기 실행 테스트를 위한 부분.
			alert("전송 시작!");
		}


		// 6.응답처리.
		function on_ReadyStateChange(){
			if (xmlHttp.readyState == 4) {
				if (xmlHttp.status == 200) { // 정삭적으로 응답한 상태
					//alert('서버에서 보낸 데이터:' + xmlHttp.responseText) // responseText
					parseData(xmlHttp.responseText);
				} else {
					alert('에러');
				}
			}
		}

		//#################################################
		//7. CSV포맷  데이터 처리.
		function parseData(strText){
			var ary = strText.split('|');   // 자바스크립트는 배열자동으로 잡아줌. 즉, ary에 strText 데이터 split되어 들어오므로 배열됨.  // |기준으로 분할되어 배열에 저장됨
			for(var i=0; i<ary.length; i++){
				var param = ary[i].split('=');	// '=' 기준으로 다시한번 split
				if(param[0].trim() == 'cate'){	// trim() 공백제거 해줘야함
					document.getElementById('cate').value = param[1]
				}
				if(param[0].trim() == 'name'){
					document.getElementById('name').value = param[1]
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
