#Day4 - Summary (HTML / CSS)
> 2017.05.11 THU	
> **박윤식**

-

#CSS의 화면 표시 속성
>CSS display

###화면표시방법
>display:block

- 기존에 블럭요소가 아닌 요소를 블럭 속성을 갖도록 합니다.

>display:inline

- 기존에 인라인 요소가 아닌 요소를 인라인 속성을 갖도록 합니다.
- 반대로, div가 display 프로퍼티에 inline속성을 받으면 인라인 요소로 취급

>display:inline-block

- 인라인 요소에 높이와 상/하 패딩, 마진값을 줄 때 사용합니다.

>display:none

- 해당 요소의 하위 요소들도 전부 보이지 않게 되며, 공간도 차지하지 않습니다.

>visibility

- display: none;은 화면에서 차지하던 공간조차도 전부 없어지며,
- visibility: hidden;은 화면에서 차지하던 공간은 그대로인채 투명해진다고 생각하시면 됩니다.

###화면 넘침 표시방법
>overflow

```
div {  	overflow: hidden;		//넘친 콘텐츠를 전부 숨김
	overflow: visible;		//영역 밖으로 콘텐츠가 나간 모습이 보임
 	overflow: auto;			//콘텐츠가 넘칠경우, 스크롤바가 생성된다
	overflow: scroll;  		//콘텐츠가 넘치지 않아도 항상 스크롤바가 있다.}
```

- 높이가 고정되어있고, 내용이 길면 스크롤 할 부분에서는 auto를 사용합니다.

-

#CSS float 속성
>CSS float


###float속성
>float: 띄우다	
>float 속성은 중간에 이미지를 넣은 단락을 만들고자 하는 경우에도 사용가능.	
>float를 사용하면 해당 요소를 문서의 흐름과 별개로 취급하여, 왼쪽이나 오른쪽으로 띄워줄 수 있다. ex)float:right; float left;


###clear 속성
>float 요소와 겹치는 경우, float속성을 해제합니다.

```
p{ 	clear: both;			//left, right 모두 해제
	clear: left;
	clear: right;  }
```
-

#CSS float 레이아웃
>CSS로 레이아웃을 구현할 때는 float속성을 자주 사용합니다.

###float layout

>CSS

```
.float-frame {  	width: 300px;
	background-color: #eee;
	border: 1px solid #ddd;
	padding: 10px;  }   .float-unit {
	width: 50px;  	background: #333;
	color: #fff;
	font-size: 18px;
	font-weight: bold;
	text-align: center;
	padding: 15px 0;
	margin-right: 5px;  }
```
>HTML

```
<div class="float-frame">  	<div class="float-unit">A</div>
	<div class="float-unit">B</div>
	<div class="float-unit">C</div>
	<div class="float-unit">D</div>  </div>
```

>float속성을 추가 

```
.float-util {
	float:left;
}
```

- 이 경우 항목들은 float:left를 따라 잘 배열 되지만, 부모요소의 height가 인식되지 않는다.

###float 레이아웃 - 임의의 요소삽입
>float을 해제할 임의의 요소삽입

- HTML에 `<br style="clear: both;">`br태그를 이용한 임의의 요소를 삽입할수 있다.

###float 레이아웃 - overflow를 사용

> 부모요소에 overflow를 설정할 수 있다.

```
overflow: auto;
overflow: hidden;
```
- overflow:hidden은 overflow:visible때는 인식하지 못하던 float요소와, 자식욧의 margin값을 인식하게 된다.

###float 레이아웃 - 부모에도 float를 설정
>CSS의 부모에 float:left를 적용

###float 레이아웃 - 가상선택자를 이용 *
>::after 가상선택자를 사용
>때에 따라서 ::before 사용 가능

```
.float-frame::after {	content: ' ';			//컨텐츠 속성은 반ㄷ시 있어야 함	display: block;	height: 0;
	clear: both
}
```
-

#CSS 포지션
>CSS position : CSS 의 요소의 위치를 설정합니다.

- static		:	기본값
- relative	:	static과 같은 순서로 배치되지만, top, right, bottom, left속성을 이용해 위치를 지정 가능
- fixed		:	브라우저 창 기준으로 위치
- absolute	:	자신과 가장 가까운 'position'이 'static'이 아닌 부모를 기준(없을 경우 본문(body)가 기준)

-

#CSS 가운데 정렬
>CSS Center Positioning

###가로 가운데 정렬
>부모의 가운데로 정렬하는 법

```
width: 500px;
margin:0 auto;
```

- 전체 크기가 정해져 있지 않을 경우, 내용의 width만 지정한 후 좌/우 여백은 auto로 같게 처리해 준다.

###가로/세로 가운데 정렬
>부모의 가로/세로 가운데 정렬하는 법
>




-

