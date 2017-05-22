##jupyter설치
>jupyter는 작업폴더내에 설치해야한다.


```
>> pip install jupyter
>> jupyter notebook
```
```
작업중 실행 : ctrl + enter : 줄바뀜 없이 실행
		   shift + enter : 새로운 줄이 생기며 실행
```

##iTerm2설치
>google에서 설치

#### 스코프(영역)

파이썬에서는 코드 작성 시, 각 함수마다 독립적인 스코프(영역)을 가진다.  
메인 프로그램(현재 동작하는 프로그램의 최상위 위치)의 영역은 전역 영역(Global Scope)라고 하며, 전역 스코프 내부에서 독립적인 영역을 갖고 있는 경우에는 지역 영역(Local Scope)라고 부른다.

아래 코드의 경우, `show_global_champion`함수 내부의 영역은 별개의 로컬 스코프를 가지며, `champion`변수는 전역 영역의 것을 가져와 출력하는것을 볼 수 있다.

```python
champion = 'Lux'

def show_global_champion():
    print('show_global_champion : {}'.format(champion))

show_global_champion()
print('print champion : {}'.format(champion))
```

위 코드를 아래와 같이 변경 후, 실행 해 본다.

```python
champion = 'Lux'

def show_global_champion():
    print('show_global_champion : {}'.format(champion))

def change_global_champion():
    print('before change_global_champion : {}'.format(champion))
    champion = 'Ahri'
    print('after change_global_champion : {}'.format(champion))

show_global_champion()
change_global_champion()
```


`change_global_champion`함수에서 오류가 발생한다.

첫 번째 코드에서는 `champion`변수가 함수의 로컬 스코프에 존재하지 않기 때문에 글로블 스코프에서 해당 변수를 찾아 출력하였으나, 이번 코드에서는 내부에 또다른 `champion`변수가 존재하기 때문에 할당하기 전인 변수를 사용한 것으로 판단하여 프로그램에서 오류를 발생시킨다.

이름이 같은 두 변수가 다른 객체임을 내장함수 `id`를 사용해 확인해보자.

또한, 각 영역에 해당하는 데이터들은 `locals()`함수를 사용해 확인 할 수 있으며, 전역 영역의 데이터들은 `globals()`함수를 사용한다.


#### 스코핑 룰

스코프는 지역(Local), 전역(Global)외에도 내장(Built-in)영역이 존재하며, 내장영역이 가장 바깥, 그 내부에 전역, 그 내부에 지역 순으로 정의된다.  
분리된 영역에서, 외부 영역에서는 내부 영역의 데이터를 사용할 수 없지만 내부 영역에서는 자신의 외부 영역에 있는 데이터를 참조할 수 있다.  
(반대의 경우에는 함수의 인자로 데이터를 전달한다)

```
>> globals()
```


#### 내장 함수와 내장 영역

`print`, `dict`등 지정하지 않고 사용했던 내장 함수들은 위 스코핑 룰의 내장 스코프에 존재하는 함수들이다.  
전역스코프의 `__builtin__`변수에 할당되어 있으며, 전역 스코프에서는 해당 변수의 내부를 참조할 수 있도록 파이썬이 시작될 때 자동으로 처리된다.

확인시 `dir`함수를 사용하며, `dir`함수는 해당 객체가 사용 가능한 속성 및 함수들을 리스트 형태로 나타내준다.

```
>> dir(__builtin__)
```

#### 로컬 스코프에서 글로벌 스코프의 변수를 사용

```python
champion = 'Lux'

def change_global_champion():
    champion = 'Ahri'
    print('after change_global_champion : {}'.format(champion))

change_global_champion()
print('print global champion : {}'.format(champion))
```

이 경우, 위의 `show_global_champion`함수와는 다르게 `change_global_champion`함수는 `champion`변수에 새로운 값을 대입한다.  
만약 로컬 스코프에서 글로벌 스코프의 변수를 변경해야 한다면, 해당 변수가 로컬 스코프에 생성되는 것이 아닌 글로벌 영역에 이미 존재하는 값을 사용함을 명시해주어야 한다.

```python
champion = 'Lux'

def change_global_champion():
    global champion
    champion = 'Ahri'
    print('after change_global_champion : {}'.format(champion))

change_global_champion()
print('print global champion : {}'.format(champion))
```

파이썬에서는 한 스코프에서 동일한 이름을 가진 두 스코프의 변수를 사용할 수 없음을 기억해야 한다.

