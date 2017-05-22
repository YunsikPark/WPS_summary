
## 공식문서

[Text Sequence - String Methods](https://docs.python.org/3/library/stdtypes.html#string-methods)

**추천도서**

- 처음시작하는 파이썬				// 초급
- 전문가를 위한 파이썬			//중급
- 파이썬 완벽가이드(programming insight)	//고급


# pyenv, virtualenv, iPython설치 및 설정

##pyenv
pyenv는 프로젝트별로 파이썬 버전을 따로 관리할 수 있도록 도와주는 라이브러리

여러 프로젝트를 동시에 진행하다보면, 어떤 프로젝트에서는 2.7을, 어떤 프로젝트에서는 3.5를 사용하는 식으로 다양한 버전을 사용할 수 있기 때문에 `pyenv`를 사용해서 파이썬 버전을 관리한다.


## virtualenv

virtualenv는 파이썬 개발환경을 프로젝트별로 분리해서 관리할 수 있게 해주는 라이브러리입니다.  
위의 pyenv와 다른점은, pyenv는 **파이썬**의 버전을 관리해주는 것이며, virtualenv는 **파이썬 패키지 설치 환경**을 따로 관리해줍니다.

## pyenv-virtualenv

위의 pyenv제작자가, pyenv를 사용할 경우 쉽게 virtualenv를 사용할 수 있도록 만든 라이브러리입니다.


## pyenv 설치

* 맥  
`brew install pyenv`  
`brew install pyenv-virtualenv`


## 기본 셸 변경

### zsh

<http://theyearlyprophet.com/love-your-terminal.html>  
bash와 비슷하게 동작하는 셸로, 사용성이 좋습니다.


#### 맥

```
brew install zsh zsh-completions
curl -L http://install.ohmyz.sh | sh
chsh -s `which zsh`
```

> **`chsh: /usr/local/bin/zsh: non-standard shell` 오류 발생할 경우**
> 
> ```
> sudo vim /etc/shells
> 맨 아래에 `which zsh`했을때의 결과를 추가 후 저장
> ```

> **현재 shell 확인법**  
> echo $SHELL




##pyenv global 설정

```
pyenv global 3.6.1 /수업은 3.5.3
```


## pyenv 설정

* 설치 후 pyenv관련 설정을 shell설정에 추가  
	* 맥 `vi ~/.zshrc`
	* 리눅스 	`vim ~/.zshrc`


> 맥
> 
```
export PYENV_ROOT=/usr/local/var/pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```


-

#### 파이썬 설치 전 필요 패키지 설치

<https://github.com/yyuu/pyenv/wiki/Common-build-problems>



#### 파이썬 셸 관련 설정 (macOS)

> 셸에서 방향키 관련 이슈 해결을 위한 유틸리티 설치

관련 유틸리티 설치 (readline, xz)

```
brew install readline xz
```

-

#### pyenv를 사용해서 파이썬 3.4.3버전 설치  

`pyenv install 3.6.1`

## pyenv 사용

#### 가상환경 생성

`pyenv virtualenv <version> <env_name>`
> `pyenv virtualenv 3.6.1 fc-python` 입력



#### 사용할 폴더로 이동
```
cd projects
mkdir python
cd python
```

#### local에 가상환경 지정
`pyenv local fc-python`


#### 가상환경 지우기
`pyenv uninstall <env_name>`

-


###pip

```
pip list

pip --upgrade pip

pip list --format=columns  

```


-

## iPython

기본 파이썬 셸보다 다양한 기능을 사용할 수 있도록 해주는 셸을 제공해줌

## iPython 설치

`pip install ipython`

커맨드라인에서 `ipython`실행

-

#### vi 단축키

`shift + g` : 가장 아래로  
`shift + a` : 현재 줄에서 가장 마지막으로

---

# 파이썬 사용해보기


## 각종 용어

**리터럴**  
변하지 않는 고정된 데이터 자체의 표현  

- 5 (정수형 데이터)
- "Fastcampus" (문자열 데이터)
- 1.4937 (부동소수점 데이터)



**표현식(expression)**  
값을 의미하는 표현 또는 값을 반환하는 표현

```python
>>> sec = 60
>>> 365*24*sec	# 표현식
525600				# 정수 525600의 리터럴 값
```
값의 의미를 지니지 않으며, 어떠한 목적을 수행하는 코드

```python
>>> for char in '안녕하세요':		# 구문 (제어문)
...   print(char)
... 
안
녕
하
세
요
```




## 실습

1. 파이썬 인터프리터를 계산기처럼 사용해서 1년이 총 몇 초인지 계산해보시오.

```
265*24*3600
```



## 변수

파이썬은 모든것(정수, 문자열, 함수 등)이 객체(Object)로 이루어져 있다.  
객체는 데이터의 형태를 결정해주는 타입으로, 파이썬에서는 객체의 타입을 바꿀 수 없다.

프로그래머는 **변수**를 선언하고 사용하는 형태로 컴퓨터의 메모리에 값을 할당하고, 참조할 수 있다. 파이썬에서는 값을 할당할때 `=`기호를 사용한다.

> 일반적으로, 프로그래밍 언어에서 같다(Equal)의 의미는 `=`이 아닌 `==`이 담당한다.
>



다음과 같은 코드는 **var1**이라는 이름을 가진 변수에 100의 정수를 할당하고, `print`를 이용해 **var1**변수가 가진 값을 출력한다.

```python
>>> var1 = 100
>>> print(var1)
100
```

변수는 단지 이름일 뿐이며, 그 자체가 어떠한 값을 갖는것이 아니다.  
위의 경우 **var1**이라는 변수는 100이란 데이터를 직접 가지는 것이 아니며, 100이라는 정수형 객체가 있고 a는 단순히 해당 객체를 **참조**하는 역할을 한다.

아래와 같이 명령어를 입력한다.

```python
>>> var2 = var1
>>> var3 = var1
>>> var4 = var1
```

어떠한 변수가 참조하고 있는 객체가 메모리 상에서 가지고 있는 고유의 주소(id)를 출력하는 id내장함수를 사용해본다.

```python
>>> id(var1)
4520513888
>>> id(var2)
4520513888
>>> id(var3)
4520513888
>>> id(var4)
4520513888
```

모든 변수들이 같은 객체를 가리키는 것을 볼 수 있다.

변수는 언제든 다른 객체를 가리킬 수 있다.

```
>>> var1 = 101
>>> id(var1)
4520513920
```

**var1**이 다른 객체를 참조하도록 변경했을 때, **var2, var3, var4**가 기존에 **var1**을 참조하던 것이 아닌, **var1**이 참조하던 객체를 참조했다는 것을 확인할 수 있다.

```
>>> id(var1)
4520513920
>>> id(var2)
4520513888
>>> id(var3)
4520513888
>>> id(var4)
4520513888
```
**단 1~100의 변수는 자주 사용하는 객체이므로 파이썬 내부적으로 고정된 주소를 사용하므로 따로 변수를 지정하더라도 같은 주소를 가진다.**


### 변수의 타입 확인

내장함수 **type**사용  

```python
>>> type(var1)
<class 'int'>
```

정수(Integer)형 변수임을 알 수 있다.

```python
>>> type('안녕하세요')
<class 'str'>
```

문자열은 **str**(문자열)형임을 나타낸다.

위의 출력에서, 클래스(class)는 객체의 타입(정의)을 나타낸다.  
`class`와 `type`은 거의 같은 의미로 사용된다.

### 변수의 이름 제한

#### 사용가능한 문자

- 소문자
- 대문자			// 가능한 쓰지 않는다.(python 개발자 사이에서의 규칙)
- 숫자
- 언더스코어(_)	// 일반적으로 사용하지 않는다.

이름은 숫자로 시작할 수 없으며, 언더스코어로 시작하는 변수명은 특별한 처리방법을 따르므로 일반적으로 사용하지 않는다.



#### 예약어

아래 예약어들은 파이썬 구문을 정의하는데 사용되기 때문에 변수로 사용할 수 없다.

False, class, finally, is, return,  
None, continue, for, lambda, try,  
True, def, from, nonlocal, while,  
and, del, global, not, with,  
as, elif, if, or, yield,  
assert, else, import, pass,    
break, except, in, raise



## 실습

1. 1일이 몇 초인지 계산 후, 해당 결과를 seconds_per_day 변수에 할당하라.
2. 1년이 몇 초인지 계산 후, 해당 결과를 seconds_per_year 변수에 할당하라.
3. 각 변수의 타입을 확인해본다.
4. `문자열을 입력해주세요 : `라는 안내문구를 띄워주도록 `input`함수를 사용해본다. 결과는 `var`에 할당한다.

# 내장데이터 타입 (숫자)

## 수학 연산자

연산자|설명|예|결과
---|---|---|---|
\+	| 더하기		| 32 + 7	| 39 
\-	| 빼기		| 82 - 2	| 80
\*	| 곱하기		| 3 * 7	| 21
/	| 나누기		| 7 / 2	| 3.5
//	| 정수나누기	| 7 // 2	| 3
%	| 나머지		| 7 % 3	| 1
**	| 지수		| 2**10	| 1024

## 산술 연산자 결합

a에 100을 할당하고, 3을 뺀 결과를 다시 a에 할당한다.

```
>>> a = 100
>>> result = a - 3
>>> a = result
>>> print(a)
97
```

위 코드는 아래와 같이 줄여서 사용가능하다.

```
>>> a = 100
>>> a = a - 3
>>> print(a)
97
```


위 코드는 산술 연산자 결합으로 아래와 같이 사용가능하다.

```
>>> a = 100
>>> a -= 3
>>> print(a)
97
```


## 우선순위

```python
>>> 10 + 5 * 4
```

우선순위 규칙이 적용되지만, 가독성에 문제가 있을 경우 괄호로 묶어준다.

```python
>>> 20 + (300 + 25 * 4)
```


## 진수(base)

기본적으로 숫자형 데이터는 10진수로 간주되지만, 파이썬에서는 2진수, 8진수, 16진수를 표현할 수 있다.

- 2진수(binary): **0b**또는 **0B**로 시작
- 8진수(octal): **0o**또는 **0O**로 시작
- 16진수(hex): **0x**또는 **0X**로 시작

```python
>>> 10
10
>>> 0b10
2
>>> 0o10
8
>>> 0x10
16
```


## 형변환

내장함수 **int**, **float**를 사용

```python
>>> int("35")
35
```


# 문자열

> 파이썬3에서는 문자열에서 기본적으로 유니코드(Unicode)를 사용하며, 불변(immutable)하다.

## 문자열 표현

**작은 따옴표 또는 큰 따옴표**  

```
>>> '패스트캠퍼스'
'패스트캠퍼스'
>>> "패스트캠퍼스"
'패스트캠퍼스'
```



작은 따옴표 또는 큰 따옴표를 사용했을 때, 사용하지 않은 인용 부호는 문자열 내부에서 사용 가능하다.

```
>>> '패스트캠퍼스 "웹 프로그래밍 스쿨"'
'패스트캠퍼스 "웹 프로그래밍 스쿨"'
```

```
>>> "패스트캠퍼스 \"웹 프로그래밍 스쿨\""
'패스트캠퍼스 "웹 프로그래밍 스쿨"'
```


**세 개의 작은 따옴표 또는 큰 따옴표**  
여러줄에 걸친 문자열을 나타낼 때 사용

```
>>> '''소환사 여러분.
... 
... 7.1 패치를 소개합니다.
... 
... 앞으로 있을 여러 번의 패치에 대해서는 차차...
... 하지만 그렇다고 이번 패치가 하향....
... 정의의 전장에서 승리를 기원합니다.'''
```


## 문자열 더하기

```
>>> notice = ''
>>> notice += '공지사항'
>>> notice += '(패치노트)'
>>> notice += ': 7.1 패치노트'
```
```
>>> notice
'공지사항(패치노트): 7.1 패치노트'
```

## 형변환

내장함수 **str**을 사용

```
>>> str(147)
'147'
```

문자열을 제외한 객체를 `print`함수로 호출하면, 내부적으로 `str`함수를 사용한 결과를 나타내준다.

## 이스케이프 문자

특수문자, 또는 특별한 역할을 하는 의미를 나타내는 문자를 뜻한다.  

이스케이프 문자|설명
---|---
\a	| 비프음 발생
\t	| 탭(tab)
\n	| 줄바꿈
\\	| \\(역슬래시) 입력
\\'	| 작은따옴표(') 입력
\\"	| 큰따옴표(") 입력

