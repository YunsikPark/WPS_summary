#Day2 - Summary (HTML / CSS)
> 2017.05.09 TUE	
> **박윤식**
 
-
#1. Table 요소
> **표를 만들 수 있는 table 요소**

###테이블의 기본구조
>*table basic*

```
<table>
	<tr>
       <th>이름</th>
       <th>나이</th>
       <th>점수</th>
    </tr>
    <tr>
       <td>철수</td>
       <td>23세</td>
       <td>70점</td>
    </tr>
    <tr>
       <td>영희</td>
       <td>21세</td>
       <td>89점</td>
    </tr>
</table>
```
<table>
	<tr>
       <th>이름</th>
       <th>나이</th>
       <th>점수</th>
    </tr>
    <tr>
       <td>철수</td>
       <td>23세</td>
       <td>70점</td>
    </tr>
    <tr>
       <td>영희</td>
       <td>21세</td>
       <td>89점</td>
    </tr>
</table>

- `<table></table>` 테이블의 시작과 끝
- `<tr></tr>` 행을 나타낸다.
- `<th></th>` 테이블의 헤더 셀.
- `<td></td>` 일반 셀.


###셀 병합
>*colspan*

```
<table>
	<tr>  		<td>a</td>  		<td>b</td>
	</tr>  	<tr>  		<td colspan="2">c</td>  	</tr>
</table>
```
<table>
	<tr>  		<td>a</td>  		<td>b</td>
	</tr>  	<tr>  		<td colspan="2">c</td>  	</tr>
</table>

- **`colspan`**은 가로로 셀을 합친다.
- 즉, 열(col)들을 병합하는 속성
- 병합은 **`th`** 또는 **`td`** 에서 사용할 수 있다.
- 병합된 셀 수 만큼 행(**`tr`**)안에 셀을 덜 적어준다.

>*rowspan*

```
<table>
	<tr>  		<td rowspan="3">a</td>  		<td>b</td>
	</tr>  	<tr>
		<td>c</td>  	</tr>
	<tr>  		<td>d</td>
	</tr>  </table>
```
<table>
	<tr>  		<td rowspan="3">a</td>  		<td>b</td>
	</tr>  	<tr>
		<td>c</td>  	</tr>
	<tr>  		<td>d</td>
	</tr>  </table>

- **`rowspan`**은 세로로 셀을 합친다.
- 새로로 합쳐진(병합된) 셀의 수에 해당하는 다음 행(**`tr`**)의 셀 개수는 하나씩 줄어들게 된다.



###행의 구조화
>*thead, tbody, tfoot*

```
<table>
    <thead>
      <tr>
        <th>이름</th>
        <th>나이</th>
        <th>성별</th>
        <th>성적</th>
        <th>메모</th>
      </tr>
    </thead>
    
    <tbody>
      <tr>
        <td>홍길동</td>
        <td>22세</td>
        <td>남자</td>
        <td>98점</td>
        <td>잘생김</td>
      </tr>
      <tr>
        <td>김춘향</td>
        <td>19세</td>
        <td>여자</td>
        <td>99점</td>
        <td>이쁨</td>
      </tr>
      <tr>
          <td colspan="3">평균</td>
          <td>87</td>
          <td></td>
        </tr>
      </tbody>
      
      <tfoot>
        <tr>
          <td colspan="5">Copyright @ ...</td>
        </tr>
      </tfoot>
  </table>
```
  <table>
    <thead>
      <tr>
        <th>이름</th>
        <th>나이</th>
        <th>성별</th>
        <th>성적</th>
        <th>메모</th>
      </tr>
    </thead>    
    <tbody>
      <tr>
        <td>홍길동</td>
        <td>22세</td>
        <td>남자</td>
        <td>98점</td>
        <td>잘생김</td>
      </tr>
      <tr>
        <td>김춘향</td>
        <td>19세</td>
        <td>여자</td>
        <td>99점</td>
        <td>이쁨</td>
      </tr>
      <tr>
          <td colspan="3">평균</td>
          <td>87</td>
          <td></td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td colspan="5">Copyright @ ...</td>
        </tr>
      </tfoot>
  </table>