#Semantic Tag
>웹 사이트에서 자주 사용하는 문서 구조를 태그로 만든 것  검색엔진, 시각장애인용 스크린리더, 개발자에게 문서의 각 부분이 어떤 역할을 하는지 쉽게 알려줌



>header 	머릿말, 페이지 맨 위나 왼쪽에 삽입 
>nav 	내비게이션 링크, 가로/세로 형태의 메뉴에 사용 
>section 	콘텐츠 영역 
>article 	콘텐츠 내용 
>aside 	본문 이외의 내용 (메인 내용에 영향을 주지 않는 링크 등) 
>footer 	꼬릿말, 제작자 및 저작권 정보 표시



-
#Sass
>Syntactically Awesome Stylesheet

### #Sass는?
>CSS 전처리기(Pre-processor)	
>	
>Sass와 같은 ‘CSS확장 언어’의 파일을 웹 브라우저에서 해석할 수 있는   css파일로 만들어주는 처리기

###Sass 기본구조
>Sass basic structure

```
div.container {
	padding: 15px;
	margin: 0;   	> p#main-title {
	font-size: 16px;
	font-weight: bold;  	} 
		  	> .fixed {
	position: fixed;
	bottom: 10px;
	right: 10px;  	}
}
```

###Sass의 출력 스타일 - expanded
>expanded CSS

```
div.container {
	padding: 15px;
	margin: 0;  }   
div.container > p#main-title {
	font-size: 16px;
	font-weight: bold;  }   
div.container .fixed {
	position: fixed;
	bottom: 10px;  
	right: 10px;  }
```
###Sass의 출력 스타일 - nested
>nested CSS

```
div.container {  	padding: 15px;  	margin: 0; }  	div.container > p#main-title {  		font-size: 16px;  		font-weight: bold; }
	div.container .fixed {  		position: fixed;
		bottom: 10px;
		right: 10px; }
```

###Sass의 출력 스타일 - compact
>compact CSS

```
div.container { padding: 15px; margin: 0; }  div.container > p#main-title { font-size: 16px; font-weight: bold; }   div.container .fixed { position: fixed; bottom: 10px; right: 10px; }
```
###Sass의 출력 스타일 - compressed
>compressed CSS

```
div.container{padding:15px;margin:0}div.container p#main-title{font-size:16px;font-weight:bold}div.container > .fixed{position:fixed;bottom:10px;right:10px}
```

###sass-autocompile
>atom package-Setting

- Compile on Save				:	저장시 자동 컴파일
- Compile with 'compressed'	:	Compressed 방식 파일 생성
- Compile with 'compact'		:	Compact 방식 파일 생성
- Compile with 'nested'			:	Nested 방식 파일 생성
- Compile with 'expanded'		:	Expanded 방식 파일 생성


- 상대 경로 지정		:	'../css/$1.css'

-

#Sass 문법
>Sass Syntax


###주석 Comment
>`//주석내용`		
> 또는		
>`/*주석내용*/` (CSS기본)		
>을 사용합니다.



```
// 한 줄 주석은 Sass에서만 지원하며,
// CSS컴파일 시 나타나지 않습니다.

div.container { 	padding: 15px;  	margin: 0;  /* 기존에 CSS에서 사용하는 주석 형태는 컴파일 시에도 나타납니다 */

	p#main-title { 		font-size: 16px; 		font-weight: bold;  
} 
/*  	여러 줄 주석은	기존 CSS주석 형태로만 사용 가능합니다  
*/  	.fixed { 		position: fixed;
		bottom: 10px;
		right: 10px;	}
}
```

*compile 전*

```
@charset "UTF-8";
div.container {  	padding: 15px;  	margin: 0;  
		/* 기존에 CSS에서 사용하는 주석 형태는 컴파일 시에도 나타나게 됩니다 */ 
	/*		여러 줄 주석은		기존 CSS주석 형태로만 사용 가능합니다 
	*/ }   
div.container p#main-title {
	font-size: 16px;
	font-weight: bold;  }   div.container .fixed {
	position: fixed;
	bottom: 10px;  right: 10px;  }
```
*compile 후*


###중첩(Nested)
```
.container {
	width: 1100px;
	margin: 0 auto;    
		> #page { 		width: 800px; 		border: 1px solid #eee;
		padding: 10px; 
		
		p.section-title {  
			font-size: 20px;  
			text-align: center;
		}
		
		p.section-content {
			font-size: 12px;
			color: #999;
		}
	}
}
```
> CSS에서의 .conteainer > #page를 뜻함

``` 
> #page { 	width: 800px; 	border: 1px solid #eee;
	padding: 10px;  
```
> CSS에서의 .container > #page p.section-title을 뜻함

``` 
p.section-title {  
	font-size: 20px;  
	text-align: center;  
```


###부모 참조 선택자 (&)
*Referencing parent selectors*


>Sass	

```
#page {
	width: 800px; 	border: 1px solid #eee;  
	padding: 10px;  	a { 
		text-decoration: none;		&:hover {
			color: red;
		}
		
		.link-container & {  
			font-size: 30px;
		}
	}
}
```