## 인덱스 연산

문자열에서 문자를 추출하기 위해 대괄호와 오프셋을 지정할 수 있다.  
가장 왼쪽은 0이며, 가장 오른쪽은 -1로 시작한다.

```
>>> lux = '빛으로 강타해요!'
>>> lux[0]
'빛'
>>> lux[-1]
'!'
>>> lux[50]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
```

문자열은 불변이므로 인덱싱한 부분에 새 값을 대입할 수 없다.



```
>>> lux[0] = '손'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

## 슬라이스 연산

**[start:end:step]** 형식을 사용한다.

- [:] 
	- 처음부터 끝까지
- [start:]
	- start오프셋부터 마지막까지
- [:end]
	- 처음부터 end오프셋까지
- [start:end]
	- start오프셋부터 end오프셋까지
- [start:end:step]
	- start오프셋부터 end오프셋까지, step만큼씩 뛰어넘은 부분
- [ : : -1]
   - 역순으로 출력

   
## 길이

내장함수 **len**을 사용


## 문자열 나누기(split)

문자열의 내장함수 **split**을 사용  
**split**함수에 인자로 주어진 **구분자**를 기준으로 하나의 문자열을 리스트 형태로 반환해준다.

```python
>>> girlsday = "민아,유라,소진,혜리"
>>> girlsday.split(',')
['민아', '유라', '소진', '혜리']
```

**split**함수에 인자를 주지 않을 경우, 공백문자를 구분자로 사용한다.


## 문자열 결합(join)

**split** 함수와 반대의 역할을 한다.  
문자열 리스트를 하나의 문자열로 결합해주며, 각 문자열을 결합해줄 구분자 문자열을 지정한 후 **join**함수를 사용해준다.

```python
>>> girlsday_list = girlsday.split(',')
>>> girlsday_str = ', '.join(girlsday_list)
>>> print(girlsday_str)
민아, 유라, 소진, 혜리
```


## 대소문자 다루기

```python
>>> lux = 'lux, the Lady of Luminosity'
>>> lux.capitalize()
'Lux, the lady of luminosity'
>>> lux.title()
'Lux, The Lady Of Luminosity'
>>> lux.upper()
'LUX, THE LADY OF LUMINOSITY'
>>> lux.lower()
'lux, the lady of luminosity'
>>> lux.swapcase()
'LUX, THE lADY OF lUMINOSITY'
```


## 공식문서

[Text Sequence - String Methods](https://docs.python.org/3/library/stdtypes.html#string-methods)

**추천도서**

- 처음시작하는 파이썬				// 초급
- 전문가를 위한 파이썬			//중급
- 파이썬 완벽가이드(programming insight)	//고급

## 문자열 포맷

#### 옛 스타일 (%)

```
string % data
```

변환타입|설명
---|---
%s	|	문자열
%d	|	10진수
%x	|	16진수
%o	|	8진수
%f	|	10진 부동소수점수
%e	|	지수로 나타낸 부동소수점수
%g	|	10진 부동소수점수 혹은 지수로 나타낸 부동소수점수
%%	|	리터럴 %

```
>>> '%s' % 42
'42'
>>> '%d x %d : %d' % (3, 4, 12)
'3 x 4 : 12'
```
#### 정렬

```
%[정렬기준(-,없음)][전체글자수].[문자길이 또는 소수점 이후 문자길이][변환타입]
```

```python
>>> d = 37
>>> f = 3.14
>>> s = 'Fastcampus'
>>> '%d %f %s' % (d, f, s)
'37 3.140000 Fastcampus'
>>> '%10d %10f %10s' % (d, f, s)
'        37   3.140000 Fastcampus'
>>> '%14d %14f %14s' % (d, f, s)		//기본 오른쪽 정렬
'            37       3.140000     Fastcampus'
>>> '%-14d %-14f %-14s' % (d, f, s)				//음수를 넣으면 좌측정렬로 바뀐다.
'37             3.140000       Fastcampus    '
>>> '%-14.3d %-14.3f %-14.3s' % (d, f, s)
'037            3.140          Fas           '
```




#### 새 스타일 ({}, format)

```
{}.format(변수)
```

```python
# 기본형태
>>> '{} {} {}'.format(d, f, s)
'37 3.14 Fastcampus'