#### 내부함수에서의 로컬 스코프 (nonlocal)
```
champion = 'Lux'

def local1():
    champion = 'Ahri'
    print('local1 locals() : {}'.format(locals()))
    
    def local2():
        champion = 'Ezreal'
        print('local2 locals():', locals())
        
    local2()
local1()

```
```
local1 locals() : {'champion': 'Ahri'}
local2 locals(): {'champion': 'Ezreal'}
```

```python
champion = 'Lux'

def local1():
    champion = 'Ahri'
    print('local1 locals() : {}'.format(locals()))

    def local2():
        champion = 'Ezreal'
        print('local2 locals() : {}'.format(locals()))
    local2()

print('global locals() : {}'.format(locals()))
local1()
```

로컬 스코프 내부에는 또 다른 로컬 스코프가 존재할 수 있다.  
전역 스코프가 아닌, 자신의 바로 바깥 영역의 로컬 스코프(자신보다 한 단계 위의 로컬 스코프)의 데이터를 참조하고자 한다면, `nonlocal`키워드를 사용한다.

```python
champion = 'Lux'

def local1():
    champion = 'Ahri'
    print('local1 locals() : {}'.format(locals()))

    def local2():
        nonlocal champion
        champion = 'Ezreal'
        print('local2 locals() : {}'.format(locals()))
    local2()
    print('local1 locals() : {}'.format(locals()))

print('global locals() : {}'.format(locals()))
local1()
```

```
In [33]:

# 로컬 스코프에서 global키워드를 사용

champion = 'Lux'
print('champion variable init, id:', id(champion))

def change_global_champion():
    global champion
    champion = 'Ahri'
    print('champion variable edit in local, id:', id(champion))
    print('in_change_global_champion: {}'.format(champion))

change_global_champion()
print('champion variable after edit, id:', id(champion))
print('after_change_global_champion: {}'.format(champion))

--------------------------------------
champion variable init, id: 4568627216
champion variable edit in local, id: 4568628504
in_change_global_champion: Ahri
champion variable after edit, id: 4568628504
after_change_global_champion: Ahri



In [39]:
# 다중 로컬 스코프에서 global 키워드 사용

champion = 'Lux'

def local1():
    global champion
    champion = 'Ahri'
    print('local1 locals():', locals())
    
    def local2():
        global champion
        champion = 'Ezreal'
        print('local2 locals():', locals())

    local2()
local1()
print('global champion value:', globals()['champion'])

--------------------------------------
local1 locals(): {}
local2 locals(): {}
global champion value: Ezreal




In [66]:
# nonlocal 키워드 사용 (변수는 str형)

champion = 'Lux'

def local1():
    def local2():
#         nonlocal champion
#         print('local2 before champion id:', id(champion))
        champion = 'Ezreal'
        print('local2 after champion id:', id(champion))
#         print('local2 locals():', locals())
#         print('local2 champion value:', locals().get('champion'))


    champion = 'Ahri'
#     print('local1 before champion value:', locals().get('champion'))
    print('local1 before champion id:', id(champion))
    local2()
    print('local1 after champion id:', id(champion))
#     print('local1 locals():', locals())
#     print('local1 after champion value:', locals().get('champion'))
local1()
# print('global champion value:', globals()['champion'])

--------------------------------------
local1 before champion id: 4568628504
local2 after champion id: 4568872696
local1 after champion id: 4568628504




In [68]:
# 상위영역의 변수가 리스트일경우
champion = ['Lux']

def local1():
    def local2():
        nonlocal champion
#         global champion
        print('local2 before champion id:', id(champion))
        # append를 이용하면 champion리스트 변수를 "사용" 한 것이 되므로 상위 스코프에서 가져온다
#         champion.append('Ezreal')
        # 새 리스트를 할당하면 champion리스트 변수를 새로 "할당" 한 것이 되므로 상위 스코프와 별개로 동작한다
        champion = ['Ezreal']
        print('local2 after champion id:', id(champion))
#         print('local2 locals():', locals())
#         print('local2 champion value:', locals().get('champion'))


    champion = ['Ahri']
#     print('local1 before champion value:', locals().get('champion'))
    print('local1 before champion id:', id(champion))
    local2()
    print('local1 after champion id:', id(champion))
#     print('local1 locals():', locals())
#     print('local1 after champion value:', locals().get('champion'))
local1()
# print('global champion value:', globals()['champion'])

--------------------------------------
local1 before champion id: 4569499144
local2 before champion id: 4569499144
local2 after champion id: 4569579336
local1 after champion id: 4569579336
```

#### global키워드와 인자(argument)전달의 차이

인자로 전달한 경우

```
global_level = 100
def level_add(value):
    value += 30
    print(value)

level_add(global_level)
print(global_level)
```

global키워드를 사용한 경우

