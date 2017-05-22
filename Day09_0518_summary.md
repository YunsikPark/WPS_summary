#Day9 - Summary (Python)
> 2017.05.18 THU
> **박윤식**
 
-
## while문 (Python)
for문과 유사하나, while뒤의 조건이 참일 경우에 계속해서 반복한다.

```
while 조건:
  조건이 참일경우 실행
  조건이 거짓이 될 경우까지 계속해서 반복
```

```
>>> count = 0
>>> while count < 10:
...   print(count)
...   count += 1
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

## 컴프리헨션 (Comprehension)

> 함축 또는 내포

iterable한 객체로부터 파이썬의 자료구조를 만드는 방법. 가독성과 사용성에서 이득을 얻을 수 있을 경우 항상 사용해준다.

#### 리스트 컴프리헨션

```
[표현식 for 항목 in iterable객체]
```

[1,2,3,4,5]를 만드는 방법

##### range와 for문을 사용할 경우

```
>>> numbers = []
>>> for item in range(1, 6):
...   numbers.append(item)
... 
>>> numbers
[1, 2, 3, 4, 5]
```

##### 리스트 컴프리헨션을 사용할 경우

```
>>> [item for item in range(1, 6)]
[1, 2, 3, 4, 5]
```

만약 각 item에 2배의 값을 할당하고 싶다면?

```
 [item*2 for item in range(1,6)]
```

만약 1~5중 짝수만 해당하는 리스트를 만들고 싶다면?

```
[item for item in range(1,6) if item % 2 ==0]
```

##### 리스트 컴프리헨션의 중첩

```
for color in colors:
  for fruit in fruits:
```

```
[(color, fruit) for color in colors for fruit in fruits]
```

#### 셋 컴프리헨션

```
{표현식 for 표현식 in iterable객체}
```

#### 제네레이터 컴프리헨션

```
(표현식 for 표현식 in interable객체)
```
괄호로 되어있지만 튜플을 생성하지 않는다. (튜플은 컴프리헨션이 없다)

제너레이터 객체는 순회 가능하며, 리스트 형태로 만들 수 있다.


## 실습

1. for문을 2개 중첩하여 (0,0), (0,1), (0,2), (0,3), (1,0), (1,1)..... (6,3)까지 출력되는 반복문을 구현한다.

```
In [30]: for a in range(7):
    ...:     for b in range(4):
    ...:         print ((a,b))
    ...:         
    ...:        
```

2. 리스트 컴프리헨션을 중첩하여 위 결과를 똑같이 출력한다.

```
[(a,b) for a in range(7) for b in range(4)]
```

3. 1, 2번의 반복문에서 튜플의 첫 번째 항목이 짝수일때만 출력하도록 조건을 변경한다.

```
[(a,b) for a in range(7) for b in range(4) if a % 2 == 0]
```

4. 1000에서 2000까지의 숫자 중, 홀수의 합을 구해본다.

```


In [67]: sum([x for x in range ( 1000,2001 ) if x % 2 == 1])
Out[67]: 750000
```

5. 리스트 컴프리헨션을 사용하여 구구단 결과를 갖는 리스트를 만들고, 해당 리스트를 for문을 사용해 구구단 형태로 나오도록 출력해본다.  
  각 단마다 한 번 더 줄바꿈을 넣어준다.
 
```
In [74]: l = ['{} x {} = {}'.format(x,y,x*y if y !=9 else '{}\n'.format(x*y)) for x in range(2,10)for y in range (2,10)]


In [74]: l = ['{} x {} = {}'.format(x,y,x*y if y !=9 else str(x*y)+'\n') for x in range(2,10)for y in range (2,10)]   


for item in l:
    ...:     print(item)

```

6. 1에서 99까지의 정수 중, 7의 배수이거나 9의 배수인 정수인 리스트를 생성한다. 단, 7의 배수이며 9의 배수인 수는 한 번만 추가되어야 한다. 

```
l2 = [x for x in range(100) if not x % 7 or not x % 9]
```


# 함수

반복적인 작업을 하는 코드를 재사용이 가능하게 정의해 놓은 것.

```python
def 함수명(매개변수[parameters]):
	동작
```

#### 함수의 정의, 실행

```python
# 실행 시 'call func'를 print하는 함수 정의
>>> def func():
...   print('call func')
... 

# 함수 자체는 function객체를 참조하는 변수
>>> func
<function func at 0x10dabf378>