# 각 인자의 순서를 지정
>>> '{1} {2} {0}'.format(d, f, s)
'3.14 Fastcampus 37'

# 각 인자에 이름을 지정
>>> '{d} {f} {s}'.format(d=50, f=1.432, s='WPS')
'50 1.432 WPS'

# 딕셔너리로부터 변수 할당
>>> dict = {'d': d, 'f': f, 's': s}
>>> '{0[d]} {0[f]} {0[s]} {1}'.format(dict, 'WPS')
'37 3.14 Fastcampus WPS'

# 타입 지정자 입력
>>> '{:d} {:f} {:s}'.format(d, f, s)
'37 3.140000 Fastcampus'

# 이름과 타입지정자를 모두 사용
>>> '{digit:d} {float:f} {string:s}'.format(digit=700, float=1.4323, string='Welcome')
'700 1.432300 Welcome'

# 필드길이 10, 우측정렬
>>> '{:10d}'.format(d)
'        37'
>>> '{:>10d}'.format(d)
'        37'

# 필드길이 10, 좌측정렬
>>> '{:<10d}'.format(d)
'37        '

# 필드길이 10, 가운데 정렬
>>> '{:^10d}'.format(d)
'    37    '

# 필드길이 10, 가운데 정렬, 빈 공간은 ~로 채움
>>> '{:~^10d}'.format(d)
'~~~~37~~~~'
```





# 시퀀스 타입

파이썬에 내장된 시퀀스 타입에는 문자열, 리스트, 튜플이 있다.  
문자열은 인용부호(작은따옴표, 큰따옴표)를 사용하며, 리스트는 대괄호[], 튜플은 괄호()를 사용하여 나타낸다.  
시퀀스 타입의 객체는 인덱스 연산을 통해 내부 항목에 접근 할 수 있다.

## 리스트

리스트는 순차적인 데이터를 나타내는 데 유용하며, 문자열과는 달리 내부 항목을 변경할 수 있다.


#### 리스트의 생성

```
>>> empty_list1 = []
>>> empty_list2 = list()
>>> sample_list = ['a', 'b', 'c', 'd']
>>> sample_list2 = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
```
다음과 같이 sample_list를 지정해줄 수도 있다.
```
sample_list='a b c d'split()
```


#### 다른 데이터를 리스트로 변환

**list** 함수를 사용

```python
>>> list('League of legends')
['L', 'e', 'a', 'g', 'u', 'e', ' ', 'o', 'f', ' ', 'l', 'e', 'g', 'e', 'n', 'd', 's']
```

이 외에도 리스트로 변환 가능한 타입에서 사용가능하다.



이 외에도 리스트로 변환 가능한 타입에서 사용가능하다.

#### 인덱스 연산

sample_list2를 이용해서 실습. 5월, 7월을 인덱스연산을 통해 추출해보자.

#### 내부항목 변경

sample_list를 이용, 3번째 요소인 'c'를 대문자 'C'로 바꿔본다.

#### 슬라이스 연산

- sample\_list2를 이용, 1월부터 3월씩 건너뛴 결과를 quarters에 할당
- sample\_list2를 이용, 끝에서부터 3번째 요소까지를 last_three에 할당
- sample\_list2를 이용, 끝에서부터 처음까지(거꾸로) 2월씩 건너뛴 결과를 reverse\_two\_steps에 할당


#### 리스트 항목 추가 (append)

```python
>>> sample_list.append('e')
>>> sample_list
['a', 'b', 'c', 'd', 'e']
```

#### 리스트 병합 (extend, +=)

```
>>> fruits = ['apple', 'banana', 'melon']
>>> colors = ['red', 'green', 'blue']
>>> fruits.extend(colors)
>>> fruits
['apple', 'banana', 'melon', 'red', 'green', 'blue']
```

```
>>> fruits = ['apple', 'banana', 'melon']
>>> colors = ['red', 'green', 'blue']
>>> fruits += colors
>>> fruits
['apple', 'banana', 'melon', 'red', 'green', 'blue']
```

**extend**대신 **append**를 사용하면?


```
>>> fruits = ['apple', 'banana', 'melon']
>>> colors = ['red', 'green', 'blue']
>>> fruits.append(colors)
>>> fruits
['apple', 'banana', 'melon', ['red', 'green', 'blue']]
```

#### 특정 위치에 리스트 항목 추가 (insert)

리스트 함수 **insert(offset)**을 사용  

- fruits리스트의 1번째 위치에 'mango'를 추가해보자
	- `fruits.insert(0, 'mango')`
- fruits리스트의 100번째 위치에 'pineapple'을 추가해보자

#### 특정 위치 리스트 항목 삭제 (del)

파이썬 구문 **del**을 사용  
> del은 리스트 함수가 아닌, 파이썬 구문이므로 `del <리스트>[오프셋]` 형식을 사용한다.

---
```
>>> del fruits[0]
```

**지정된 변수 초기화하기 ipython 기능**

```
%reset
%reset -f
```
**지정된 변수 리스트 보기 ipython 기능**

```
%hist
```
---

#### 값으로 리스트 항목 삭제 (remove)

```
>>> fruits.remove('mango')
```

#### 리스트 항목 추출 후 삭제 (pop)

```
>>> fruits.pop()
>>> fruits.pop(-3)
```

#### 값으로 리스트 항목 오프셋 찾기 (index)

```
>>> fruits.index('red')
```


#### 존재여부 확인 (in)

```
>>> 'red' in fruits
True
```

#### 값 세기 (count)

```
>>> fruits.append('red')
>>> fruits.append('red')
>>> fruits.count('red')
3
```

#### 정렬하기 (sort, sorted)

- sort는 리스트 자체를 정렬		//원래있던 것의 소스를 바꿔버림
- sorted는 리스트의 정렬 복사본을 반환		//원래 있던 소스를 건들지 않음 


#### 리스트 복사 (copy)

- copy함수
- list함수
- 슬라이스 연산[:]


```
fruits =['apple','banana','melon']