```
global_level = 100
def level_add():
    global global_level
    global_level += 30
    print(global_level)

level_add()
print(global_level)
```

인자로 전달한 경우, 같은 객체를 가리키는 글로벌 변수 `global_level`과 매개변수 `value`가 존재한다.  
이 때, 매개변수인 `value`의 값을 변경하는 것은 `global_level`에는 영향을 주지 않는다.

global키워드의 경우 둘은 같은 변수이다.

하지만 리스트 변수가 전달된다면?



```
In [9]:
# global키워드와 인자(argument)전달의 차이
global_level = 100
print('initial_global id:', id(global_level))

# 인자 전달의 방법
def level_add(value):
    print('before_level_add_parameter id:', id(value))
    value += 30
    print('after_level_add_parameter id:', id(value))
    print('in_level_add, value:', value)


level_add(global_level)
print('after_level_add, value:', global_level)
print('after_level_add_global, id:', id(global_level))
--------------------
initial_global id: 4487118720
before_level_add_parameter id: 4487118720
after_level_add_parameter id: 4487119680
in_level_add, value: 130
after_level_add, value: 100
after_level_add_global, id: 4487118720



In[12]:
# global키워드와 인자(argument)전달의 차이
global_level = 100
print('initial_global id:', id(global_level))

# 인자 전달의 방법
def level_add(value):
    print('before_level_add_parameter id:', id(value))
    value += 30
    print('after_level_add_parameter id:', id(value))
    print('in_level_add, value:', value)
    return value


global_level = level_add(global_level)
print('after_level_add, value:', global_level)
print('after_level_add_global, id:', id(global_level))

# global 키워드 사용
def add_global_level():
    global global_level
    global_level +=30

add_global_level()
print('after_add_globa_level, value:', global_level)
print('after_add_global_level, id:', id(global_level))


---------------------------------------

initial_global id: 4487118720
before_level_add_parameter id: 4487118720
after_level_add_parameter id: 4487119680
in_level_add, value: 130
after_level_add, value: 130
after_level_add_global, id: 4487119680
after_add_globa_level, value: 160
after_add_global_level, id: 4487120640


In[13]:
# global키워드와 인자(argument)전달의 차이  list형 객체
global_level = [100]
print('initial_global id:', id(global_level))

# 인자 전달의 방법
def level_add(value):
    print('before_level_add_parameter id:', id(value))
    value[0] += 30
    print('after_level_add_parameter id:', id(value))
    print('in_level_add, value:', value)
    return value


global_level = level_add(global_level)
print('after_level_add, value:', global_level)
print('after_level_add_global, id:', id(global_level))

# global 키워드 사용
def add_global_level():
    global global_level
    global_level[0] +=30

add_global_level()
print('after_add_globa_level, value:', global_level)
print('after_add_global_level, id:', id(global_level))

-------------------------------------------

initial_global id: 4518638024
before_level_add_parameter id: 4518638024
after_level_add_parameter id: 4518638024
in_level_add, value: [130]
after_level_add, value: [130]
after_level_add_global, id: 4518638024
after_add_globa_level, value: [160]
after_add_global_level, id: 4518638024

```






#### 람다함수

한 줄 짜리 표현식으로 이루어지며, 반복문이나 조건문 등의 제어문은 포함될 수 없다.  
또한, 함수이지만 정의/호출이 나누어져 있지 않으며 표현식 자체가 바로 호출된다.

```python
lambda <매개변수> : <표현식>
```

```
# 함수의 정의
>>> def multi(x):
...   return x*x
... 

# 함수의 호출
>>> multi(5)
25

# 람다함수의 사용
>>> (lambda x : x*x)(5)
25

# 람다함수를 사용해 함수 정의
>>> f = lambda x : x*x
>>> f(5)
25
```

#### 람다함수의 사용

```python
import string
>>> for char in string.ascii_lowercase:
...   if char > 'i':
...     print(char.upper())
...   else:
...     print(char)
```

```
>>> for char in string.ascii_lowercase:
...   print((lambda x : x.upper() if x > 'i' else x)(char))
```

#### 클로져 (Closure)

함수가 정의된 환경을 말하며, 파이썬 파일이 여러개일 경우 각 파일은 하나의 `모듈`역할을 하고, 각 `모듈`은 독립적인 환경을 가진다.  
독립된 환경은 각자의 영역을 전역 영역으로 사용한다.

**closure/module_a.py**

```python
level = 100
def print_level():
    print(level)
```

**closure/module_b.py**

```python
import module_a
level = 50
def print_level():
    print(level)
    
module_a.print_level()
print_level()
```

`python module_b.py`로 `module_b`를 실행한다.

