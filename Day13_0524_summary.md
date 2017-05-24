# 예외처리

오류가 발생하면 프로그램은 에러를 출력하며 강제종료되거나, 원하지 않는 동작을 한다.

이러한 오류를 안전하게 처리하고, 바로 강제종료 되지 않고 오류 발생 후 처리할 루틴을 실행하고자 할 때 예외처리를 사용한다.

##### 가장 기본적인 형태

```python
try:
	시도할 코드
except:
	에러가 발생했을 경우 실행할 코드
```

- 리스트의 범위를 넘어간 에러를 테스트해본다.

```
import random
try:
    l = random.sample(range(10), 10)
    print(l[20])

except IndexError:
    print('Index Error')

print('Program Terminated')
```

##### 여러가지 예외를 구분할 경우
```python
try:
	시도할 코드
except <예외 클래스1>:
	에러클래스 1에 해당할 때 실행할 코드
except <예외 클래스2>:
	...
except <예외 클래스3>:
	...
```

- 리스트의 범위를 넘어간 경우, `IndexError`를 명시적으로 처리해본다
- 딕셔너리의 키가 없는 경우, `KeyError`를 명시적으로 처리해본다

```
import random
l = random.sample(range(10),10)
d = {'apple':'red'}

try:
    print(l[20])
    prnt(d['yello'])

except IndexError:
    print(IndexError)

except KeyError:
    print(KeyError)

print('Program Terminated')
```

##### 예외사항을 변수로 사용할 경우
```python
try:
	시도할 코드
except <예외클래스> as <변수명>:
	<변수명>을 사용한 코드
```

- 위 예외에서 변수로 전달된 예외객체를 출력해본다

```
import random
l = random.sample(range(10),10)
d = {'apple':'red'}

try:
    print(l[20])
    prnt(d['yello'])

except IndexError as e:
    print(e)
    print(dir(e))
    print(e.args)

except KeyError as e:
    print(e)
    print(dir(e))
    print(e.args)

print('Program Terminated')
```


## try ~ else

`else`문은 `try`이후 예외가 발생하지 않을 경우 실행된다.

```Python
try:
	시도할 코드
except:
	예외 발생시 실행 코드
else:
	예외가 발생하지 않았을 시 실행할 코드
```

## try ~ finally

`finally`문은 `try`이후 예외가 발생하건, 하지않건 무조건 마지막에 실행된다.

## 예외 발생시키기

예외를 발생시킬때는 `raise`구문을 사용한다.

## 예외 만들기

내장 클래스 `Exception`을 상속받아 커스텀 예외를 만들 수 있다.
초기화 메서드에서 예외에서 처리할 데이터를 받고, `print`문으로 사용되고 싶다면 `__str__`메서드를 오버라이드 해준다.


1. 정규 표현식으로 검사했을 때 일치하는 패턴이 없을 경우,
   발생할 NotMatchedException을 정의.  
   1-1.  Exception을 상속    
   1-2. \_\_init\_\_ 초기화 메서드에 패턴 문자열과 소스 문자열을 받도록 함    
   1-3. \_\_str\_\_ 메서드가 일치하는 결과가 없다는 문자열을 리턴하도록 함    
   
2. 패턴문자열과 소스 문자열을 매개변수로 갖는 search\_from\_source 함수를 정의하고
   re.sesarch에 소스 문자열을 전달했을 때,
   MatchObject를 찾지 못하면 NoMatdhedException을 발생시킴
   
3. tyr~except구문에서 위 함수를 실행해 예외를 발생 시킴

4. 위 구문에 else절을 추가해서 예외가 발생하지 않았을 경우의 검색결과를 출력

5. 위 구문에 finally절을 추가해서 프로그램이 끝났음을 출력