fruits=fruits_copy

fruits_copy = fruits.copy()

fruits[0]= 'asdf'

fruits =['asdf','banana','melon']

fruits_copy = ['apple','banana','melon']
```


## 튜플

튜플은 리스트와 비슷하나, 정의 후 내부 항목의 삭제나 수정이 불가능하다.

#### 튜플 생성

```python
>>> empty_tuple = ()
```

```python
>>> colors = ('red', )
>>> fruits = ('apple', 'banana')
```

튜플을 정의할 때는 괄호가 없어도 무관하나, **괄호로 묶는것이 좀 더 튜플임을 구분하기 좋다**.  
또한, 튜플의 요소가 1개일 때는 요소의 뒤에 쉼표(,)를 붙여야 한다.



#### 튜플 언패킹

```python
>>> f1, f2 = fruits
```

값의 교환

#### 형 변환

**tuple**함수를 사용 (튜플 생성에는 사용 불가능)

리스트를 튜플로 변환

#### 튜플을 사용하는 이유

- 리스트보다 적은 메모리 사용
- 정의후에는 변하지 않는 내부 값




## 실습

1. 문자열 'Fastcampus'를 리스트, 튜플 타입으로 형변환하여 새 변수에 할당한다.

```
s = 'Fastcampus'
l = list(s)
t = tuple(s)

