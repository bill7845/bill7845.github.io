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

### Jquery 기초 문법

<br>

> Jquery도 자바스크립트 기반 문법이기 때문에 스트립트 태그에 기술한다 <br>
> Jquery를 사용하기 위해  <br>
> '#' => 아이디, . => 클래스

<br>

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Test</title>

<!-- 내 라이브러리에 jqery가 있는 경우 -->
<script type="text/javascript" src = "../lib/jquery-3.4.1.min.js"></script>
<!-- 구글에 있는 jquery 파일 사용 -->
<!-- <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script> -->

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

<br>

### Jquery 기초문법2

<br>

> 공통된 부분을 변수선언하여 처리 가능 <br>
> hover 이벤트의 경우 마우스를 댔을경우와 땠을경우 두가지의 함수 인자 <br>
> 여러 속성을 바꿀 경우 자바스크립트 객체구조(json)형식으로 접근

<br>

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8"/>
	<title> 첫 연습 </title>

<style type = "text/css">
	#here {
		position : absolute;
		top : 0;
		left : 0;
	}
</style>

<!-- 구글에 있는 jquery 파일 사용 -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>

<script type="text/javascript">
	//문서가 로딩된후에 id가 here인 것을 클릭하면 내용을 text()안의 내용으로 바꾼다.
	//어떤 동작 후 ( ex) 클릭이나 마우스 이벤트 등) 다음 동작을 실행하기 위해서 ( ex) 텍스트 내용을 바꾼다(덮어쓴다)를 하기 위해 인자를 function으로 받는다. 자바스크립트 함수처럼 )
	$(function(){
		$("#here").click(function(){
			$("#here").text("클릭하면 내용 변경");
		});
	})

		//변수선언을 해서 공통된 부분 처리 가능
		var here = $("#here");
		here.click(function(){
			here.text("클릭하면 내용 변경");
		});

		//마우스커서를 가져다 댔을 때
		here.mouseenter(function(){
			here.text("마우스가 들어옴");
		});

		//마우스를 땠을 때
		here.mouseleave(function(){
			here.text("마우스가  나감");
		});

		//마우스를 댔을 때 ,땠을 때 두 경우 모두 hover 이벤트이기 때문에 함수 인자가 두개 들어간다
		here.hover(function(){here.css("border", "2px solid green")}, function(){here.css("border", "2px dashed red")});

		//ms 단위
		here.fadeOut(1000);
		here.fadeIn("slow");

		//연결동작으로 붙여서 써도 된다.
		here.fadeOut(1000).fadeIn("slow"); //slow = 600ms, fast = 200ms, duration = 400ms
		here.slideUp("slow").slideDown(1000);

		//여러 속성을 바꾸고 싶을 때 자바스크립트 객체(jason구조)를 사용해서 바꾼다.
		here.animate({top : 200, left : 400}); //위치조절 애니매이션을 사용하기 위해선 css로 원래 위치를 지정해놓고 사용한다.

		var std = $("#student");
		// var n = $("#name")으로 찾아도 되는데 body 내용이 많아 질 수록 기준점을 정해준 다음 찾아주는게 효율적
		var n = std.find("#name");

		//여러 속성을 바꾸고 싶을 때 자바스크립트 객체(jason구조)를 사용해서 바꾼다.
		n.css({"background" : "#AAFF33", "color" : "red", "font-size" : "34pt"});
	});
</script>
</head>
<body>

	<div id="here">
	아자아자 제이쿼리~~!!!
	</div>

	<div id="student">
		<div id="name">홍길동</div>
		<div id="age">34</div>
	</div>

