## 선택 정렬
>[wiki](https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC)

### 외부 및 내부 Loop까지
전체리스트의 길이가 n개 라고 가정했을 때,
n-1번의 loop를 돌며

각 loop내부에서는 n - loop 횟수변의 비교를 함 **<- 중요**
(아래 예제는 편의를 위해 0번째 대신 1번째부터 시작합니다)

#####출력예시
```
sample_list = [5, 1, 3, 7, 2, 9]
def selection_sort(ori_list):
    ori_len = len(ori_list)
    for i in range(ori_len -1):
        print('{}번째 loop입니다'.format(i + 1))
        
selection_sort(sample_list)
```
>1번째 loop입니다  
>2번째 loop입니다  
>3번째 loop입니다   
>4번째 loop입니다  
>5번째 loop입니다



```
sample_list = [5, 1, 3, 7, 2, 9]
def selection_sort(ori_list):
    # 주어진 리스트의 길이
    ori_len = len(ori_list)
    
    #리스트길이 -1번만큼 순회, 각 인덱스는 i에 지정
    for i in range(ori_len -1):
        print('{}번째 loop입니다'.format(i + 1))
        
        #loop 내부에서 매 loop마다 리스트 길이 -i(상위 인덱스)만큼 순회
        for j in range(i+1, ori_len):
            print('{}번째 loop내부의 {}번째 loop'.format(i+1, j+1))
        
selection_sort(sample_list)        
```
>1번째 loop입니다   
1번째 loop내부의 2번째 loop   
1번째 loop내부의 3번째 loop   
1번째 loop내부의 4번째 loop      
1번째 loop내부의 5번째 loop  
1번째 loop내부의 6번째 loop  
2번째 loop입니다  
2번째 loop내부의 3번째 loop  
2번째 loop내부의 4번째 loop  
2번째 loop내부의 5번째 loop   
2번째 loop내부의 6번째 loop  
3번째 loop입니다   
3번째 loop내부의 4번째 loop  
3번째 loop내부의 5번째 loop   
3번째 loop내부의 6번째 loop  
4번째 loop입니다  
4번째 loop내부의 5번째 loop   
4번째 loop내부의 6번째 loop   
5번째 loop입니다	  
5번째 loop내부의 6번째 loop	   	

```
sample_list = [5, 1, 3, 7, 2, 9]
def selection_sort(ori_list):
    # 주어진 리스트의 길이
    ori_len = len(ori_list)
    
    #리스트길이 -1번만큼 순회, 각 인덱스는 i에 지정
    for i in range(ori_len -1):
        print('{}번째 loop입니다'.format(i + 1))
        
        #loop 내부에서 매 loop마다 리스트 길이 -i(상위 인덱스)만큼 순회
        for j in range(i+1, ori_len):
            #loop마다 자신의 값을 출력
            print('{}번째 요소의 값은 {}'.format(i+1, ori_list[j]))
        
selection_sort(sample_list)
```


>1번째 loop입니다  
1번째 요소의 값은 1  
1번째 요소의 값은 3  
1번째 요소의 값은 7  
1번째 요소의 값은 2  
1번째 요소의 값은 9  
2번째 loop입니다  
2번째 요소의 값은 3  
2번째 요소의 값은 7  
2번째 요소의 값은 2  
2번째 요소의 값은 9  
3번째 loop입니다  
3번째 요소의 값은 7  
3번째 요소의 값은 2  
3번째 요소의 값은 9  
4번째 loop입니다  
4번째 요소의 값은 2  
4번째 요소의 값은 9  
5번째 loop입니다  
5번째 요소의 값은 9  




```
sample_list = [5, 1, 3, 7, 2, 9]
def selection_sort(ori_list):
    # 주어진 리스트의 길이
    ori_len = len(ori_list)
    
    #리스트길이 -1번만큼 순회, 각 인덱스는 i에 지정
    for i in range(ori_len -1):
        print('{}번째 loop입니다'.format(i + 1))
        
        cur_min_index = i
        print('현재 최소 값은{}, 인덱스는{} 입니다.'.format(
            ori_list[cur_min_index],
            cur_min_index +1
        ))
        

selection_sort(sample_list)    
```

>1번째 loop입니다.  
현재 최소 값은5, 인덱스는1 입니다.   
2번째 loop입니다.  
현재 최소 값은1, 인덱스는2 입니다.   
3번째 loop입니다.  
현재 최소 값은3, 인덱스는3 입니다.   
4번째 loop입니다.  
현재 최소 값은7, 인덱스는4 입니다.   
5번째 loop입니다.  
현재 최소 값은2, 인덱스는5 입니다.   