l
['F', 'a', 's', 't', 'c', 'a', 'm', 'p', 'u', 's']

t
('F', 'a', 's', 't', 'c', 'a', 'm', 'p', 'u', 's')
```

2. 1번에서 할당한 리스트, 튜플 변수를 이용해 다시 문자열을 만든다.

```
','.join(l)

Fastcampus

```

## 딕셔너리(dictionary)

Key-Value형태로 항목을 가지는 자료구조.


#### 딕셔너리 생성

```python
>>> empty_dict1 = {}
>>> empty_dict2 = dict()
>>> champion_dict = {
... 'Lux': 'the Lady of Luminosity',
... 'Ahri': 'the Nine-Tailed Fox',
... 'Ezreal': 'the Prodigal Explorer',
... 'Teemo': 'the Swift Scout',
... }
```

#### 형변환

**dict** 함수를 사용, 두 값의 시퀀스(리스트 또는 튜플)을 딕셔너리로 변환 한다.

```python
>>> sample = [[1,2], [3,4], [5,6]]
>>> dict(sample)
{1: 2, 3: 4, 5: 6}
```

#### 항목 찾기/추가/변경 [key]

```
>>> champion_dict['Lux']
'the Lady of Luminosity'
>>> champion_dict['Sona'] = 'Maven of the Strings'
>>> champion_dict['Lux'] = 'Demacia'
```


#### 결합 (update)

```
>>> item_dict = {
... 'Doran\'s Ring': 400,
... 'Doran\'s Blade': 450,
... 'Doran\'s Shield': 450,
... }
>>> com_dict = {}
>>> com_dict.update(champion_dict)
>>> com_dict.update(item_dict)
>>> com_dict
```

서로 같은 키가 있을 경우, update에 주어진 딕셔너리의 값이 할당된다.




#### 삭제 (del)

```
>>> del com_dict['Doran\'s Blade']
>>> del com_dict['Doran\'s Ring']
>>> del com_dict['Doran\'s Shield']
```


#### 전체 삭제 (clear)

전체 항목을 삭제

```
com_dict.clear()