- `colgroup`이 열을 그룹화한다면, **`thead`**, **`tbody`**, **`tfoot`**은 행을 그룹화 한다.
- **`thead`**는 열의 제목을 나타낸다.
- **`tbody`**는 본문에 해당하는 영역
- **`thead`** 와 **`tfoot`**은 table에서 한 번만 선언될 수 있으나, **`tbody`**는 여러번 선언되어 행을 그룹화 할 수 있다.
- **`tfoot`**는 도표 하단을 나타낸다.
- 일반적으로 도표 전체의 합계나 결과를 표시하는 경우가 많다.

####Example
```
  <table>
    <thead>
      <tr>
        <td colspan="9">포켓몬스터의 전설의 포켓몬</th>
      </tr>
      <tr>
        <th>지방</th>
        <th colspan="2">메인 전설의 포켓몬</th>
        <th colspan="6">그외 전설의 포켓몬</th>
      </tr>
    </thead>
    <!-- tbody>tr>td+td[colspan=2]+td[colspan=2]*3 -->
    <tbody>
      <tr>
        <td>관동지방</td>
        <td colspan="2">뮤즈</td>
        <td colspan="2">프리져</td>
        <td colspan="2">썬더</td>
        <td colspan="2">파이어</td>
      </tr>
      <!-- tr>td*3+td[colspan=2]*3 -->
      <tr>
        <td>성도지방</td>
        <td>칠색조</td>
        <td>루기아</td>
        <td colspan="2">라이코</td>
        <td colspan="2">엔테이</td>
        <td colspan="2">스이쿤</td>
      </tr>
      <!-- tr>td[rowspan=2]+td*2+td[colspan=2]*3 -->
      <tr>
        <td rowspan="2">호연지방</td>
        <td>그란돈</td>
        <td>가이오가</td>
        <td colspan="2">레지락</td>
        <td colspan="2">레지아이스</td>
        <td colspan="2">레지스틸</td>
      </tr>
      <!-- tr>td[colspan=2]*4 -->
      <tr>
        <td colspan="2">레쿠자</td>
        <td colspan="2">라티아스</td>
        <td colspan="2">라티오스</td>
        <td colspan="2">테오키스</td>
      </tr>
      <!-- tr>td[rowspan=2]+td*2+td[colspan=6] -->
      <tr>
        <td rowspan="2">칼로스지방</td>
        <td>제르네아스</td>
        <td>이벨타르</td>
        <td colspan="6" rowspan=2>#</td>
      </tr>
      <!-- tr>td[colspan=2] -->
      <tr>
        <td colspan="2">지가르테</td>
      </tr>
      <!-- tr>td[rowspan=3]+td*2+td[colspan=3]*2 -->
      <tr>
        <td rowspan="3">알로라지방</td>
        <td>코스모그</td>
        <td>코스모움</td>
        <td colspan="3">카푸꼬꼬꼭</td>
        <td colspan="3">카푸나비나</td>
      </tr>
      <!-- tr>td*2+td[colspan=3]*2 -->
      <tr>
        <td>솔가레오</td>
        <td>루나아라</td>
        <td colspan="3">카푸브루루</td>
        <td colspan="3">카푸느지느</td>
      </tr>
      <!-- tr>td[colspan=2]+td[colspan=3]*2 -->
      <tr>
        <td colspan="2">네크로즈마</td>
        <td colspan="3">실버디</td>
        <td colspan="3">울트라비스트</td>
      </tr>
    </tbody>
  </table>
```
  <table>
    <thead>
      <tr>
        <td colspan="9">포켓몬스터의 전설의 포켓몬</th>
      </tr>
      <tr>
        <th>지방</th>
        <th colspan="2">메인 전설의 포켓몬</th>
        <th colspan="6">그외 전설의 포켓몬</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>관동지방</td>
        <td colspan="2">뮤즈</td>
        <td colspan="2">프리져</td>
        <td colspan="2">썬더</td>
        <td colspan="2">파이어</td>
      </tr>
      <tr>
        <td>성도지방</td>
        <td>칠색조</td>
        <td>루기아</td>
        <td colspan="2">라이코</td>
        <td colspan="2">엔테이</td>
        <td colspan="2">스이쿤</td>
      </tr>
      <tr>
        <td rowspan="2">호연지방</td>
        <td>그란돈</td>
        <td>가이오가</td>
        <td colspan="2">레지락</td>
        <td colspan="2">레지아이스</td>
        <td colspan="2">레지스틸</td>
      </tr>
      <tr>
        <td colspan="2">레쿠자</td>
        <td colspan="2">라티아스</td>
        <td colspan="2">라티오스</td>
        <td colspan="2">테오키스</td>
      </tr>
      <tr>
        <td rowspan="2">칼로스지방</td>
        <td>제르네아스</td>
        <td>이벨타르</td>
        <td colspan="6" rowspan=2></td>
      </tr>
      <tr>
        <td colspan="2">지가르테</td>
      </tr>
      <tr>
        <td rowspan="3">알로라지방</td>
        <td>코스모그</td>
        <td>코스모움</td>
        <td colspan="3">카푸꼬꼬꼭</td>
        <td colspan="3">카푸나비나</td>
      </tr>
      <tr>
        <td>솔가레오</td>
        <td>루나아라</td>
        <td colspan="3">카푸브루루</td>
        <td colspan="3">카푸느지느</td>
      </tr>
      <tr>
        <td colspan="2">네크로즈마</td>
        <td colspan="3">실버디</td>
        <td colspan="3">울트라비스트</td>
      </tr>
    </tbody>
  </table>
  
  
