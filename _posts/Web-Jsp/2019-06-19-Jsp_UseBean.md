---
layout: post
title: Jsp UseBean
comments: true
categories: [Web/Jsp]
tags: [Web,Javascript,Jsp]
---
<br>

# <center> Jsp UseBean </center>

<br>

#### 1. UseBean 활용

<br>

* infoPut.jsp

```Javascript
<%@ page contentType="text/html; charset=UTF-8"
pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<title> 빈 기초 </title>
</head>
<body>
	<h2> 당신의 정보를 입력하세요 </h2><br/><br/>

	<form method="get" action="InfoSave.jsp" name="input">
	이       름 :  <input type=text name="name"><br/>
	주 민 번 호 :  <input  type=password name="id"><br/>
	<input type=submit value="저장" >
	<input type=reset value="취소">
	</form>

</body>
</html>
```

<br>

* InfoSave.jsp

```Javascript
<%@ page contentType="text/html; charset=UTF-8"
pageEncoding="UTF-8"%>

<%@ page import="info.beans.infoBean" %>

<jsp:useBean id="bean" class="info.beans.infoBean">  <!--id => 가져올 자바클래스 이름지정해주기 , class => 자바클래스 경로  -->
	<jsp:setProperty name='bean' property='*'/>

  <!--java 클래스객체(bean)의 이름들과 form의 이름들이 같을경우에만  -->
  <!-- name => 위에서 설정한 id  -->
</jsp:useBean>


<%	/*이런 자바코드를 쓰지않고 위의 동적jsp 사용  */
	/* infoBean bean = new infoBean();
	String name = request.getParameter("name");
	bean.setName(name);
	String id = request.getParameter("id");
	bean.setId(id); */
%>

<!DOCTYPE html>
<html>
<body>
	<h2>  당신의 신상명세서 확인 </h2>
	이   름  : <jsp:getProperty property="name" name="bean" /><br/>  //property는 가져올 setter지정,  name => 지정해논 자바클래스 이름
	주민번호 : <%= bean.getId() %> <br/> //getProperty 안쓰고 getter로도 가능
	성  별   : <jsp:getProperty property="gender" name="bean"/> <br/>  
	맞습니까????
</body>
</html>
```