```

일부삭제

```
champion_dict['Sona']
```

#### in으로 키 검색

True/False를 반환한다.

```
'Lux' in champion_dict
```

#### 키 또는 값 얻기

**keys()**  
모든 키 얻기

**values()**  
모든 값 얻기

**items()**  
모든 키-값 얻기 (튜플로 반환)

```
champion_dict.items()


list(champion_dict.items())[0]
list(champion_dict.items())[0][0]
list(champion_dict.items())[0][1]
```

#### 복사

**copy()**  






## 셋(Set)

셋은 키만 있는 딕셔너리와 같으며, 중복된 값이 존재할 수 없다.


#### 셋 생성

```python
>>> empty_set = set()
>>> champions = {'lux', 'ahri', 'ezreal'}
```

#### 형변환

문자열, 리스트, 튜플, 딕셔너리를 셋으로 변환할 수 있으며, 중복된 값이 사라진다.
(순서가 사라지며 중복된 값 또한 사라진다.)

```
>>> set('ezreal')
{'e', 'z', 'a', 'l', 'r'}
```

```
>>> set(champion_dict)
{'Ahri', 'Lux', 'Ezreal', 'Sona', 'Teemo'}
```
딕셔너리는 키만 남는다.

#### 집합 연산

연산자|설명
---|---
\|	|	합집합(Union)
&	|	교집합(Intersection)
\-	|	차집합(Difference)
^	|	대칭차집합(Exclusive)
<=	|	부분집합(Subset)
<	|	진부분집합(Proper subset)
\>=	|	상위집합(Superset)
\>	|	진상위집합(Proper superset)

```
>>> A = {1,2,3,4,5}
>>> B = {4,5,6,7,8,9}
>>> C = {4,5,6}
>>> A|B
>>> A&B
>>> A-B
>>> B-A
>>> A^B
>>> A <= B
>>> C <= B
>>> C < B
>>> B <= B
>>> B < B
```

## 실습

1. 6가지 색상의 영어 키, 한글 값을 갖는 딕셔너리(colors)를 생성한다. (red, green, blue, yellow, black, white)

```
colors = {
          'red':'빨강',
          'green':'초록',
          'blue':'파랑',
          'yellow':'노랑',
          'black':'검정',
          'white':'흰색',
          }
```

2. colors에서 blue키의 값을 출력한다.

```
colors['blue']
```
3. colors를 셋(Set)으로 만들어 colors_set변수에 할당한다.

```
colors_set=set()

set(colors)

또는

colors_set=set(colors)

```

4. colors_set에 `purple`이 존재하는지 확인한다.

```
'purple' in colors_set
```

5. `[2,4,3,7,6,8,4,6,5,3,2,5,6,7,3]`에서 중복된 값을 없애고, 오름차순으로 정렬한 `list`를 반환한다.


```
l=[2,4,3,7,6,8,4,6,5,3,2,5,6,7,3]

s=set(l)
s

l2=list(s)

l2

l2.sort()