```
sample_list = [5, 1, 3, 7, 2, 9]
def selection_sort(ori_list):
    # 주어진 리스트의 길이
    ori_len = len(ori_list)
    
    #리스트길이 -1번만큼 순회, 각 인덱스는 i에 지정
    for i in range(ori_len -1):
        print('{}번째 loop입니다'.format(i + 1))
        
        cur_min_index = i
        print('현재 최소 값은{}, 인덱스는{} 입니다.'.format(
            ori_list[cur_min_index],
            cur_min_index +1
        ))
        
        #loop 내부에서 매 loop마다 리스트 길이 -i(상위 인덱스)만큼 순회
        for j in range(i+1, ori_len):
                #cur_min_index가 가지는 값과 j인덱스가 가지는 갑슬 비교
                if ori_list[cur_min_index] > ori_list[j]:
                    print('{}번째 index의 {}값이 기존값보다 작음'.format(
                    j +1,
                    ori_list[j]
                    ))

selection_sort(sample_list)    
```

>1번째 loop입니다.  
현재 최소 값은5, 인덱스는1 입니다.   
2번째 index의 1값이 기존값보다 작음.  
3번째 index의 3값이 기존값보다 작음.  
5번째 index의 2값이 기존값보다 작음.  
2번째 loop입니다.  
현재 최소 값은1, 인덱스는2 입니다.   
3번째 loop입니다.  
현재 최소 값은3, 인덱스는3 입니다.   
5번째 index의 2값이 기존값보다 작음.  
4번째 loop입니다.  
현재 최소 값은7, 인덱스는4 입니다.   
5번째 index의 2값이 기존값보다 작음.  
5번째 loop입니다.  
현재 최소 값은2, 인덱스는5 입니다.   


```
import random

sample_list = [5, 1, 3, 7, 2, 9]
sample_list = [x for x in range(10)]
random.shuffle(sample_list)

def selection_sort(ori_list):
    # 주어진 리스트의 길이
    ori_len = len(ori_list)
    
    #리스트길이 -1번만큼 순회, 각 인덱스는 i에 지정
    for i in range(ori_len -1):
        print('{}번째 loop입니다'.format(i + 1))
        
        cur_min_index = i
        print('현재 최소 값은{}, 인덱스는{} 입니다.'.format(
            ori_list[cur_min_index],
            cur_min_index +1
        ))
        
        #loop 내부에서 매 loop마다 리스트 길이 -i(상위 인덱스)만큼 순회
        #순회 시, i+1 부터 리스트 전체 길이까지 수회하여 비교하려는 첫번째 인덱스 이후부터 끝까지 순회
        
        for j in range(i+1, ori_len):
                #cur_min_index가 가지는 값과 j인덱스가 가지는 갑슬 비교
                if ori_list[cur_min_index] > ori_list[j]:
                    cur_min_index = j
                    print('{}번째 index의 {}값이 기존값보다 작음'.format(
                    cur_min_index +1,
                    ori_list[cur_min_index]
                    ))
                    
        #내부 loop가 끝난 후, cur_min_index의 값과 i인덱스의 값을 서로 바꿔준다.
        temp = ori_list[i], ori_list[cur_min_index]= ori_list[cur_min_index], ori_list[i]

        print('{}번째 loop 결과: {}'.format(i +1, ori_list))

selection_sort(sample_list)    
```
>1번째 loop입니다.  
현재 최소 값은1, 인덱스는1 입니다.   
4번째 index의 0값이 기존값보다 작음.  
1번째 loop 결과: [0, 4, 9, 1, 7, 5, 2, 3, 6, 8].   
2번째 loop입니다.  
현재 최소 값은4, 인덱스는2 입니다.   
4번째 index의 1값이 기존값보다 작음.  
2번째 loop 결과: [0, 1, 9, 4, 7, 5, 2, 3, 6, 8].  
3번째 loop입니다.  
현재 최소 값은9, 인덱스는3 입니다.   
4번째 index의 4값이 기존값보다 작음.  
7번째 index의 2값이 기존값보다 작음.  
3번째 loop 결과: [0, 1, 2, 4, 7, 5, 9, 3, 6, 8].  
4번째 loop입니다.  
현재 최소 값은4, 인덱스는4 입니다.   
8번째 index의 3값이 기존값보다 작음.  
4번째 loop 결과: [0, 1, 2, 3, 7, 5, 9, 4, 6, 8].  
5번째 loop입니다.  
현재 최소 값은7, 인덱스는5 입니다.   
6번째 index의 5값이 기존값보다 작음.  
8번째 index의 4값이 기존값보다 작음.  
5번째 loop 결과: [0, 1, 2, 3, 4, 5, 9, 7, 6, 8].  
6번째 loop입니다.  
현재 최소 값은5, 인덱스는6 입니다.   
6번째 loop 결과: [0, 1, 2, 3, 4, 5, 9, 7, 6, 8].  
7번째 loop입니다.  
현재 최소 값은9, 인덱스는7 입니다.   
8번째 index의 7값이 기존값보다 작음.  
9번째 index의 6값이 기존값보다 작음.  
7번째 loop 결과: [0, 1, 2, 3, 4, 5, 6, 7, 9, 8].  
8번째 loop입니다.  
현재 최소 값은7, 인덱스는8 입니다.   
8번째 loop 결과: [0, 1, 2, 3, 4, 5, 6, 7, 9, 8].  
9번째 loop입니다.  
현재 최소 값은9, 인덱스는9 입니다.   
10번째 index의 8값이 기존값보다 작음.  
9번째 loop 결과: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9].  
 