# 함수를 실행시키기 위해 () 사용
>>> func()
call func
```


#### 리턴값이 있는 함수 정의

```python
>>> def return_true():
...   return True
... 
>>> return_true()
True
```

함수의 결과로 Bool값을 갖는 데이터를 리턴하여 if문이나 while문의 조건으로 사용 가능하다.



#### 매개변수를 사용하는 함수 정의

```python
>>> def print_arguments(something):
...   print(something)
... 
>>> print_arguments('ABC')
ABC
```

#### 매개변수(parameter)와 인자(argument)의 차이

함수 내부에서 함수에게 전달되어 온 변수는 매개변수라 부르며, 함수를 호출할 때 전달하는 변수는 인자로 부른다.

```python
# 함수 정의때는 매개변수
def func(매개변수1, 매개변수2):
  ...
  
# 함수 호출시에는 인자
>>> func(인자1, 인자2)
```



#### 리턴값이 없을 경우

함수에서 리턴해 주는 값이 없을 경우, 아무것도 없다는 뜻을 가진 `None`객체를 얻는다.

#### 위치 인자(Positional arguments)

매개변수의 순서대로 인자를 전달하여 사용하는 경우

*순서를 지켜야한다*

```python
>>> def student(name, age, gender):
...   return {'name': name, 'age': age, 'gender': gender}
... 
>>> student('hanyeong.lee', 30, 'male')
{'name': 'hanyeong.lee', 'age': 30, 'gender': 'male'}
```

```
def make_student(name, age, gender):
        return{
                'name':name,
                'age':age,
                'gender':gender,
        }

s1 = make_student('hanyeong.lee',30,'male')

for key, value in s1.items():
        print('{:7}: {}'.format(key,value))
        
        
        
        
        
     or   



def make_student(name, age, gender):
        return{
                'name':name,
                'age':age,
                'gender':gender,
        }

def print_student(student):
        for key, value in s1.items():
                print('{:7}: {}'.format(key,value))

s1 = make_student('hanyeong.lee',30,'male')
print_student(s1)


```


#### 키워드 인자(Keyword arguments)

매개변수의 이름을 지정하여 인자로 전달하여 사용하는 경우

```python
>>> student(age=30, name='hanyeong.lee', gender='male')
{'name': 'hanyeong.lee', 'age': 30, 'gender': 'male'}
```

**위치인자와 키워드인자를 동시에 쓴다면, 위치인자가 먼저 와야 한다**


#### 기본 매개변수값 지정

인자가 제공되지 않을 경우, 기본 매개변수로 사용할 값을 지정할 수 있다.

```python
>>> def student(name, age, gender, cls='WPS'):
...   return {'name': name, 'age': age, 'gender': gender, 'class': cls}
... 
>>> student('hanyeong.lee', 30, 'male')
{'name': 'hanyeong.lee', 'age': 30, 'gender': 'male', 'class': 'WPS'}
```

#### 기본 매개변수값의 정의 시점

> 기본 매개변수값은 함수가 실행될 때 마다 계산되지 않고, 함수가 정의되는 시점에 계산되어 계속해서 사용된다.

```python
>>> def return_list(value, result=[]):
...   result.append(value)
...   return result
... 
>>> return_list('apple')
['apple']
>>> return_list('banana')
['apple', 'banana']
```

함수가 실행되는 시점에 기본 매개변수값을 계산하기 위해, 아래와 같이 바꿔준다.

```python
>>> def return_list(value, result=None):
...   if result is None:
...     result = []
...   result.append(value)
...   return result
... 
>>> return_list('apple')
['apple']
>>> return_list('banana')
['banana']
```

#### 위치인자 묶음

함수에 위치인자로 주어진 변수들의 묶음은 `*매개변수명`으로 사용할 수 있다.  
관용적으로 `*args`를 사용한다.

```python
def print_args(*args):
  print(args)
```

#### 키워드인자 묶음

함수에 키워드인자로 주어진 변수들의 묶음은 `**매개변수명`으로 사용할 수 있다.
관용적으로 `**kwargs`를 사용한다.

```python
def print_kwargs(**kwargs):
  print(kwargs)