```


6. 2차원 딕셔너리인 `lol`을 만든다.
	- `lol`딕셔너리의 `champions`키에 셋(Set)을 이용해 `lux`, `ahri`, `ezreal`을 할당하고,

	```
	lol = dict()
	lol['champions']={'lux','ahri','ezreal'}
	
	```

	
	- `lol`딕셔너리의 `items`키에 아래의 각 항목들을 딕셔너리를 이용해 리스트로 할당한다.
		- Key: Doran Ring, Value: 400
		- Key: Doran Blade, Value: 450

```
lol['items']=[]
lol['items'].append({'Doran Ring':400})
lol['items'].append({'Doran Blade':450})

or

lol = {
'champions':{'ahri','ezreal','lux'},
'items':[
{'Doran Ring':400},
{'Doran Blade':450},
]
}

```
		
		
7. `x = {1,2,3,4,5,6,8}`, `y={4,5,6,9,10,11}`, `z={4,6,8,9,7,10,12}`일 때,
	- x,y,z의 교집합에 해당하는 숫자는?
	- y,z의 교집합이며 x에는 속하지 않는 숫자는?
	- x에만 속하고 y,z에는 속하지 않는 숫자는?


---

- 대괄호 : 리스트
- 중괄호 :
	- 셋 = 키값만<br>
	- 딕셔너리 = 키 value
- 소괄호 : 튜플

---


# 제어문

## if, elif, else(조건문)

if와 else는 조건이 참인지 거짓인지 판단하는 파이썬 선언문(Statement)이며, elif는 else내의 if를 중첩해야 할 때 사용한다.

```
if 조건:
	조건이 참일 경우
else:
	조건이 거짓일 경우
```

```
if 조건1:
	조건1이 참일 경우
else:
	조건1이 거짓일 경우
	
	if 조건2:
		조건1은 거짓이나, 조건2는 참일 경우
	else:
		조건1,2가 모두 거짓일 경우
```
위 코드는 아래와 같이 `elif`로 줄여쓸 수 있다.

```
if 조건1:
	조건1이 참일 경우
elif 조건2:
	조건1은 거짓이나, 조건2가 참일 경우
else:
	조건1,2가 모두 거짓일 경우
```


## 조건표현식

```
참일경우 if 조건식 else 거짓일 경우
```

`is_holiday`에 `True`또는 `False`값을 할당한 후, `if`문과 `조건표현식`을 사용해서 각각 'Good'과 'Bad'를 출력하는 코드를 짜본다.

```
is_holyday = True

print('Good') if is_holyday else print('Bad')

```

```
In [187]: if[]:
     ...:     print('list')
     ...: else:
     ...:     print('empty list')
     ...:     
empty list

In [188]: if['a']:
     ...:     print('list')
     ...: else:
     ...:     print('empty list')
     ...:     
list

```


## 중첩 조건표현식

```
# 조건이 2개일 경우
조건1이 참일경우 if 조건1 else 조건1은 거짓이나 조건2가 참일경우 if 조건2 else 조건1,2가 모두 거짓일 경우
```

`vacation`에 1에서 10중 아무 값이나 할당 후, `if, elif, else`문과 `중첩 조건표현식`을 사용해서 각각 `vacation`이 7이상이면 'Good', 5이상이면 'Normal', 그 이하면 'Bad'를 출력하는 코드를 짜본다.

```
print('Good') if vacation >= 7 else print('Normal') if vacation >= 5 else print('Bad')
```


## for문 (조건에 따른 순회)

#### 기본형태

시퀀스형 데이터를 순회하고자 할 때 사용한다.

```
for 항목 in 순회가능(iterable)객체:
   <항목을 사용한 코드>
```

iterable한 객체에는 문자열, 튜플, 딕셔너리, 셋 등이 있다.

```
>>> champion_list = ['lux', 'ahri', 'ezreal', 'zed']
>>> for champion in champion_list:
...   print(champion)
... 
lux
ahri
ezreal
zed
```

딕셔너리에서 키나 값을 순회할 때는, iterable한 객체의 위치에 dict.keys()나 dict.values()를 사용한다.  
키, 값을 모두 순회할 때에는 dict.items()를 사용한다.

```
In [190]: for item in ['a','b','c']:
     ...:     print(item)
     ...:     
a
b
c

In [191]: for char in 'Lux':
     ...:     print(char)
     ...:     
L
u
x

```

```
In [192]: for value in champion_dict.values():
     ...:     print(value)
     ...:     
the Lady of Luminosity
the Nine-Tailed Fox
the Prodigal Explorer
the Swift Scout
Haven of the Strings

In [193]: for item in champion_dict.items():
     ...:     
     ...:     print(item)
     ...: 
('Lux', 'the Lady of Luminosity')
('Ahri', 'the Nine-Tailed Fox')
('Ezreal', 'the Prodigal Explorer')
('Teemo', 'the Swift Scout')
('Sona', 'Haven of the Strings')



In [196]: for key, value in champion_dict.items():
     ...:     print('Champion:{}, Description:{}'.format(key, value))
     ...:     