## [빅오 표기법](https://namu.wiki/w/%EC%A0%90%EA%B7%BC%20%ED%91%9C%EA%B8%B0%EB%B2%95)

1번째 -> N -1
2번째 -> N -2
...


---

# 모듈과 패키지

## 모듈
 
지금까지 셸에서 진행한 실습의 경우, 하나의 모듈 내부에서 작업한 것으로 취급된다.

파이썬 파일은 각각 하나의 모듈로 취급되며, 실행이나 함수의 정의, 단순 변수의 모음 등등 여러 역할을 한다.

#### 모듈 불러오기 (import)

기본 게임모듈에서, 부가적인 기능들을 불러와서 사용하는 형태로 코드를 작성해본다.

**module/shop.py**

```python
def buy_item():
    print('Buy item!')

buy_item()
```

**module/game.py**

```python
def play_game():
    print('Play game!')

play_game()
```

**module/lol.py**

```python
import game
import shop

print('= Turn on game =')
game.play_game()
shop.buy_item()
```

#### \_\_name\_\_변수 

`lol.py`가 실행될 때, `game`과 `shop`가 import되는 순간 해당 코드가 실행되어 버리는 문제가 있다.

이 때, 파이썬 인터프리터를 이용해 실행한 코드인지를 확인하여 단순히 `import`한 모듈의 경우 실행을 막는 방식을 사용할 수 있다.

각 모듈은 자신의 이름을 가지며, 모듈 이름은 모듈의 전역변수 `__name__`에서 확인 할 수 있다.

```
print(__name__)
```

파이썬 인터프리터가 실행한 모듈의 경우, `__main__`이라는 이름을 가진다. 따라서 `python <파일명>`으로 실행한 경우에만 동작할 부분은 if문으로 감싸준다.

**module/shop.py**

```python
def buy_item():
    print('Buy item!')

if __name__ == '__main__':
    buy_item()
```

**module/game.py**

```python
def play_game():
    print('Play game!')

if __name__ == '__main__':
    play_game()
```

다시 `lol.py`를 실행해본다.




#### lol.py 리펙토링

```python
import game
import shop

def turn_on():
    print('= Turn on game =')

    while True:
        choice = input('What would you like to do?\n  1: Go to Shop, 2: Play Game, 0: Exit\n    Input : ')
        if choice == '0':
            break
        elif choice == '1':
            shop.buy_item()
        elif choice == '2':
            game.play_game()
        else:
            print('Choice not exist')
        print('-----------------------')

    print('= Turn off game =')

if __name__ == '__main__':
    turn_on()
```



#### from을 사용해 import

```
  1 from functions  import game
  2 from functions import shop
  3
  4 def turn_on():
  5     print(' = Turn on game = ')
  6
  7     while True:
  8         choice = input('What would you like to do? \n 1: Go to Shop, 2: Play Game, 0:Exit\n Input:'    )
  9         if choice == '0':
 10             break
 11         elif choice == '1':
 12             shop.buy_item()
 13         elif choice == '2':
 14             game.play_game()
 15         else:
 16             print('Choice not exist')
 17         print('------------------')
 18
 19     print('= Turn off game =')
 20
 21 if __name__ == '__main__':
 22     turn_on()
 23
```