```
"""
1. 정규 표현식으로 검사했을 때 일치하는 패턴이 없을 경우,
   발생할 NotMatchedException을 정의
   1-1. Exception을 상속
   1-2. __init__ 초기화 메서드에 패턴 문자열과 소스 문자열을 받도록 함
   1-3. __str__ 메서드가 일치하는 결과가 없다는 문자열을 리턴하도록 함
2. 패턴문자열과 소스 문자열을 매개변수로 갖는 search_from_source 함수를 정의하고
   re.sesarch에 소스 문자열을 전달했을 때,
   MatchObject를 찾지 못하면 NoMatdhedException을 발생시킴
3. tyr~except구문에서 위 함수를 실행해 예외를 발생 시킴
4. 위 구문에 else절을 추가해서 예외가 발생하지 않았을 경우의 검색결과를 출력
5. 위 구문에 finally절을 추가해서 프로그램이 끝났음을 출력
"""
import re

class NotMatchedException(Exception):
    """
    pattern, source를 받아 매치되지 않았음을 알려주는 Exception클래스
    """
    def __init__(self, pattern_string, source_string):
        self.pattern_string = pattern_string
        self.sources_string = source_string

    def __str__(self):
        return 'Pattern "{}" is not matched in source "{}"'.format(
            self.pattern_string,
            self.sources_string
        )

def search_from_source(pattern_string, source_string):
    m = re.search(pattern_string, source_string)
    if m:
        return m
    raise NotMatchedException(pattern_string, source_string)



try:
    source = 'Lux, the Lady of Luminocity'
    pattern_string = r'L\w{2}\b'
    m = search_from_source(pattern_string, source)


except NotMatchedException as e:
    print(e)

else:
    print('Search result : {}'.format(m.groups()))

finally:
    print('--- Search End ---')

```








# 파일 다루기

프로그램이 실행되는 동안 데이터는 휘발성 기억장치인 메모리(RAM)에 저장된다. 작업중인 데이터를 저장하거나, 이미 저장되어있는 데이터를 불러오기 위해서는 하드디스크나 SSD에 파일을 쓰거나 읽는 과정이 필요하다.

## 파일 열기

```python
변수 = open(파일명, 모드)
```

내장함수 `open()`을 사용하며, 파일명은 파일의 경로를 나타낸다.

-

**모드의 첫 번째 글자**

모드|설명
---|---
r|읽기
w|쓰기 (파일이 이미 존재할 경우 덮어쓴다)
x|쓰기 (단, 파일이 존재하지 않을 경우에만)
a|추가 (파일이 존재할 경우 파일의 끝부터 쓴다)

**모드의 두 번째 글자**

모드|설명
---|---
t 또는 없음|텍스트타입
b|이진데이터 타입


**이진데이터**  
이진형식(0과 1)로 이루어진 **텍스트를 제외한 모든 데이터**를 말함.  
텍스트 역시 이진데이터의 일종이지만, 데이터의 구조가 인코딩과 개행문자 등 텍스트 형태로 바로 사용할 수 있게 되어있다는 차이가 있다.


파일을 열고 사용한 뒤에는 파일을 닫아야한다.

## 파일 쓰기: write()

```python
>>> skills = '''Illumination
... Light Binding
... Prismatic Barrier
... Lucent Singularity
... Final Spark'''
>>>
>>> len(skills)
75
```

```python
>>> f = open('skills.txt', 'wt')
>>> f.write(skills)
75
>>> f.close()
```

`skills.txt`파일에 내용을 쓴다.

만약 문자열이 클 경우, 일정 단위로 나누어서 파일에 쓰는 방식을 사용한다.

```python
>>> f = open('skills.txt', 'wt')
>>> size = len(skills)
>>> offset = 0
>>> chunk = 30
>>> while True:
...   if offset > size:
...     break
...   f.write(skills[offset:offset+chunk])
...   offset += chunk
...
30
30
15
```

덮어쓰기를 방지하려면 `wt`대신 `xt`를 사용해서 이미 존재하는 파일은 쓸 수 없도록 처리한다.

```python
>>> try:
...   f = open('skills.txt', 'xt')
...   f.write('Other contents')
... except FileExistsError:
...   print('skills.txt exists')
...
skills.txt exists
```

## 텍스트파일 전체 읽기: read()

`read()`함수는 전체 파일을 한 번에 가져오므로, 메모리 사용에 유의해야한다.

```python
>>> f = open('skills.txt', 'rt')
>>> skills = f.read()
>>> f.close()
>>> len(skills)
75
```

한 번에 읽을 크기를 제한하고 싶다면, 인자로 최대 문자수를 입력해준다.

```python
>>> f = open('skills.txt', 'rt')
>>> chunk = 30
>>> while True:
...   part = f.read(chunk)
...   if not part:
...     break
...   skills += part
...
>>> f.close()
>>> len(skills)
75
```

파일을 전부 읽으면 빈 문자열이 리턴되고, `if`문에서 `False`로 판단하여 루프가 끝난다.