-
#2. Form요소
>**데이터를 입력하거나 전송할 때 사용하는 요소**	
>**form은 브라우저(클라이언트)에서 서버로 데이터를 전송하기 위해 사용하는 태그**

```
<form action="" method="get">  	<label for="username">ID</label>
	<input type="text" name="username">  </form>
```
<form action="" method="get">
	<label for="username">ID</label>
	<input type="text" name="username">  </form>

###method 속성
- method : 폼에서 서버로 데이터를 전송하는 방식을 결정
- GET : URL에 데이터를 담아 전달 *(따로 설정하지 않는 경우 GET이 Default 값을 갖는다.)*
- POST : URL과는 별도로 데이터를 전달 _**(아이디/패스워드와 같은 중요한 정보를 전달 할 경우 사용)**_

###action 속성
- form에서 데이터를 전송할 URL을 기입한다.



###input 태그의 type들
>`input` 요소는 값을 가지거나, form에 영향을 준다.

```
<input type="text" id="username">  <input type="password" id="password">  <input type="radio" id="radio">  <input type="checkbox" id="checkbox">  <input type="button">  <input type="file" id="file">  <input type="submit">  <input type="reset">  <input type="hidden" id="hidden" value="hiddenValue">
```

- text : 텍스트를 입력할 수 있는 칸 생성
- password : 입력한 값을 보여주지 않는 칸 생성
- radio : 여러 선택지 중에 한가지 선택지를 고를 때 사용하는 
- checkbox : 체크박스 생성
- button : 버튼 생성	_**(일반적으로 button은 `button` tag를 사용한다.)**_
- file : 파일을 업로드하는 버튼 생성
- submit : 입력한 내용을 전송하는 버튼 생성
- reset : 같은 form안에 있는 요소들을 초기화하는 버튼 생성
- hidden : 사용자에게 보이지 않는 값을 생성 _(오류를 방지하기 위해 기본적으로 넣어준다.)_


###input 태그의 주요 속성들
```
<input type="text" value="disabled" disabled>
<input type="text" value="readonly" readonly>
<input type="text" required><input type=“text" placeholder=“공백은 안됩니다">
<input type="text" size="3">  <input type="text" maxlength="10">  <input type="checkbox" checked="checked">  <input id="radio1" type="radio" name="agree" checked="checked">
<input id="radio2" type="radio" name="agree">
```

- disabled: form submit 할 때 해당 값은 아예 보내지 않게 된다.
- readonly: form submit 할 때 값이 포함되고 사용자의 조작을 막을 수 있다. `만약 사용자의 조작을 막고 비활성화된 모습을 보여주고 싶다면 readonly속성을 지정하고 style을 지정하는 방법을 사용한다.`
- required : 사용자의 입력이 반드시 필요한 것임을 명시적으로 나타낸다.
- placeholder: input 태그 안에 보여지게 될 문구를 넣을 수 있다.
- maxlength: 폼 컨트롤의 최대 길이를 지정하는 속성
- radio: 같은 이름을 가진 radio요소는 동시에 체크되지 않는다.
- name: name 요소는 id와 동일한 값을 넣어주는데, input태그에서만 사용되며 폼의 값을 넘기기 위해 사용된다. 즉, 필요없는 폼에 쓰이는 name은 불필요하다.