#### 네임스페이스 (Namespace)

각 모듈은 독립된 네임스페이스(이름공간)를 가진다. 메인으로 사용되고 있는 모듈이 아닌 import된 모듈의 경우, 해당 모듈의 네임스페이스를 사용해 모듈 내부의 데이터에 접근한다.

같은 함수명을 가진 모듈을 2개 만들고, 한 쪽에서 다른 한 쪽의 모듈을 import 한 뒤 각각의 모듈의 함수를 실행시켜본다.

#### from을 사용해 모듈의 함수를 직접 import

`import 모듈명`의 경우, 모듈의 이름이 전역 네임스페이스에 등록되어 `모듈명.함수`로 사용가능하다.

모듈명을 생략하고 모듈 내부의 함수를 쓰고 싶다면, `from 모듈명 import 함수명`으로 불러들일 수 있다.

#### from 모듈명 * 을 사용해 모듈 내 모든 식별자 (변수, 함수) import

#### as로 별칭 할당

`from 모듈명 import` 또는 `import 모듈명`에서, 같은 모듈명이 존재하거나 혼동 될 수 있을 경우, 뒤에 `as`를 붙여 사용할 모듈명을 변경할 수 있다.

#### 커맨드라인에서 인자 전달

프로그램 실행 시 인자를 전달 할 수 있다. 파이썬의 내장`sys`모듈의 `argv`리스트에서 확인 할 수 있다.

리스트의 첫 번째 항목은 모듈명이 전달되므로, 2번째 항목부터 전달 된 값을 확인 할 수 있다.



```
#lol.py

~
~
~
  1 #import game
  2 import sys
  3 from game import play_game, title as game_title
  4 from shop import buy_item, title as shop_title
  5 title = 'main module'
  6
  7 if __name__ == '__main__':
  8     print(sys.argv)
  9     print('= Start game =')
 10     print(title)
 11     print(game_title)
 12     print(shop_title)
 13     play_game()
 14     buy_item()
~
```

```
#shop.py

  1 title = 'Shop Module'
  2 def buy_item():
  3     print('Buy item!')
  4
  5 if __name__ == '__main__':
  6     buy_item()
  7
  
```

```
game.py

  1 title = 'Game Module'
  2 def play_game():
  3     print('Play game')
  4
  5 if __name__ == '__main__':
  6     play_game()
~
```

-

## 패키지

패키지는 모듈들을 모아 둔 특별한 **폴더**를 뜻한다. (일반적인 폴더와는 다르다)

폴더를 패키지로 만들면 계층 구조를 가질 수 있으며, 모듈들을 해당 패키지에 모을 수 있는 역할을 한다.

패키지를 만들 때는 패키지로 사용할 폴더에 `__init__.py`파일을 넣어주면, 해당 폴더는 패키지로 취급된다. (비어있어도 무관하다)

`shop.py`와 `game.py`를 `func`패키지에 넣어본다.

```
├── func
│   ├── __init__.py
│   ├── game.py
│   └── shop.py
└── lol.py
```

패키지는 모듈과 동일하게 import할 수 있으며, 위와 같이 func패키지에 모듈들을 넣은 경우에는

`from func import game, shop`으로 기존 코드의 변경 없이 패키지에서 모듈을 가져오는 방식을 사용할 수 있다.

또는 단순히 `import func`후 `func.game`, `func.shop`을 사용하는 방식도 가능하다.


####tree(파일 구조 보기)

```
>> bew install tree						// 	tree 다운로드
>> tree									// 	tree 구조 보기
>> tree -I "__pycache__"				// 패턴으로 __pycache__폴더는 보이지 않게 하기.
>> 
functions>> touch '__init__.py'		// __init__.py 파일 생성
```


* lol.py
   
> shop.py, game.py의 위치를 옮긴 후 lol.py를 다음과 같이 수정한다.

```
 1 #import game
  2 import sys
  3 from functions.game import play_game, title as game_title
  4 from functions.shop import buy_item, title as shop_title
  5 title = 'main module'
  6
  7 if __name__ == '__main__':
  8     print(sys.argv)
  9     print('= Start game =')
 10     print(title)
 11     print(game_title)
 12     print(shop_title)
 13     play_game()
 14     buy_item()
```

