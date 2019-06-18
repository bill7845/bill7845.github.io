---
layout: post
title: Jquery Basic
comments: true
categories: [Web/Jquery]
tags: [Web,Javascript,Jquery]
---
<br>

# <center> Jquery 기초 </center>

<br>

### 1. Jquery 기초 문법

> Jquery도 자바스크립트 기반 문법이기 때문에 스트립트 태그에 기술한다 <br>
> Jquery를 사용하기 위해 

<br>

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Test</title>
<!-- jquery도 자바스크립트 기반이기 때문에 스크립트에 기술한다 -->
<script type="text/javascript" src = "../lib/jquery-3.4.1.min.js"></script>
<script type="text/javascript">
	//$(선택자).동작하기() -> css처럼 원하는 태그 & 내용물을 찾는다
	//문서를 다 읽고 내용물을 시작하자 window.onload = function()이랑 같은기능
	//자바스크립트랑 비슷한 방법
	$(document).ready(function(){
		$("#here").hide(); //id가 here인 것 숨기기
	});

	//그래서 나온 jquery문법
	jQuery(function(){
		$("#here1").hide();
	});

	//축약형
	//글씨를 출력한 다음 안보이게 하는거라 새로고침계속누르면 글씨가 떴다가 사라지는거 볼 수 있음
	$(function(){
		$("#here2").hide();
	});
</script>
</head>
<body>
	<div id = "here">
		오늘은 행복한 화요일
	</div>
	<div id = "here1">
		오늘은 행복한 화요일
	</div>
	<div id = "here2">
		오늘은 행복한 화요일
	</div>
</body>
</html>
```