```


```


  1 def print_args(*args):
  2     print(args)
  3   
  4     
  5 
  6 def print_kwargs(**kwargs):
  7     print(kwargs)
  8 
  9 
 10 print_args('python','ruby','java', 
 #print_args(language = 'python', ide='pycharm')
 11 
 12 print_kwags(language = 'python', ide='pycharm')
 13 #print_kwags('python','ruby','java')
 14 



  1 def print_args(*args, **kwargs):
  2     #'입력받은 positional arguments를 출력해줍니다'
  3     print(args)
  4     print(kwargs)
  5 
  6 
  7 def print_kwargs(**kwargs):
  8     print(kwargs)
  9 
 10 
 11 print_args('python','ruby','java', language = 'python', ide='pycharm')
 12 
 13 print('')
 14 
 15 print_args(language = 'python', ide='pycharm')
 16 
 17 print('')
~                          

```





#### docstring

함수를 정의한 문서 역할을 한다.  
함수 정의 후, 몸체의 시작부분에 문자열로 작성하며, 여러줄로도 작성 가능하다.

```python
>>> def print_args(*args):
...   'Print positional arguments'
...   print(args)
... 
>>> help(print_args)
```



#### 함수를 인자로 전달

파이썬에서는 함수 역시 다른 객체와 동등하게 취급되므로, 함수에서 인자로 함수를 전달, 실행, 리턴하는 형태로 프로그래밍이 가능하다.

- 'call func'를 출력하는 함수를 정의하고, 함수를 인자로 받아 실행하는 함수를 정의하여 첫 번째에 정의한 함수를 인자로 전달해 실행해보자.


```
(fc-python) ------------------------------------------------------------
~/projects/python/09.function »                               willbook@Yunsikui-MacBook-Pro
(fc-python) ------------------------------------------------------------
~/projects/python/09.function » vi function_arguments.py      willbook@Yunsikui-MacBook-Pro

  1 def print_call_func():
  2     #'단순히 "call_func"라는 문자열을 출력해준다.
  3     print('call_func')
  4 
  5 def execute_another_function(another_function):
  6     #'매개변수로 주어진 함수를 실행한다.
  7     another_function()
  8 
  9 # execute_another_function 함수에 print_call_func 함수를 인자로 전달하여 실행해본다.
 10 
 11 f1 = print_call_func
 12 #print(id(f1))
 13 #print(id(print_call_func))
 14 execute_another_function(f1)
 15 
 16 
 17 
 18 
 19 #msg라는 매개변수를 갖는 함수를 정의, 해당 함수는 print(msg)를 실행하는 또 다른 함수를 >    생성해서 리턴해준다.
 20 #execute_another_function에서 위의 함수를 이용해 만든 함수를 인자로 전달하여 실행
 21 
 22 def return_print_function(msg):
 23     # 이 내부에서 새로운 함수를 생성(def어떤함수)하고
 24     # 아래에서 리턴해줘야 한다.
 25     def return_function():
 26         print(msg)
 27 
 28     return return_function
 29 
 30 
 31 f1 = return_print_function('이걸 출력해주세요')
 32 execute_another_function(f1)
 33 
 34 
 35 def return_print_function(msg):
 36     # 이 내부에서 새로운 함수를 생성(def어떤함수)하고
 37     # 아래에서 리턴해줘야 한다
 38     def return_function(msg, msg2):
 39          print(msg, msg2)
 40 
 41     return return_function
 42 
 43 f1 = return_print_function('이걸출력해주세요')
 44 f1 = ('첫번째 문자열',' 두번째문자열')
 45 
 46 
 47 

```

#### 내부 함수

함수 안에서 또 다른 함수를 정의해 사용할 수 있다.

- 문자열 인자를 하나 전달받는 함수를 만들고, 해당 함수 내부에 전달받은 문자열을 대문자화해서 리턴해주는 내부 함수를 구현한다.  
문자열을 전달받는 함수는 내부함수를 실행한 결과를 리턴하도록 한다.


####function\_arguments\_sample.py
1. 숫자를 입력받아 해당하는 숫자 단수의 (x, y, z)형 튜플의 리스트로 곱할 수 1,2 와 결과를 저장하는 함수 make\_gugu(num) 작성

	ex) make\_gugu(3) -> return [(3,1,3),(3,2,6), ...(3,9,27)]


2. 매개변수 print_type과 gugu\_list를 가지며, print\_type에 따라 gugu\_list를 단순출력 또는 '{} x {} = {}'형으로 출력해주는 함수 print\_gugu(print\_type, gugu\_list)작성
	
	ex)print\_gugu('simple',<어떤리스트>) -> print((3,1,3),(3,2,6)...)
	print\_type은 'simple'과 'normal'로 나눠지며, simple은 튜플을 그냥 출력 normal은 위의 format string 형태로 출력
	
3. 매개변수 range, print\_type, make\_gugu\_function, print\_gugu\_function을 가지고 range에 해당하는 범위의 구구단을 생성하고 출력하는 함수 gugu 작성
 
 gugu함수에서는 매 단마다 줄바꿈 및 이번이 몇 단인지를 알려주는 문자열을 출력
 
 \_function으로 끝나는 매개변수는 함수 자체를 전달
 ex)gugu(range(3,7), 'normal', make\_gugu, print\_gugu)
 
 =3단=
 
 3x1=3
 ...
 
 =6단=
 
 6x1=6
 ...
 
 6x9=54
 
 
 
```
# 다음을 채워라.


  1 def make_gugu(num):
  2	    pass     
  3         
  4 
  5     return return_gugu
  6 
  7 def print_gugu(print_type, gugu_list):
  8     pass
  9 
 10 def gugu(range_, print_type, make_gugu_function, print_gugu_function):
 11     pass
 12 

```

```
~/projects/python/09.function » vi function_arguments_sample.py

  1 def make_gugu(num):
  2     return[(num, y, num*y) for y in range(1,10)]
  3 
  4 #result = make_gugu(3)
  5 #print(result)
  6 
  7 
  8 
  9 def print_gugu(print_type, gugu_list):
 10     if print_type == 'simple':
 11         for item in gugu_list:
 12             print(item)
 13 
 14     elif print_type == 'normal':
 15         for x, y, z in gugu_list:
 16             print('{} x {} = {}'.format(x, y, z))
 17 
 18 g_list = make_gugu(3)
 19 print_gugu('normal', g_list)
 20 
 21 
 22 
 23 def gugu(range_, print_type, make_gugu_function, print_gugu_function):
 24     #range_변수에는 iterable한 range형 객체가 주어졌다고 가정
 25     for num in range_:
 26         print('{val:=^10s}'.format(val=' ' + str(num)+ '단'))
 27 
 28         #make_gugu_function을 이용해 (x,y,x*y)형태의 원소들을 갖는 리스트를 생성
 29         cur_gugu_list = make_gugu_function(num)
 30         #생성한 리스트를 인자로 전달해 출력
 31         print_gugu_function(print_type, cur_gugu_list)
 32 
 33         print('')
 34 
 35 gugu(range(2, 4), 'normal', make_gugu, print_gugu)
 36 
 37 
 38 

```

또는


```
  1 def make_gugu(num):
  2     return[(num, y, num*y) for y in range(1,10)]
  3 
  4 
  5 
  6 
  7 def print_gugu(print_type, gugu_list):
  8     def print_gugu_simple():
  9         for item in gugu_list:
 10             print(item)
 11     def print_gugu_normal():
 12         for x,y,z in gugu_list:
 13             print('{} x {} = {}'.format(x, y, z))
 14             
 15     if print_type == 'simple':
 16         print_gugu_simple()
 17     elif print_type == 'normal':
 18         print_gugu_normal()
 19         
 20         
 21          
 22 
 23 def gugu(range_, print_type, make_gugu_function, print_gugu_function):
 24     #range_변수에는 iterable한 range형 객체가 주어졌다고 가정
 25     for num in range_:
 26         print('{val:=^10s}'.format(val=' ' + str(num)+ '단'))
 27         
 28         #make_gugu_function을 이용해 (x,y,x*y)형태의 원소들을 갖는 리스트를 생성
 29         cur_gugu_list = make_gugu_function(num)
 30         #생성한 리스트를 인자로 전달해 출력
 31         print_gugu_function(print_type, cur_gugu_list)
 32         
 33         print('')
 34         
 35 gugu(range(2, 4), 'normal', make_gugu, print_gugu)
 36 

```




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

```
  1 champion = 'Lux'
  2 
  3 def show_global_champion():
  4     print('show_global_champion:{}'.format(champion))
  5     print('show_global_champion id : {}'.format(id(champion)))
  6 
  7 def change_global_champion():
  8     #print('before_change_global_champion : {}'.format(champion))
  9     
 10     champion = 'Ahri'
 11     print('local scope champion id: {}'.format(id(champion)))
 12     print('after_change_global_champion : {}'.format(champion))
 13     print('change_global_champion locals(): {}'.format(locals()))
 14     print('change_global_champion globals(): {}'.format(globals()))
 15 
 16 
 17 
 18 show_global_champion()
 19 change_global_champion()
 20 print('print_champion :{}'.format(champion))
 21 print('print_champion id: {}'.format(id(champion)))
 22 print('print_locals(): {}'.format(locals()))
~

```