#### *, \_\_all\_\_

패키지에 포함된 하위 패키지 및 모듈을 불러올 때, `*`을 사용하면 해당 모듈의 모든 식별자들을 불러온다.

이 때, 각 모듈에서 자신이 import될 때 불러와질 목록을 지정하고자 한다면 `__all__` 을 정의하면 된다.

패키지 자체를 import시에 자동으로 가져오고 싶은 목록이 있다면, 패키지의 `__init__.py`파일에 해당 항목을 import해주면 된다.









---

# 클래스 (class)

## 객체지향 프로그래밍

파이썬의 모든것은 객체이며, 객체를 사용할 때는 변수에 해당 객체를 참조(`Reference`)시켜 사용한다.  
객체는 변수와 함수를 가지며, 특별히 **객체**가 가진 **변수**와 **함수**는 각각 **속성(attribute)**과 **메서드(method)**라고 부른다.

객체는 어떠한 타입, 즉 특정한 **클래스**의 형태를 가진 **인스턴스**를 나타낸다.

### 클래스
>모든 클래스의 첫 글자는 대문자로 설정해야 한다.

클래스는 객체를 만들기 위한 틀이다. (현실에 비유할 경우, 붕어빵과 붕어빵 틀이라고 생각하는것이 일반적이다)

예를 들어, 상점(가게)를 나타내기 위한 클래스를 만든다고 해보면 아래와 같이 사용할 수 있다.

```python
class Shop:
    def __init__(self, name):
        self.name = name
```

위 코드에서, `__init__`은 클래스를 사용한 객체의 초기화 메서드이다. 객체를 생성할 때 인자를 어떻게 전달받고, 받은 인자를 이용해 어떤 객체를 생성할 지 정의할 수 있다.

위 클래스를 사용해서 객체를 생성해본다.

```python
In [1]: from class_sample import Shop
In [2]: lotteria = Shop('Lotteria')
```

위 코드는 아래 순서로 동작한다.

1. Shop 클래스가 정의되었는지 찾는다.
2. Shop 클래스형 객체를 메모리에 생성한다.
3. 생성한 객체의 초기화 메서드 `__init__`을 호출한다.
4. name값을 저장하고, 만들어진 객체를 반환한다.
5. `lotteria`변수에 반환된 객체를 할당한다.

객체의 메서드를 정의할 때, 첫 번째 인수는 항상 `self`이다. `self`에는 메서드를 호출하는 객체 자신이 자동으로 전달된다.  
이렇게 `self`가 자동으로 호출되는 이유는 클래스의 메서드를 사용할 때 어떤 객체가 해당 메서드를 사용하고 있는지 알 수 있도록 하기 위해서이다. 또한 이렇게 하나의 메서드를 여러 객체가 공유할 수 있다.

속성이나 메서드에 접근할 때는 `객체.속성명` 또는 `객체.메서드명` 을 사용한다.

**`Shop`클래스에 `show_info`메서드를 정의해본다. 해당 메서드는**

```
상점정보 (<상점명>)
```  
을 출력한다.


#### 클래스 속성

어떤 하나의 클래스로부터 생성된 객체들이 같은 값을 가지게 하고 싶을 경우, 클래스 속성(class attribute)를 사용한다.

```python
class Shop:
    description = 'Python Shop Class'
    def __init__(self, name):
        self.name = name
```

마찬가지로, 객체들에게서 각각의 인스턴스와는 별개의 공통된 메서드를 사용하게 하고 싶을 경우 클래스 메서드(class method)를 사용한다.

### 메서드

#### 인스턴스 메서드

인스턴스 메서드는 첫 번째 인수로 `self`를 가진다. 인스턴스를 이용해 메서드를 호출할 때 호출한 인스턴스가 자동으로 전달되며, 전달받은 인스턴스는 상태를 확인하거나 조작하는데에 사용된다.



##pycharm 설정

환경설정 -> project -> project Interpreter -> : pyenv 에서 관리하고 있는 python 버전을 설정해줘야한다.

project interpreter에서 톱니 바퀴를 누른 후 more 클릭
/usr/local/var/pyenv/versions/3.6.1/bin/python을 클릭하여 설정해준다.

만약 안보인다면
project interpreter에서 톱니 바퀴를 누른 후 add 클릭
/usr/local/var/pyenv/versions/3.6.1/bin/python3.6를 찾아야한다.