```
skills = '''Illumination
Light Binding
Prismatic Barrier
Lucent Singularity
Final Spark'''

len(skills)

f = open('skills.txt', 'wt')
f.write(skills)
f.close()


try:
    f = open('skills.txt', 'xt')
except FileExistsError:
    print('File is already exist')
print('Program Terminate')


f = open('skills.txt', 'rt')
skills = f.read()
f.close()
print(skills)
```



## 텍스트파일 줄 단위 읽기: readline()

```python
>>> skills = ''
>>> f = open('skills.txt', 'rt')
>>> while True:
...   line = f.readline()
...   if not line:
...     break
...   skills += line
...
>>> f.close()
>>> len(skills)
75
```
파일을 라인단위로 읽어 문자열에 저장한다.

빈 라인(`\n`)은 길이가 1이며, 파일의 끝에서만 완전히 빈 문자열 (`''`)을 리턴한다.


## 이터레이터를 사용한 텍스트 파일 읽기

```python
>>> skills = ''
>>> f = open('skills.txt', 'rt')
>>> for line in f:
...   skills += line
...
>>> f.close()
>>> len(skills)
75
```

`readline()`을 호출한 것과 같은 결과를 보인다.

## 텍스트파일을 줄 단위 문자열 리스트로 리턴: readlines()

```python
>>> f = open('skills.txt', 'rt')
>>> lines = f.readlines()
>>> f.close()
>>> for line in lines:
...   print(line)
...
Illumination

Light Binding

Prismatic Barrier

Lucent Singularity

Final Spark
>>> for line in lines:
...   print(line, end='')
...
Illumination
Light Binding
Prismatic Barrier
Lucent Singularity
Final Spark>>>
```

각 줄에 줄바꿈(`\n`)문자가 있으므로 `print()`함수에 `end`인자를 주어 줄바꿈을 없앨 수 있다.

마지막 라인에는 줄바꿈이 없으므로 인터프리터 프롬프트가 같은 줄에 표시된다.


```
skills = '''Illumination
Light Binding
Prismatic Barrier
Lucent Singularity
Final Spark'''

len(skills)

f = open('skills.txt', 'wt')
f.write(skills)
f.close()


try:
    f = open('skills.txt', 'xt')
except FileExistsError:
    print('File is already exist')
print('Program Terminate')


f = open('skills.txt', 'rt')
fl = f.readlines()
print(fl)

```

## 자동으로 파일 닫기: with

연 파일을 닫지 않을 경우, 파이썬에서는 해당 파일이 더 이상 사용되지 않을 때 파일을 자동으로 닫아준다.

다만 메인프로그램이나 오랫동안 동작하는 함수에서 파일을 열 경우, 명시적으로 닫아주지 않을 경우 문제가 발생한다.

```
with 표현식 as 변수
```
위의 구문을 사용하면, `with`문 내부에서 파일을 사용한 후 구문이 종료되면 자동으로 파일을 닫아주므로 프로그래밍 단계에서 일일이 파일을 닫아주는 부분에 신경쓰지 않아도 된다.

```python
>>> with open('skills.txt', 'wt') as f:
...   f.write(skills)
```

## 이진데이터 다루기

쓰거나 읽을 때, `t`대신 `b`인자를 사용하면 된다.

---

#크롤링
> 참고도서   
>**파이썬을 이용한 웹 크롤러**

## HTML Parser

```
import re

f= open('example.html')
html = f.read()


pattern_div = re.compile(r'<div.*?>([.\w\W]*?)</div>')
m = re.search(pattern_div, html)
div = m.group(1)

pattern_p = re.compile(r'<p.*?>([.\w\W]*?)</p>')
m_list = re.finditer(pattern_p, div)
for m in m_list:
    print(m.group(1))
```

```
import re

f= open('example.html')
html = f.read()

pattern_tag_base = r'<{tag}.*?>([.\w\W]*?)</{tag}>'

def find_tag_content(tag, source):
    """
    주어진 tag의 내용을 리턴
    :param tag: 검색을 원하는 태그 ex)'div'
    :param source: 태그를 검색 할 전체 문자열 
    :return: 주어진 tag의 내용 문자열
    """

    pattern = re.compile(pattern_tag_base.format(tag=tag))
    m = re.search(pattern, source)
    if m:
        return m.group(1)
    return None


# html 문자열 변수에서 'div'태그의 내용을 찾아 변환한느 함수 실행
div = find_tag_content('div', html)
# print(div)


p = find_tag_content('p', div)
print(p)


#원리
pattern_div = re.compile(r'<div.*?>([.\w\W]*?)</div>')
m = re.search(pattern_div, html)
div = m.group(1)


pattern_p = re.compile(r'<p.*?>([.\w\W]*?)</p>')
m_list = re.finditer(pattern_p, div)


```