함수의 전역 영역은 해당 함수가 정의된 모듈의 전역 영역으로, 전역변수는 모듈의 영역에 영향을 받는다.

#### 내부함수의 클로져

```python
>>> level = 0
>>> def outter():
...   level = 50
...   def inner():
...     nonlocal level
...     level += 3
...     print(level)
...   return inner
...
>>> func = outter()
```

위의 경우, `outter`함수는 `inner`함수를 반환하여 결과를 `func`전역변수에 할당한다.  
`inner`함수의 호출 결과가 아닌 함수 자체를 반환하기 때문에, `func`변수는 실행할 수 있는 함수객체이다.  
이 때 `inner`함수가 사용하는 `level`변수는 `nonlocal`키워드를 사용했기 때문에 `outter`에 새로 정의된 지역변수 `level`을 사용한다.  
반복적으로 `func`함수를 실행하면 `inner`의 외부(`outter`)에 존재하는 `level`변수의 값을 증가시키고 `print`시키기 때문에, 값은 계속해서 증가한다.

func2를 만든다면?


```
level=0
def outer():
    level = 50
    
    def inner():
        nonlocal level
        level += 3
        print(level)
    return inner

f = outer()
f()
f()
f()

f2 = outer()
f2()
f2()
f2()

f3 = outer()
f3()
f3()

-------------------------------------------
53
56
59
53
56
59
53
56


```

#### 데코레이터 (decorator)

함수를 받아 다른 함수를 반환하는 함수. 예를 들면, 기존에 존재하던 함수를 바꾸지 않고 전달된 인자를 보기위한 디버깅 `print`함수를 추가한다던가 하는 기능을 할 수 있다.

1. 기능을 추가할 함수를 인자로 받음
2. 데코레이터 자체에 추가할 기능을 함수로 정의
3. 인자로 받은 함수를 데코레이터 내부에서 적절히 호출
4. 위 2가지를 행하는 내부 함수를 반환

아래와 같이 함수 2개를 만들고, 새 구문을 추가해본다.

- 인자로 문자열 변수를 받아 출력해주는 함수 `print_string`구현
- 인자로 정수형 변수를 받아 출력해주는 함수 `print_int`구현
- 각 함수에 대해 자신이 전달받은 인자에 대한 `type`을 출력하는 구문을 추가

여러 함수에 대해 같은 기능을 추가할 경우, 데코레이터를 사용한다.

```python
def print_debug(func):
    def inner_func(*args, **kwargs):
        print('args :', args)
        print('kwargs :', kwargs)
        result = func(*args, **kwargs)
        return result
    return inner_func
```

데코레이터함수(인자로 전달할 함수) 형태로도 사용이 가능하지만, 데코레이터를 사용할 경우에는 함수 위에 데코레이터를 추가해서 사용가능하다.

```python
@print_debug
def any_func():
    pass
```

또한 데코레이터는 여러개를 가질 수 있으며, 함수에서 가장 가까운 것 부터 실행한다.

- print_debug이후 결과를 제곱하고 print해주는 데코레이터를 실행, 반대로 실행


```

```




#### 제네레이터 (generator)

제네레이터는 함수는 파이썬의 시퀀스 데이터를 생성하는데 사용된다. 실제 시퀀스 데이터와 다른 점은, 시퀀스 전체를 가지고 있는 것이 아니라 시퀀스 데이터를 생성하기 위한 어떠한 루틴만을 가지고 있는 것이다.  
이 방식을 택했을 때의 장점은, 전체 크기만큼의 메모리를 가지고 있는 시퀀스 데이터와는 달리 메모리를 적게 사용할 수 있다.

제네레이터는 마지막으로 호출한 위치(항목)에 을 기억하고 있으며, 한 번 순회할 때 마다 그 다음 값을 반환한다.

제네레이터는 함수를 통해서 만들어지며, 함수 내부의 반복문에서 `yield`키워드를 사용하면 제네레이터가 된다.

```python
>>> def range_gen(num):
...   i = 0
...   while i < num:
...     yield i
...     i += 1
...
>>> gen = range_gen(10)
>>> gen
<generator object range_gen at 0x10b682168>
>>> type(gen)
<class 'generator'>
>>> gen.__next__()
0
>>> gen.__next__()
1
>>> gen.__next__()
2
>>> gen.__next__()
3
>>> gen.__next__()
4
>>> gen.__next__()
5
>>> gen.__next__()
6
>>> gen.__next__()
7
>>> gen.__next__()
8
>>> gen.__next__()
9
>>> gen.__next__()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

함수 내부에 `yield`키워드가 사용되어 제네레이터 함수가 되었으며, 함수를 실행하면 제네레이터 객체를 반환한다.  
`yield`부분에서 멈춘 제네레이터 객체를 순회하기 위해서는 `__next__()` 함수를 실행해준다.


```