위의 설정은 가상환경 설정이므로 프로젝트를 진행 할 때마다 설정해줘야 한다.

keymap 화면분할 command+ shift +2

상위 폴더에서 우클릭 -> Mark Directory As... -> Sources Root


terminal ; alt + fn + f12

pycharm 내에서 사용되는 터미널의 python --version 이 2.xx버전을 사용할 경우

.zshrc 에서 두번째 줄 주석을 해제해 줘야한다
export PATH=$HOME/bin:usr/local/bin:$PATH

이렇게 한 후 사용해야 한다.



###실습


> **실습**  
> `Shop`클래스의 초기화 메서드 인자로 `shop_type`과 `address`를 추가하고, 해당 인자들을 사용해 객체의 초기값을 만들어준다  
> 
> `Shop`클래스의 인스턴스 메서드 `show_info`를 아래와 같은 결과를 출력할 수 있도록 수정해본다

```python
>>> shop.show_info()
상점 (롯데리아)
  유형: 패스트푸드
  주소: 서울시 강남구
```

```
#class_sample.py

class Shop:
    # description = 'Python Shop Class'

    def __init__(self, name, shop_type, address):
        self.name = name
        self.shop_type = shop_type
        self.address= address

    def shop_info(self):
        print('상점정보{})\n 유형: {}\n 주소 {}'.format(
            self.name,
            self.shop_type,
            self.address
        ))
```
```
# class_practice.py

from class_sample import Shop

lotteria = Shop('Lotteria', '패스트푸드', '신사역')
lotteria.shop_info()


```

> **실습**  
> `Shop`클래스에 `change_type`인스턴스 메서드를 추가하고, 상점유형(shop_type)을 변경할 수 있는 기능을 추가한다  
> 
> 새로운 `Shop`인스턴스를 하나 생성하고, `show_info()` 인스턴스 메서드를 사용해 본 후 `change_type`메서드를 사용해 `shop_type`을 변경시키고 다시 `show_info()`메서드를 실행해 결과가 잘 반영되었는지 확인한다.

```

class Shop:
    # description = 'Python Shop Class'

    def __init__(self, name, shop_type, address):
        self.name = name
        self.shop_type = shop_type
        self.address= address

    def shop_info(self):
        print('상점정보{})\n 유형: {}\n 주소 {}'.format(
            self.name,
            self.shop_type,
            self.address
        ))

    def change_type(self, shop_type):
        self.shop_type = shop_type

```

```
from class_sample import Shop

lotteria = Shop('Lotteria', '패스트푸드', '신사역')

lotteria.change_type('정크푸드점')
lotteria.shop_info()
```
#### 클래스 메서드

클래스 메서드는 클래스 속성에 대해 동작하는 메서드이다. 위의 인스턴스 메서드와 달리 호출 주체가 클래스이며, 첫 번째 인자도 클래스이다.  
만약 인스턴스가 첫 번째 인자로 주어지더라도 해당 인자의 클래스로 자동으로 바뀌어 전달된다.

클래스메서드는 `@classmethod`데코레이터를 붙여 선언하며, 첫 번째 인자의 이름은 관용적으로 `cls`를 사용한다.

> **실습**  
> `Shop`클래스에 클래스 속성 `description`을 수정하는 클래스 메서드를 작성한다.



```
class Shop:
    description = 'Python Shop Class'

    def __init__(self, name, shop_type, address):
        self.name = name
        self.shop_type = shop_type
        self.address= address

    def shop_info(self):
        print('상점정보{})\n 유형: {}\n 주소 {}'.format(
            self.name,
            self.shop_type,
            self.address
        ))

    def change_type(self, shop_type):
        self.shop_type = shop_type

    @classmethod
    def change_description(cls, description):
        cls.description = description
```

```
from class_sample import Shop

lotteria = Shop('Lotteria', '패스트푸드', '신사역')

lotteria.change_type('정크푸드점')
lotteria.shop_info()

print(Shop.description)
Shop.change_description('Changed description')
print(Shop.description)
lotteria.change_description('Changed by instance')
print(lotteria.description)
print(Shop.description)

```

#### 스태틱 메서드

스태틱 메서드는 클래스 내부에 정의된 일반 함수이며, 단지 클래스나 인스턴스를 통해서 접근할 수 있을 뿐 해당 클래스나 인스턴스에 영향을 주는 것은 불가능하다.

스태틱메서드는 `@staticmethod`데코레이터를 붙여 선언한다.