Champion:Lux, Description:the Lady of Luminosity
Champion:Ahri, Description:the Nine-Tailed Fox
Champion:Ezreal, Description:the Prodigal Explorer
Champion:Teemo, Description:the Swift Scout
Champion:Sona, Description:Haven of the Strings


```

#### 중첩

```
for 항목1 in iterable객체1:
  iterable객체1을 순회하며 실행할 코드
  for 항목2 in iterable객체2:
    iterable객체1 내부에서 새로운 iterable객체2를 순회하며 실행할 코드
```

아래의 item / inner_item 그리고 x/y 등의 변수는 특별한 의미는 없지만 이해하며 구분할 수 있게 이름을 지어 줘야한다.

```
In [197]: l=[
     ...: ['a','b','c'],
     ...: ['1','2','3'],
     ...: ['A','B','C']
     ...: ]

In [198]: for item in l:
     ...:     for inner_item in item:
     ...:         print(inner_item)
     ...:         
a
b
c
1
2
3
A
B
C


In [199]: for x in l:
     ...:     for y in x:
     ...:         print(y)
     ...:         
a
b
c
1
2
3
A
B
C


```

#### 중단하기 (break)

데이터를 순회하던 중, 특정 조건에서 순회를 멈추고 반복문을 빠져나갈 때 사용한다.

```
for 항목 in iterable객체:
  (반복문을 중단하고 싶을때)break
```

```

In [200]: lux= 'the Lady of Luminosity'

In [201]: for char in lux:
     ...:     print(char)
     ...:     if char =='p':
     ...:         break
     ...: else:
     ...:     print('not break')
     ...:     
t
h
e
 
L
a
d
y
 
o
f
 
L
u
m
i
n
o
s
i
t
y
not break

```



#### 건너뛰기 (continue)

데이터를 순회하던 중, 반복문을 중단하지 않고 다음 반복으로 건너뛸 때 사용한다.

```
for 항목 in iterable객체:
  (현재의 반복을 중간에 그만두고 다음 반복으로 건너뛰고 싶을 때)continue
```

#### break확인 (else)

for문으로 데이터를 순회하던 중, break문이 호출되지 않고 반복문이 종료되면 else문이 실행된다.

```
for 항목 in iterable객체:
  pass
else:
  break가 한 번도 호출되지 않았을 경우의 코드
```




#### 여러 시퀀스 동시순회 (zip)

```
>>> fruits = ['apple', 'banana', 'melon']
>>> colors = ['red', 'yellow', 'green', 'purple']
>>> for fruit, color in zip(fruits, colors):
...   print('fruit:', fruit, ' color:', color)
... 
fruit: apple  color: red
fruit: banana  color: yellow
fruit: melon  color: green
```

zip으로 묶은 시퀀스들 중, 가장 짧은 시퀀스가 완료되면 순회가 종료된다.

zip을 사용하면 여러 시퀀스로부터 튜플을 만들 수 있다.

```
>>> list(zip(fruits, colors))
```

zip으로 반환되는 것은 리스트가 아닌 zip클래스 형태의 iterable객체이기 때문에, 리스트 형태로 사용하려면 list()함수를 사용해준다.

dict()함수를 사용할 경우 딕셔너리 객체가 만들어지게 된다.

#### 숫자 시퀀스 생성 (range)

range()함수는 특정 범위의 숫자 스트림 데이터를 반환한다.

```
range(start, stop, step)
```

zip과 마찬가지로, iterable한 객체를 반환하며, 따라서 for문을 순회할 수 있다.

```
>>> for x in range(0, 10):
...   print(x)
... 
0
1
2
3
4
5
6
7
8
9
```


```
In [212]: fruits = ['apple','banana','melon']

In [213]: colors = 'red yellow green purple'.split()

In [214]: colors
Out[214]: ['red', 'yellow', 'green', 'purple']

In [215]: len(fruits)
Out[215]: 3

In [216]: len(colors)
Out[216]: 4

In [217]: for index in range(len(fruits)):
     ...:     print(index)
     ...:     
0
1
2


In [220]: for index in range(len(fruits)):
     ...:     print(fruits[index])
     ...:     print(colors[index])
     ...:     
apple
red
banana
yellow
melon
green

In [221]: for fruit, color in zip(fruits, colors):
     ...:     print(fruit)
     ...:     print(color)
     ...:     
apple
red
banana
yellow
melon
green

In [222]: t = zip(fruits,colors)

In [223]: t
Out[223]: <zip at 0x105cbd3c8>

In [224]: z = zip(fruits, colors)

In [225]: t = tuple(z)

In [226]: t
Out[226]: (('apple', 'red'), ('banana', 'yellow'), ('melon', 'green'))

In [227]: l= tuple(z)

In [228]: l
Out[228]: ()

In [229]: z = zip(fruits, colors)

In [230]: l = list(z)

In [231]: l
Out[231]: [('apple', 'red'), ('banana', 'yellow'), ('melon', 'green')]

In [232]: t = tuple(z)

In [233]: t
Out[233]: ()


```