</body>
</html>
```

<br>

### Jquery 기초문법3

<br>

> css와 다르게 동작을 했을 때와 동작이 사라졌을 때 효과를 다 지정해줘야됨 알아서 원 상태로 돌아가지 않음 <br>
> jquery는 getter와 setter가 동일하다. ex) aa() : getter, aa("내용물") : setter <br>
> 속성값 이용하여 찾기 ( ex: #sm_1 : selected)
> 동적구조 변경

<br>

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8"/>
	<title> 첫 연습 </title>
<style type = "text/css">
	.active {border : 2px solid red;}
</style>

<script type="text/javascript" src = "../lib/jquery-3.4.1.min.js"></script>

<script type="text/javascript">
	$(function(){
		var man = $(".man");
		var woman = $(".woman");
		var input = $(".inputText");

		man.css("background", "red");
		woman.css("background", "blue");

		//2.css와 연결. 스크립트 위에 css에 active 클래스 효과 만들어 놓음
		//css와 다르게 동작을 했을 때와 동작이 사라졌을 때 효과를 다 지정해줘야됨 알아서 원 상태로 돌아가지 않음
		//focus와 blur가 짝꿍인듯
		input.focus(function(){
			$(this).addClass("active");  // addClass => 클래스 추가
		});
		input.blur(function(){
			$(this).removeClass("active"); // removeClass => 클래스 제거
		});

		//3.자바스크립트와 innerHTML과 유사한 역할
		//jquery의 특성: getter와 setter가 동일. ex) text() : getter, text("내용물") : setter
		//html에 단순 text를 넣는다
		$("#divText").text("<img src = 'images/puppy.jpg'>");
		//html에 내용물 집어넣기, 태그까지 써서 사용. ex) 이미지 넣기. 개발자 모드보면 <div>태그 안에<img>태그로 이미지 넣은거 확인할 수 있음
		$("#divHtml").html("<img src = 'images/puppy.jpg'>");
		//div태그 구조는 살아 있는데 내용이 다 살아짐
		$("#divEmpty").empty();
		//속성을 바꿔주는것
		$("#changeGrim").attr("src", "images/cat.jpg");

		//var() : value를 가져오거나 지정하는 함수
		$("#tf").val("나는 홍길동");
		$("#ta").val("작성중 입니다.");
		//콤보박스에 있는 value값으로 지정할 수 있다.
		$("#sel").val("incheon");
		//중복이 허용된 경우에는 배열로 넣어서 지정
		$("#sel_m").val(["seom1", "seom3"]);

		//여러 요소들중 고르는것
		var gender = $("input[name = 'gender']");
		gender.eq(1).attr("checked", true);
// 		$(list).get()
		//선택된 값들 가져와서 result 부분에 쓰기
		$("#check").click(function(){
			var list = [];
			$("#sel_m :selected").each(function(){
				list.push($(this).text());  // this => 선택된 항목의 text를 push
			})
			$("#result").text($("#tf").val() + $("#ta").val() + $("#sel :selected").val() +$("#sel_m :selected").text() + $("input[name = 'gender']:checked").val());
		})

		//5.동적구조 변경
		var actor = $("#actor");
		var tae = $("#tae");
		var su = $("#su");
		var bin = $("#bin");
		//모두 actor의 자식 노드로 들어가는 것이다.
		actor.append(tae);
		su.appendTo(actor);
		actor.append(bin);

		//동적으로 태그 추가
		var n = $("<div/>");
		n.text("새배우");
		n.appendTo(actor);
		actor.append("<div id = 'old'>헌배우</div>");
		$("<div id = 'old2'>헌헌배우</div>").appendTo(actor);

		//여러개 요소일 경우
		$(".data").each(function(){
			$(this).click(function(){
				alert($(this).text());
			});
		});
	});
</script>
</head>
<body>
	<!--  1 -->
	<ul>
		<li class="man">김수현</li>
		<li class="woman">김희애</li>
		<li class="woman">송혜교</li>
		<li class="man">하정우</li>
		<li class="woman">김태희</li>
	</ul>
	<!-- 2 -->
	<input type="text" class="inputText"/>
	<input type="text" class="inputText"/>
	<input type="text" class="inputText"/>


	<!-- 3 -->
		<div id="divText">여기에 글씨를</div>
		<div id="divHtml">여기에 그림을</div>
		<div id="divEmpty">여기를 비움</div>
		<p>
		<img src="images/puppy.jpg" id='changeGrim'>
		</p>

	<!-- 4 -->
		<p>
		<input id="tf" type="text" size="20" />
		<textarea id="ta" rows="3" cols="20"></textarea>
		<select id="sel">
			<option value="seoul">서울</option>	<!-- option에 value 값 없어도 됨 -->
			<option value="busan">부산</option>
			<option value="masan">마산</option>
			<option value="incheon">인천</option>
		</select>
		<select id="sel_m" multiple="multiple">
			<option value="seom1">제주도</option>
			<option value="seom2">울릉도</option>
			<option value="seom3">독도</option>
			<option value="seom4">거제도</option>
		</select>
		<input type='radio' name = 'gender' value = "남자"/>남자
		<input type='radio' name = 'gender' value = "여자"/>여자
		<input type='button' id='check' value='확인'/>
		<input type='button' id='sel' value='초기화'/> <!--  [과제] 클릭시 값 지정하려면  -->
		<div id='result'></div>
		</p>

	<!-- 5 -->
		<div id="actor">배우</div>
		<div id="tae">김태희</div>
		<div id="su">김수현</div>
		<div id="bin">현빈</div>
		<!-- [ 과제 ] 동적 테이블 만들기  -->

	<!-- 6 -->
		<div class="data">이름</div>
		<div class="data">직업</div>
		<div class="data">나이</div>


</body>
</html>
```