```
class Shop:
    description = 'Python Shop Class'

    def __init__(self, name, shop_type, address):
        self.name = name
        self.shop_type = shop_type
        self.address= address

    def shop_info(self):
        print('상점정보{})\n 유형: {}\n 주소 {}'.format(
            self.name,
            self.shop_type,
            self.address
        ))

    def change_type(self, shop_type):
        self.shop_type = shop_type



    @classmethod
    def change_description(cls, description):
        cls.description = description

    @staticmethod
    def print_hello():
        print('hello')
```

```
from class_sample import Shop

lotteria = Shop('Lotteria', '패스트푸드', '신사역')

lotteria.change_type('정크푸드점')
lotteria.shop_info()

print(Shop.description)
Shop.change_description('Changed description')
print(Shop.description)
lotteria.change_description('Changed by instance')
print(lotteria.description)
print(Shop.description)
print(Shop.print_hello())


```

### 속성 접근 지정자 (attribute access modifier)

#### 캡슐화

객체를 구현할 때, 사용자가 반드시 알아야 할 데이터나 메서드를 제외한 부분을 은닉시켜 정해진 방법을 통해서만 객체를 조작할 수 있도록 하는 방식.

객체의 데이터나 메서드의 은닉 정도를 결정할 때, 속성 접근 지정자를 사용한다.

- `change_type`메서드나 `change_description`클래스 메서드를 사용하지 않고도 내부 내용을 변경할 수 있다.

속성 이름을 `__`로 시작하면, 외부에서의 접근을 제한한다. 이 경우를 `private 지정자`라고 한다.

- `shop_type`의 이름을 `__shop_type`으로 바꾸고 외부에서 직접 변경해본다.

- 실제 이름은 `_<클래스명>__<속성명>`으로 되어있다.

파이썬은 속성을 실제로 사용하지 못하도록 숨기지 않고, 네임 맹글링(name mangling)이라는 기법을 사용한다. 파이썬에서는 문법적으로 `private`데이터에 대한 접근을 막는 법을 제공하지는 않는다.  
이는 개발자에게 최대한 제약을 가하지 않는다는 파이썬의 철학때문이다.


**(파이썬 튜토리얼 중)**  
As is true for modules, classes in Python do not put an absolute barrier between definition and user, but rather rely on the politeness of the user not to "break into the definition."  
모듈에서도 그렇듯이, 파이썬의 클래스는 정의와 사용자 사이에 절대적인 장벽을 놓는다기보다는 "정의를 바깥에서 깨부수지 않는" 사용자의 정중함에 의존하고 있다고 할 수 있다.

---

## 거품정렬
[wiki](https://ko.wikipedia.org/wiki/%EA%B1%B0%ED%92%88_%EC%A0%95%EB%A0%AC)

>인접한 두 원소를 검사하여 정렬하는 방법.  
>버블 정렬(Bubble Sort)은 시간 복잡도가 O(n^2)로 상당히 느리지만,   
>코드가 단순하기 때문에 자주 사용된다.   
>
>원소의 이동이 거품이 수면으로 올라오는 듯한 모습을 보이기 때문에 지어진 이름


* 두 인접한 원소를 검사하여 정렬하는 방법
* 시간 복잡도 O(n^2)
* 코드가 단순하기 때문에 자주 사용


### 버블 정렬 알고리즘 분석

* 메모리 사용공간
	* n개의 원소에 대하여 n개의 메모리 사용

* 연산시간
	* 최선의 경우: 자료가 이미 정렬되어 있는 경우

:: 비교횟수 : i번째 원소를 (n-1)번 비교하므로, n(n-1)/2번
:: 자리교환횟수 : 자리교환이 발생하지 않음

- 최악의 경우 : 자료가 역순으로 정렬되어 있는 경우
::비교횟수: i번째 원소를 (n-1)번 비교하므로 n(n-1)/2번
::자리교환횟수 : i번째 원소를 (n-1)번 교환하마ㅡ로 n(n-1)/2번

평균 시간 복잡도는 O(n^2)이 됨


```
import random

source = [x for x in range(10)]
random.shuffle(source)

def bubblesort(x):
    length = len(x)-1

    for i in range(length):
        for j in range(length -i):
            if x[j] > x[j+1]:
                x[j], x[j+1] = x[j+1], x[j]
                # print(x)

            # print(x)

    return x

bubblesort(source)

print(source)
```

---