###label 태그
> 폼 요소에 label을 붙임.

####label 내부에 표현

`<label>ID <input type="text"></label>`

- label 태그 내에 폼 요소를 삽입

####label과 별도로 표현

```
<label for="username">Username</label>
<input type="text" id="username">
```
- `for` 속성과 `form` 요소의 `id` 를 연결시키면 `label`이 정확히 해당 `form` 요소를 가리키게 된다.

###select 태그
>select태그는 여러개의 주어진 값 중 일부를 선택하는 역할을 한다.

```
<select name="number" id="select-id">
    <option value="1">First</option>
    <option value="2">Second</option>
    <option value="3">Third</option>
    <option value="4">Fourth</option>
</select>
```

####select태그의 속성

```
<select multiple="multiple">  	<option value="apple">Apple</option>
	<option value="banana">Banana</option>
	<option value="orange">Orange</option>  </select>
```
```
<select size="2">  	<option value="apple">Apple</option>
	<option value="banana">Banana</option>
	<option value="orange">Orange</option>  </select>
```
- 기본적으로 `select`요소는 `option`의 값을 한 개만 선택할 수 있다.
- `multiple` 속성을 가질 경우, ctrl(맥의 경우 cmd), shift키를 이용해 여러개의 값을 선택할 수 있다.
- `size` 속성은 한번에 `option`을 몇 개 보여줄지 정한다.

###optgroup 태크
>select요소와 option을 그룹화하여 보여준다.

```
<select name="optgroup-select" id="">
  <optgroup label="Fruits">
    <option value="apple">Apple</option>
    <option value="banana">Banana</option>
    <option value="orange">Orange</option>
  </optgroup>
  <optgroup label="Colors">
    <option value="red">Red</option>
    <option value="blue">Blue</option>
    <option value="green">Green</option>
  </optgroup>
</select>
```

###button 태그
>button요소는 input요소와 같은 type을 대체할 수 있다.

```
<button type="submit">submit type button</button>
<button type="reset">reset type button</button>
<button type="button">button type button</button>
```

###fieldset, legend 태그

```
<form action="">
  <fieldset>
    <legend>Login</legend>
    <label>username<input type="text"></label>
    <label>password<input type="password"></label>
  </fieldset>
</form>
```
- legend 요소는 fieldset의 첫 번째 자식으로 사용해야한다.
- fieldset
	- 선으로 둘러싸인 구역을 생성
	- fieldset은 다른 fieldset을 중첩해서 자식으로 가질 수 있다.




### CLASS & ID
>**`class`와 `id`의 이름은 짧게 짓기 보다는, 길더라도 해당 요소의 의미에 적합하게 짓는 것이 더 좋다.**

```
<div class="chapter" id="chapter1">
	<h2>HTML</h2>  	<p>HTML강의를 시작해봅시다</p>  </div>
    <div class="chapter" id="chapter2">
	<h2>CSS</h2>  	<p>Chapter2는 CSS입니다!</p>  </div>
    <div class="chapter" id="chapter3">
	<h2>JavaScript</h2>
	<p>JavaScript는 야무님이죠!</p>  </div>  
```

####네이밍
- 첫 글자는 알파벳으로 시작
- 두 번째부터는 알파벳, 숫자, -, _를 사용 가능
- 대소문자 구분

####클래스와 아이디의 차이
- `id`(아이디)는 페이지에서 딱 한번만 선언 가능, 요소의 unique한 특성을 나타냄
- `class`(클래스)는 여러번 사용가능, 범용적인 부분을 나타냄



###색상
>색상은 Hex code를 사용한 #000000 ~ #FFFFFF까지의 값과, HTML규격에 미리 정의된 ColorName을 사용할 수 있다.

```
<p style="color: #333;">Color #333</p>  <p style="color: DarkGreen;">Color DarkGreen</p>
```

-