<br>

### Jquery filter

<br>

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>jquery filter</title>

<!--4. class 속성제어 -->
<style type="text/css">
	.bg { background : yellow; }
	.border { border : 3px dotted red; }
	.borderRed { border : 3px dotted red; }
	.borderBlue { border : 3px dotted blue; }
</style>

<script type="text/javascript" src = "../lib/jquery-3.4.1.min.js"></script>
<script type="text/javascript">
	$(function(){

		//요소찾기
//$("li") -> 모든 li요소
// 		//li첫번째 요소
// 		alert($("li:eq(0)").text());

// 		//짝수요소
// 		alert($("li:even").text());

// 		//네번째 요소
// 		alert($("li:eq(3)").text());

// 		//세번째까지의 요소
// 		alert($("li:lt(3)").text());

// 		//첫번째를 제외한 요소
// 		alert($("li:gt(0)").text());

// 		//'튀김'을 포함한 요소
// 		alert($("li:contains('튀김')").text());

		//각 그룹별 첫번째 요소 css랑 위치찾는게 비슷하다
		//다 같다
// 		$("li:first-child").css("border", "1px solid red");
// 		$("ul").find("li:first").css("border", "1px solid blue");

		//li요소 클릭 시 bg클래스 추가, toggleClass는 클릭할때마다 add했다가 remove했다가 반복
		$("li").each(function(){
			$(this).click(function(){
				$(this).addClass("bg");
			});
		});
		//어묵 밑에 자식요소들만 border 클래스 적용
		$("#food").find("ul").children().css("border", "1px solid red");

		//li요소에 마우스가 올라가면 bg클래스 적용, 내려가면 bg클래스 제거. 단, 어묵밑의 자식요소 빼고
		$("ul > li").not("#food ul > li, #food :nth-child(3)").hover(function(){
			$(this).addClass("bg");
		}, function(){
			$(this).removeClass("bg");
		});

	});

</script>

</head>
<body>
		<h1>제이쿼리 시작</h1>
		<h2>내가 좋아하는 음식 </h2>
		<ul id="food">
			<li>떡볶이</li>
			<li>어묵</li>
			<li>
				<ul>
					<li>어묵꼬치</li>
					<li>어묵튀김</li>
					<li>어묵탕</li>
				</ul>
			</li>
			<li>닭튀김</li>
			<li>돼지튀김</li>
			<li>소튀김</li>
			<li>구두튀김</li>
		</ul>
		<!-- 2. 추가하고 다시 확인 -->
		<h2>내가 좋아하는 술</h2>
		<ul>
			<li>와인</li>
			<li>맥주</li>
			<li>막걸리</li>
			<li>소주</li>
		</ul>
	<div id="result"></div>
</body>
</html>
```

<br>

### jquery event

<br>

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>jquery event</title>

<style type="text/css">
	.bg { background : yellow; }
	.border { border : 3px dotted red; }
</style>
<script type="text/javascript" src = "../lib/jquery-3.4.1.min.js"></script>
<script type="text/javascript">
	$(function(){
		//이벤트 연결 방식 (정석)
		//bind는 매번 이벤트 연결
		//one은 한번만 연결 각 요소마다.
// 		$("li").bind("click", function(){
// 			$("#result").text($(this).text());
// 		});

// 		$("li").one("click", function(){
// 			$("#result").text($(this).text());
// 		});

		//축약형을 훨씬 많이씀
// 		$("li").click(function(){
// 			$("#result").text($(this).text());
// 		});

		//이벤트 요소가 함수 매개변수로 들어온다. 확인용
		$("li").click(function(evt){
			for(var prop in evt){
				console.log(prop + ":" + evt[prop]);
			}
		});

		//동적으로 li요소 만들기
		$("h1").click(function(){
			var li = $('<li/>').text(new Date());
			$("ul").append(li);
		});

		//h1요소에 마우스 대면 손바닥모양 표시 : 누르란 의미
		$("h1").css("cursor", "pointer");

		//동적으로 만든 요소에도 이벤트가 적용되게 하는 법 live는 옛날버전 최근에는 on을 사용한다.
		$("body").on("click" ,'ul > li', function(){
			$("#result").text($(this).text());
		});
	});
</script>

</head>
<body>
	<h1>제이쿼리 이벤트</h1>
	 <ul>
		<li>부에노스 아이레스</li>
		<li>바르셀로나</li>
		<li>리마</li>
		<li>라파스</li>
	 </ul>
	<div id="result"></div>
</body>
</html>
```