-  &은 자신의 부모 선택자를 참조합니다.	
-  &앞에 선택자가 있을 경우,	해당 선택자 다음에 현재 위치에서의 부모선택자를 참조한다.


>CSS

```
#page {  	width: 800px;  	border: 1px solid #eee;   
	padding: 10px;  } 

#page a {   
	text-decoration: none;  } 

#page a:hover {   
	color: red;  }   
.link-container #page a {   
	font-size: 30px;  }
```


###중첩 속성(Nested properties)

>Sass 	
>속성 다음에 -(dash) 로 이어지는 속성은 아래로 내려   작성할 수 있습니다

```
.container { 	margin: { 		left: auto;  
		right: auto;	}
}
```

>CSS

```
.container {
	margin-left: auto;
	margin-right: auto;  }
```

###선택자 상속(@extend)
*Selector inheritance*

>Sass	
>상속을 사용하면 같은 속성에서 일부만 바뀐 요소를 쉽게 컨트롤 할 수 있다.	
>상속받은 선택자가 .btn의 설정을 함께 공유한다.

```
.btn {  	background-color: #cdcdcd;
	font-weight: bold;  	color: white;  	padding: 5px 20px;  } .btn-ok {  	@extend .btn;  	background-color: #d9edf7;   
} .btn-cancel {  	@extend .btn;   
	background-color: #bbb;  } 
```

>CSS

```
.btn, .btn-ok, .btn-cancel {   
	background-color: #cdcdcd;   
	font-weight: bold;  	color: white;  	padding: 5px 20px;   
}  .btn-ok {  	background-color: #d9edf7;   
}  .btn-cancel {  	background-color: #bbb;   
}
```

###대체 선택자(%)
*Placeholder selector*

- 대체 선택자로 선언된 구문은 CSS로 해석되지 않는다.

>Sass

```
%btn {  	background-color: #cdcdcd;   
	font-weight: bold;  	color: white;  	padding: 5px 20px;
}
.btn-ok {   
	@extend %btn;  
	background-color: #d9edf7;  } 
.btn-cancel {  	@extend %btn;   
	background-color: #bbb;
}
```

>CSS	
>%btn에 지정한 속성은 CSS에 나타나지 않는다.

```
.btn-ok, .btn-cancel {   
	background-color: #cdcdcd;   
	font-weight: bold;  	color: white;  
	padding: 5px 20px; 
}

.btn-ok {
	background-color: #d9edf7;
}

.btn-cancel {  	background-color: #bbb; 
} 
```



###변수 / &
*Variables*

```
$padding: 10px;   				//변수명은 $로 시작한다.
$bg-color: #ececec;   
$title-font-weight: bold;   div.container {  	background-color: $bg-color;   //자주 쓰이는 color값을 저장한다.
	padding: $padding;  	margin: 0;   	p#main-title {  		font-size: 16px;  		font-weight: $title-font-weight;  //중복으로 쓰이는 값에 유용하다.	}   	p#sub-title {  		font-size: 14px;  		font-weight: $title-font-weight;  	}   	.fixed {  		position: fixed;   
		padding: $padding;   
		bottom: 10px;   
		right: 10px;
	}  
}  
```


###변수 데이터 유형

유형|설명
---|---
숫자(number) | 정수, 소수, 단위숫자 <br> ex) 1.0, 2.3em, 50px
문자(String) | 작은 따옴표 혹은 큰 따옴표로 감싸진 문자 <br> ex) 'images/025.png', "Sass 사용법"
색상(Color)|색상정보 <br> ex) #ff2342, rgb(255,233,210)
참/거짓값(Boolean)|참 또는 거짓값 <br> true, false
리스트(List)|공백이나 콤마로 구분해서 나열 <br> 2px solid gray, Heveltica, Sans-serif
맵(Map)|파이썬의 dict와 유사 <br> ex:{color:white, font-size: 12px}
비어있음(Null) | 값 초기화시 사용



###Sass 파일 호출
>import


```
@import 'variables'; 		//현재 파일 위치를 기준으로 불러온다.
   %btn {  	background-color: $brand-primary;   
	font-weight: bold;  	color: white;  	padding: 5px 20px;  }
```

- CSS파일을 불러올 때는 확장자를 입력해야 하지만, Sass파일을 불러올 때는 확장자를 입력하지 않아도 된다.
- _로 시작하는 파일은 CSS파일로 컴파일 되지 않는다.
- import 시에만 사용하는 파일은 _로 네이밍 해야 함.



-
#[nomalize css](https://necolas.github.io/normalize.css/)
	
-


> atom에서 태그 열을 선택 한 후 ctrl+w 실행하면 선택한 태그를 감쌀 수 있는 상위 태그를 만들 수 있다.
> 	
> cmd+' 감싸고 있는 태그만 삭제 할 수 있다.