```
import re

f= open('example.html')
html = f.read()

pattern_tag_base = r'<{tag}.*?>\s*([.\w\W]*?)\s*</{tag}>'

def find_tag(tag, source):
    """
    주어진 tag 문자열, 또는 문자열의 리스트 반환
    :param tag: 검색을 원하는 태그 ex)'div'
    :param source: 태그를 검색 할 전체 문자열 
    :return: 검색 결과가 1개일 경우에는 tag 문자열, 2개 이상 일 경우에는 tag 문자열의 리스트
    """

    pattern = re.compile(pattern_tag_base.format(tag=tag))
    m_list = re.finditer(pattern, source)
    if m_list:
        return_list = [m.group() for m in m_list]
        return return_list if len(return_list) > 1 else return_list[0]
    return None

# pattern_tag_content = r'^<.*?>([.\w\W]*?)</.*?>$'
pattern_tag_content = r'<.*?>([.\w\W]*?)</.*?>'

def get_tag_content(tag_string):
    """
    tag 문자열의 주어졌을 때, 해당 tag의 내용을 리턴
    :param tag_string: tag_string: <tag>내용</tag>형태의 문자열
    :return: 위 형태에서 '내용'부름
    """
    pattern = re.compile(pattern_tag_content)
    m = re.search(pattern, tag_string)
    if m:
        return m.group(1)
    return None


# html 문자열 변수에서 'div'태그의 내용을 찾아 변환한느 함수 실행
div = find_tag('div', html)
p_list = find_tag('p', div)
print(p_list)
for p in p_list:
    print(get_tag_content(p))

div_content = get_tag_content(div)
print(div_content)

# p = find_tag('p', div)
# print(p)
#

#원리
pattern_div = re.compile(r'<div.*?>([.\w\W]*?)</div>')
m = re.search(pattern_div, html)
div = m.group(1)


pattern_p = re.compile(r'<p.*?>([.\w\W]*?)</p>')
m_list = re.finditer(pattern_p, div)



```

* 위의 코드를 객체화시켜 하나의 class모듈화하여 단순화시키자

```
import re


class Node(object):
    """
    HTML태그 하나를 가지는 클래스
        내부에 다른 클래스를 가질 수 있음
        가장 큰 범위는 <html></html>
    """

    _pattern_tag_base = r'<{tag}.*?>\s*([.\w\W]*?)\s*</{tag}>'
    _pattern_tag_content = r'<[^!]*?>([.\w\W]*)</.*?>'

    def __init__(self, source):
        self.source = source

    def __str__(self):
        return '{}\n{}'.format(
            super().__str__(),
            self.source
        )

    def find_tag(self, tag):
        """
        주어진 tag 문자열, 또는 문자열의 리스트 반환
        :param tag: 검색을 원하는 태그 ex)'div'
        :param source: 태그를 검색 할 전체 문자열 
        :return: 검색 결과가 1개일 경우에는 tag 문자열로 만든 Node객체, 2개 이상 일 경우에는 tag 문자열로 만든 Node의 리스트
        """
        pattern = re.compile(self._pattern_tag_base.format(tag=tag))
        m_list = re.finditer(pattern, self.source)
        if m_list:
            return_list = [Node(m.group()) for m in m_list]
            return return_list if len(return_list) > 1 else return_list[0]
        return None

    @property
    def content(self):
        """
        Node인스턴스의 내용을 리턴
        :return: Node(태그)내부의 내용 문자열을 리턴
        """
        pattern = re.compile(self._pattern_tag_content)
        m = re.search(pattern, self.source.strip())
        if m:
            return m.group(1).strip()
        return None

    @property
    def class_(self):
        """
        해당 Node가 가진 class속성의 value를 리턴 (문자열)
        :return: 
        """
        pass


with open('example.html') as f:
    html = Node(f.read())

node_div = html.find_tag('div')
node_p_list = node_div.find_tag('p')
for node_p in node_p_list:
    print(node_p.content)
```