In[]:

def range_gen(num):
    i = 0
    while i < num:
        yield i
        i += 1
        
gen = range_gen(10)
print(gen)
print(type(gen))

# gen.__next__()
# gen.__next__()
# gen.__next__()
# gen.__next__()
# gen.__next__()
# gen.__next__()
# gen.__next__()
# gen.__next__()
# gen.__next__()
# gen.__next__()

# for item in gen:
#     print(item)
    
# while pen:

i = 0
while i < 8:
    print(gen.__next__())
    i += 1
    
    ---------------------
<generator object range_gen at 0x10a242c50>
<class 'generator'>
0
1
2
3
4
5
6
7
```



## 실습

1. 매개변수로 문자열을 받고, 해당 문자열이 `red`면 `apple`을, `yellow`면 `banana`를, `green`이면 `melon`을, 어떤 경우도 아닐 경우 `I don't know`를 리턴하는 함수를 정의하고, 사용하여 `result`변수에 결과를 할당하고 `print`해본다.

```

```


2. 1번에서 작성한 함수에 `docstring`을 작성하여 함수에 대한 설명을 달아보고, `help(함수명)`으로 해당 설명을 출력해본다.

```
fruit_color_dict = {
    'red':'apple',
    'yello':'banana',
    'green':'melon'
}

def what_fruit_by_dict(color, dict_):
#     if color in dict_:
#         return dict_[color]
#     else:
#         return 'I dont\'t know'

    '과일을 찾을 color와 검색할 dict를 color, dict_로 입력받아 결과 문자열을 리턴'

    return dict_.get(color, 'I don\'t know')

result = what_fruit_by_dict('red', fruit_color_dict)
result2 = what_fruit_by_dict('purple', fruit_color_dict)

print(result)
print(result2)
print(help(what_fruit_by_dict))

# def what_fruit(color):
#     if color == 'red':
#         return 'apple'
#     elif color == 'yello':
#         return 'banana'
#     elif color == 'green':
#         return'melon'
#     else:
#         return 'I don\'t know'

# result = what_fruit('red')
# print(result)

---------------------------------

apple
I don't know
Help on function what_fruit_by_dict in module __main__:

what_fruit_by_dict(color, dict_)
    과일을 찾을 color와 검색할 dict를 color, dict_로 입력받아 결과 문자열을 리턴

None
```

3. 한 개 또는 두 개의 숫자 인자를 전달받아, 하나가 오면 제곱, 두개를 받으면 두 수의 곱을 반환해주는 함수를 정의하고 사용해본다.

```
def multi1(arg1, arg2 = None):
    if arg2:
        return arg1 * arg2
    return arg1 * arg1

def multi2(*args):
    if len(args) > 1:
        return args[0] * args [1]
    elif len(args) == 1:
        return args[0] * args [0]
    else:
        raise Exception('require arguments')
        
result1 = multi1(3)
result2 = multi1(3, 5)
# result2_2 = multi1(3, 5, 5)
result3 = multi2(3)
result4 = multi2(3, 5)
---------------------------------

```

4. 두 개의 숫자를 인자로 받아 합과 차를 튜플을 이용해 동시에 반환하는 함수를 정의하고 사용해본다.

```
def sum_sub (num1, num2):
    return(num1 + num2, num1 - num2)

result = sum_sub(3, 5)
print(result)

---------------------------------
(8, -2)

```

5. 위치인자 묶음을 매개변수로 가지며, 위치인자가 몇 개 전달되었는지를 print하고 개수를 리턴해주는 함수를 정의하고 사용해본다.

```
def args_count(*args):
    count = len(args)
    print(count)
    return count

args_count(3,5,2,6,7,3)


----------------------

6
Out[71]:
6
```

6. 람다함수와 리스트 컴프리헨션을 사용해 한 줄로 구구단의 결과를 갖는 리스트를 생성해본다.

```
l = ['{} x {}= {}'.format(x,y,x*y) for x in range(2,10) for y in range (1,10)]
l2 = [(lambda x,y : '{}x {} = {}'.format(x,y, x*y))(x,y) for x in range (2,10) for y in range(1,10)] 


    
l3 =[]
for x in range(2,10):
    for y in range(1,10):
        l3.append((lambda x, y : '{}x{}={}'.format(x,y,x*y))(x,y))
        l3.append('{}x{}={}'.format(x,y,x*y))
        
for item in l2:
    print(item)
-------------------------------------


```