#3. CSS
>Cascading Style Sheet	
>마크업 언어(HTML)가 실제 표시되는 방법을 기술하는 언어    
>레이아웃과 스타일을 정의할 때 사용    
>HTML에는 스타일을 제외한, 문서의 구조만이 명확히 나타나야 함

###CSS 문법
```
selector {
	property: value;
}

#body-title {  font-size: 14px;  font-weight: bold;  color: DarkSlateGrey;}
```
- 선언블럭은 스타일을 정의해줄 부분을 선택하는 선택자(selector)와 설정할 스타일의 속성(property), 값(value)로 구성된다.

###CSS 사용법 3가지
- **Internal style sheet** : `<html>`에서 `<head>` 내부 `style` 태그에 작성하는 방법
- **Inline style sheet** : 사용할 요소의 `style` 속성에 작성하는 방법
- **External style sheet** : `link` 태그를 사용해 외부 파일에 작성하는 방법


-
#4. CSS 선택자
###Universal Selector(전체선택자)
>*별표기호(Asterisk)

```
* {    padding: 0;
   margin: 0;
}
```

- HTML페이지 내부의 모든 요소에 같은 CSS속성을 적용한다.- 따라서 margin이나 padding값을 초기화하는 등, 기본값을 정할 때 주로 사용.
- 다만 문서의 모든 요소를 읽기 때문에 페이지 로딩시간이 길어 질 수 있으니 자주 사용하는 것은 좋지 않다.

###Combinator Selector(복합선택자)
>하위선택자와 자식선택자(Descendant selector & Child selector)    

####하위선택자(Descendant selector)
```
section ul {  	border: 1px solid black;  }
```

####자식선택자(Child selector)
```
section > ul {  	border: 1px solid black;
}
```

- 포함 관계를 가지는 태그들 사이에서, 포함하는 요소는 ‘부모 요소’, 포함되는 요소는 ‘자식 요소’라고 한다.
- 하위 선택자는 부모요소에 포함된 ‘모든’ 하위 요소를 지정하며,
- 자식 선택자는 부모요소의 ‘바로 아래’ 자식 요소만을 지정한다.

>인접 형제 선택자와 일반 형제 선택자 (Adjacent Sibling & General Sibling)    

####인접 형제 선택자(Adjacent Sibling)
```
h1 + ul {
	background: Azure;
	color: DarkBlue;  } 
```
####일반 형제 선택자(General Sibling)
```
h1 ~ ul {  	background: Azure;  	color: DarkBlue;
}
```

- 같은 부모 요소를 가지는 요소들은 ‘형제 관계’ 라고 부릅니다.
- 이 때, 먼저 나오는 요소를 ‘형 요소’, 나중에 나오는 요소는 ‘동생 요소’라 한다. (부모 요소 내부에서 보다 윗 줄에 쓰여진 것을 의미한다)

- 두 선택자 모두 형 요소에는 적용되지 않으며, 인접 형제 선택자는 조건을 충족하는 ‘첫 번째’ 동생 요소만을 지정하며, 일반 형제 선택자는 조건을 충족하는 ‘모든’ 동생 요소를 지정한다.


-

#5. CSS 우선순위

###CSS 스타일 적용 우선순위
>특정도(specify)값이 높은 순서대로 적용    
>특정도는 가장 구체적인 값을 의미

####특정도 계산식
스타일|특정도
---|---
important|Absolute
Inline(인라인스타일)|A
ID Selector(ID 선택자)|B
Class Selector(클래스 선택자)|C
Tag Selector(태그 선택자)	|D

- 특정도는 CSS구문에서 해당하는 스타일의 수 * 특정도 값 을 모두 더한 값입니다.
- 클래스 선택자가 3개 존재하며, 태그선택자가 있는 CSS구문이라면
- ex) p.wrap.item>.active - 클래스선택자의 갯수(3) * 클래스선택자의 특정도(10) + 태그선택자의 개수(1) * 태그 선택자의 특정도(1) = 31의 특정도를 가지게 됩니다.

>!important값은 해당하는 요소에 지정된 어떤 특정도도 무시하고 가장 우선순위로 적용됩니다.이는 테스트시에는 유용할 수 있지만, 추후 유지보수나 전체적 스타일 흐름을 방해하기 때문에 이용하지 않는 것이 좋습니다.
>`p{ font-size: 30px !important;   color: green !important;  }`

