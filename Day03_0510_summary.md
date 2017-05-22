#Day3 - Summary (HTML / CSS)
> 2017.05.10 WED	
> **박윤식**

-

경로		: 상대경로(현재경로기준)
./경로	: 상대경로(현재경로기준)
../경로	: 상대경로(상위경로로 이동)
/경로	: root경로로 이동
~/경로	: 사용자 폴더로 이동

-

###문자 들여쓰기
>text-indent


####Rem 그리고 Em, 언제 써야 할까

[참고](https://webdesign.tutsplus.com/ko/tutorials/comprehensive-guide-when-to-use-em-vs-rem--cms-23984)

###요소간 수직정렬
>vertical-align	
>박스 내에서의 수직정렬이 아닌, 나란히 오는 **인라인 요소간 수직정렬**


-

#CSS 배경스타일

###배경이미지
>이미지의 주소는 상대경로, 절대 경로 모두 사용가능하다
>하지만, style을 external style을 쓸 경우 html상의 경로와 다르기 때문에 유의해야한다.
>gif, jpg등 모두 사용 가능


###배경 이미지 반복
>가로로 반복하는 이미지의 경우, 세로로 길고 가로1px인 이미지를 이용해 배경을 나타낼 수 있으며,
>세로반복의 경우 반대로 가로로 길고 세로가 1px인 이미지를 이용해 배경을 나타낼 수 있다.
>하지만 현재에는 그라데이션 표현을 CSS 코드로 사용 가능하다.
>

###배경 이미지 위치
>삽입된 이미지의 좌표를 정해준다.
>두개의 값을 받으며, 각각 x축 y축의 값을 가진다.
>%값을 사용할 경우, 이미지 사이즈를 기준으로 움직인다. (x축이 100%일 경우, 이미지의 너비만큼 우측에서 보이게 됨)
>left, center, right, top, bottom으로 x,y축의 0%, 100%, 가운데 값을 사용할 수 있다.
> `background-image`를 사용시 height값을 줘야 표현이된다. 그렇지 않을 경우 


###배경 이미지 고정
>local값을 가질 경우, 요소의 왼쪽 상단을 기준으로 이미지를 표현하며, 스크롤 시 이미지가 같이 움직입니다.
>scroll값을 가질 경우, 요소의 왼쪽 상단을 기준으로 이미지를 표현하며, 스크롤 시 이미지가 함께 움직이지 않고 고정됩니다. 
>fixed값을 가질 경우, 요소와 관계없이 웹 페이지 전체 화면을 기준으로 이미지가 표시되며, 스크롤 시 함께 움직이지 않고 고정됩니다.

###배경 속기법
>지금까지 배운 background관련 속성을 한 번에 줄여쓸 수 있습니다.
>순서대로 image, repeat, attachment, position(x,y), color값을 나타냅니다.
>

-

#CSS 테두리 스타일

###테두리를 구성하는 요소
#### #선 굵기(border-width)	
>값을2개만적을경우,첫번째값은상&하의값,두번째값은좌&우의값을나타냅니다.
>

```
div {  border-width: 3px;					//상하좌우 모두 3px
border-top-width: 4px;  			//상단만 4px 
border-width: 3px 4px 5px 6px;   //상 우 하 좌 순서대로 3px 4px 5px 6px
border-width: 5px 10px;  			//상하 5px 좌우 10px}
```

#### #선 형태(border-style)

```
div {  border-style: solid;  border-top-style: double;  border-style: solid double dashed dotted;  }
```

- solid: 실선
- dotted: 점선
- dashed: 바느질선 형태의 점선
- double: 이중선
- groove: 입체적으로 보여줌
- ridge: groove와 반대방향으로 선이 돌출
- inset: 요소 전체가 안으로 들어가 보임
- outset: 요소 전체가 바깥으로 나와 보임


#### #선 색상(border-color)
>지금까지와 마찬가지로 Hex code, rgb, rgba, ColorName 전부 사용 가능합니다.

```
div {  border-color: #aaa;  border-color: red blue green yellow;  //상 우 하 좌 순서대로 각각 색을 설정할 수 있다.}
```

#### #테두리 속성 속기법
>border

```
div {  border: 1px solid red;  }
```

- border의 속기법은 모든 변에 동일한 값만 적용 가능합니다.- (각 변에 다른 값을 주고 싶을 경우, 각 속성(width, style등)에 4가지 값을 입력하거나, border-top-<property>에 값을 입력해야 합니다.


-

#CSS 박스 모델
###블록 요소와 인라인 요소의 차이
>인라인 요소의 길이/높이는 지정이 불가능(내용에 자동으로 맞추어짐)

###바깥 여백(마진 - margin)


###마진 겹침

###내부여백(패딩)
>padding과 magin을 구분하는 가장쉬운법은,
>padding과 margin을 준 요소에 background-color를 지정한 후 개발자 모드에서 해당요소가 차지하는 공간을 확인한다.
>

###가로,세로
>width, height

```
div {  	width: 200px;  	height: 50px;  	padding: 10px;  	border: 1px solid black;
	margin: 15px;  }
```

- 요소의 총 가로길이 : 200px(가로) + (10px + 1px + 15px) x 2 = 252px

###box-sizing
>박스 모델의 크기를 지정
>x-sizing에 border-box를 지정하면, 요소의 width값에 맞추어 padding, border값을 제외한 width가 새로 적용됩니다.

```
div {  	width: 200px;  	height: 50px;  	padding: 10px;  	border: 1px solid black;   
	margin: 15px;	box-sizing: border-box; }
```

-

#CSS 리스트 스타일
>CSS로 리스트에 스타일을 지정

###리스트 앞 Bullet 타입 설정
>`list-style-type`

```
ul {  	list-style-type: disc;   
	list-style-type: circle;   
	list-style-type: square; 	list-style-type: decimal;   
	list-style-type: lower-alpha;   
	list-style-type: upper-alpha;   
	list-style-type: lower-roman;   
	list-style-type: upper-roman;  }
```

- disc, circle, square는 Unordered List에 어울리는 속성이며,
- demical, alpha, roman은 Ordered List에 어울리는 속성.

###리스트 블릿에 이미지 지정
>`list-style-image`

```
ul {  	list-style-image: url('images/mic.png');  }
```

###리스트 블릿 위치 지정
>`list-style-position`

```
ul {  	list-style-position: inside;   
	list-style-position: outside;  }
```

- outside는 기본적인 리스트 형태.
- outside는 줄 바꿈이 일어나도 블릿과 일정한 여백을 유지한다.
- 반면, inside는 본문 내에 위치하게 된다.
- 때문에 줄바꿈이 일어나면 마치 본문의 일부처럼 보일 수 있다.

- **참고로 리스트의 여백은 `ul`요소의 `padding`으로 조절할 수 있다.**


###리스트 스타일 속기법
>`list-style`

```
ul {  	list-style: square url('images/mic.png') inside;  }
```
- 잘쓰지는 않지만, 블릿타입과 이미지 주소를 동시에 넣을 경우, 이미지를 찾지 못하면 지정한 블릿타입을 사용

-


#CSS의 테이블 스타일
>CSS Table Style

```
  <table>
    <tr>
      <td>A</td>
      <td>B</td>
      <td>C</td>
    </tr>
    <tr>
      <td>1</td>
      <td></td>
      <td>3</td>
    </tr>
    <tr>
      <td>4</td>
      <td>5</td>
      <td>6</td>
    </tr>
  </table>
```
###테두리 합치기
>`border-collapse`

```
table {  	border-collapse: collapse;  }  td {  	border: 1px solid black;   
	width: 30px;  	text-align: center; 
}
```

- 테이블의 셀간 공백을 합쳐서 없애는 속성입니다. 해당속성은 오직 table요소에만 사용 가능합니다.

###테이블 셀 간격
>`border-spacing`

```
table {  	border-spacing: 10px;  } 
```

- 셀 간 간격을 지정할 때는, border-collapse가 'collapse'값이면 적용되지 않는다.

###빈 셀의 표시
>`empty-cells`

```
table {  	border-spacing: 10px;  } td {  	border: 1px solid black;   
	width: 30px;  	text-align: center;   
	empty-cells: hide;  }
```
- empty-cells: `hide;`

###테이블 레이아웃
>table-layout	
>테이블의 기본설정은 내용이 긴 쪽이 더 늘어난다.
>**`table-layout:auto:`**


>table-layout의 속성을 **`fixed`**로 설정하면, 셀 길이가 일정하게 유지된다.	
>(이 때, table에는 width property가 설정되어 있어야 한다.)



###CSS3 :nth-child() Selector

[W3School](https://www.w3schools.com/cssref/sel_nth-child.asp)


