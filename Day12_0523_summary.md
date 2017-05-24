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


### get/set속성값과 프로퍼티

파이썬에서는 지원하지 않지만, 어떤 언어들은 외부에서 접근할 수 없는 `private`객체 속성을 지원한다. 이 경우, 객체에서는 해당 속성을 읽고 쓰기 위해 `getter`, `setter`메서드를 사용해야 한다.

파이썬에서는 해당 기능을 프로퍼티(property)를 사용해 간편히 구현한다.

- 실제 getter, setter를 구현해본다.

```python
@property
def name(self):
    return self.__name

@name.setter
def name(self, new_name):
    self.__name = new_name
    print('Set new name ({})'.format(self.__name))
```

`setter`프로퍼티를 명시하지 않으면 읽기전용이 되어 외부에서 조작할 수 없게 된다.

```
class Shop:
    description = 'Python Shop Class'

    def __init__(self, name, shop_type, address):
        self.name = name
        self.__shop_type = shop_type
        self.address= address

    def shop_info(self):
        print('상점정보: {}\n유형: {}\n주소: {}'.format(
            self.name,
            self.__shop_type,
            self.address
        ))

    def change_type(self, shop_type):
        self.__shop_type = shop_type



    @classmethod
    def change_description(cls, description):
        cls.description = description

    @staticmethod
    def print_hello():
        print('hello')
```
```
from class_sample import Shop

lotteria = Shop('롯데리아', '패스트푸드', '신사역')

lotteria.change_type('PC방')
lotteria.shop_info()
# print(lotteria.__shop_type)

lotteria.__shop_type = '다시 패스트푸드점으로'
lotteria.shop_info()
print(lotteria.__shop_type)

for item in dir(lotteria):
    print(item)


```


### 상속 (Inheritance)

거의 비슷한 기능을 수행하나, 약간의 추가적인 기능이 필요한 다른 클래스가 필요할 경우 기존의 클래스를 상속받은 새 클래스를 사용하는 형태로 문제를 해결할 수 있다.

이 때, 상속 되는 클래스를 부모(상위)클래스라고 하며, 상속을 받는 클래스는 자식(하위)클래스라고 한다.

상속을 받을때는 클래스의 정의 다음 괄호에 부모 클래스를 적어주면 된다.

```python
class Restaurant(Shop):
    pass
```

상속받은 클래스는 부모 클래스의 모든 속성과 메서드를 사용할 수 있다.

```
class Shop:
    description = 'Python Shop Class'

    def __init__(self, name, shop_type, address):
        self.name = name
        self.__shop_type = shop_type
        self.address= address

    def shop_info(self):
        print('상점: {}\n유형: {}\n주소: {}'.format(
            self.name,
            self.__shop_type,
            self.address
        ))

    @property
    def shop_type(self):
        return self.__shop_type

    @shop_type.setter
    def shop_type(self, new_shop_type):
        available_type_set = {
            '패스트푸드점',
            '편의점',
            'PC방'
        }

        if new_shop_type in available_type_set:
            self.__shop_type = new_shop_type

        else:
            print('{}은 허용되지 않습니다'.format(new_shop_type))

    @classmethod
    def change_description(cls, description):
        cls.description = description

    @staticmethod
    def print_hello():
        print('hello')

class PCroom(Shop):
    pass

```
```
from class_sample import Shop, PCroom

lotteria = Shop('롯데리아', '패스트푸드', '신사역')
xeno = PCroom('제노','PC방', '신사역')
xeno.shop_info()

```


#### 메서드 오버라이드

상속받은 클래스에서, 부모 클래스의 메서드와는 다른 동작을 하도록 할 수 있다. 이 경우 부모 클래스의 메서드를 덮어씌워서 사용하도록 하며, 이 방법을 메서드 오버라이드(method override)라고 한다.

- `show_info`메서드에서 `상점`이 아닌 `식당`으로 표현되도록 메서드를 오버라이드해 새로 정의해본다.

```
"""
public
    외부에서 제한없이 접근/수정가능

protected
    외부에서는 접근 불가능, 상속받은 클래스에서는 접근 가능

private
    내부에서만 접근수정 가능
        -> 외부 접근 가능하도록 property사용
"""

class Shop:
    description = 'Python Shop Class'

    def __init__(self, name, shop_type, address):
        self.name = name
        self.__shop_type = shop_type
        self.address= address

    def shop_info(self):
        print('상점: {}\n유형: {}\n주소: {}'.format(
            self.name,
            self.__shop_type,
            self.address
        ))

    @property
    def shop_type(self):
        return self.__shop_type

    @shop_type.setter
    def shop_type(self, new_shop_type):
        available_type_set = {
            '패스트푸드점',
            '편의점',
            'PC방'
        }

        if new_shop_type in available_type_set:
            self.__shop_type = new_shop_type

        else:
            print('{}은 허용되지 않습니다'.format(new_shop_type))

    @classmethod
    def change_description(cls, description):
        cls.description = description

    @staticmethod
    def print_hello():
        print('hello')

class PCroom(Shop):
    def shop_info(self):
        print('상점: {}\n유형: {}\n주소: {}'.format(
            self.name,
            self.shop_type,
            self.address
        ))
        


```

```
from class_sample import Shop, PCroom

lotteria = Shop('롯데리아', '패스트푸드', '신사역')
xeno = PCroom('제노','PC방', '신사역')
xeno.shop_info()

```



* public
    * 외부에서 제한없이 접근/수정가능

* protected
    * 외부에서는 접근 불가능, 상속받은 클래스에서는 접근 가능

* private
    * 내부에서만 접근수정 가능
    * : -> 외부 접근 가능하도록 property사용

    


#### 부모 클래스의 메서드를 호출 (super)

자식클래스의 메서드에서 부모 클래스에서 사용하는 메서드의 전체를 새로 쓰는것이 아닌, 부모 클래스의 메서드를 호출 후 해당 내용으로 새로운 작업을 해야 할 경우 `super()`메서드를 사용해서 부모 클래스의 메서드를 직접 호출할 수 있다.

```python
class Restaurant(Shop):
    def __init__(self, name, shop_type, address, rating):
        super().__init__(name, shop_type, address)
        self.rating = rating
```

위 코드의 경우, `super()`메서드를 사용해서 부모의 `__init__` 메서드를 호출한다.

```
"""
public
    외부에서 제한없이 접근/수정가능

protected
    외부에서는 접근 불가능, 상속받은 클래스에서는 접근 가능

private
    내부에서만 접근수정 가능
        -> 외부 접근 가능하도록 property사용
"""

class Shop:
    description = 'Python Shop Class'

    def __init__(self, name, shop_type, address):
        self.name = name
        self.__shop_type = shop_type
        self.address= address

    def shop_info(self):
        print('상점: {}\n유형: {}\n주소: {}'.format(
            self.name,
            self.__shop_type,
            self.address
        ))

    @property
    def shop_type(self):
        return self.__shop_type

    @shop_type.setter
    def shop_type(self, new_shop_type):
        available_type_set = {
            '패스트푸드점',
            '편의점',
            'PC방'
        }

        if new_shop_type in available_type_set:
            self.__shop_type = new_shop_type

        else:
            print('{}은 허용되지 않습니다'.format(new_shop_type))

    @classmethod
    def change_description(cls, description):
        cls.description = description

    @staticmethod
    def print_hello():
        print('hello')

class PCroom(Shop):

    def __init__(self, name, shop_type, address, price):
        super().__init__(name, shop_type, address)
        self.price = price

    def shop_info(self):
        print('상점: {}\n유형: {}\n주소: {}\n요금: {}'.format(
            self.name,
            self.shop_type,
            self.address,
            self.price
        ))


```

```
from class_sample import Shop, PCroom

lotteria = Shop('롯데리아', '패스트푸드', '신사역')
xeno = PCroom('제노','PC방', '신사역', 1300)
xeno.shop_info()

```


### 다형성과 덕 타이핑
> 다형성: 동일한 실행이지만, 다른 동작을 수행할 수 있도록 허용하는 것

파이썬은 다형성(polymorphism)을 덕 타이핑(duck typing)이라는 방식으로 구현한다.  
덕 타이핑은 문자 그대로  

```
`오리`는 `꽥꽥`하고 우므로, `꽥꽥`하고 우는것은 `오리`로 취급한다
```

라는 방식을 사용한다.

조금 더 자세한 예를 들자면,  
어떠한 객체에 `울기`라는 메서드가 존재할 때, `꽥꽥`이라는 결과를 리턴한다면 해당 객체는 `오리`로 취급되며 `삐약삐약`이라는 결과를 리턴한다면 `병아리`로 취급된다.

다형성을 지원하는 프로그래밍 언어에서는 같은 이름의 함수에서 서로 다른 기능을 하는 방식으로 프로그래밍을 할 수 있다.  
파이썬에서는 각 객체의 타입과 전혀 상관없이 해당 객체에서 만든 같은 이름의 메서드들을 실행할 수 있다.

- User, Food, Drink와 eat을 사용해 다형성을 구현해본다.

```
"""
public
    외부에서 제한없이 접근/수정가능

protected
    외부에서는 접근 불가능, 상속받은 클래스에서는 접근 가능

private
    내부에서만 접근수정 가능
        -> 외부 접근 가능하도록 property사용
"""

class Shop:
    description = 'Python Shop Class'

    def __init__(self, name, shop_type, address):
        self.name = name
        self.__shop_type = shop_type
        self.address= address

    def shop_info(self):
        print('상점: {}\n유형: {}\n주소: {}'.format(
            self.name,
            self.__shop_type,
            self.address
        ))

    @property
    def shop_type(self):
        return self.__shop_type

    @shop_type.setter
    def shop_type(self, new_shop_type):
        available_type_set = {
            '패스트푸드점',
            '편의점',
            'PC방'
        }

        if new_shop_type in available_type_set:
            self.__shop_type = new_shop_type

        else:
            print('{}은 허용되지 않습니다'.format(new_shop_type))

    @classmethod
    def change_description(cls, description):
        cls.description = description

    @staticmethod
    def print_hello():
        print('hello')

class PCroom(Shop):

    def __init__(self, name, shop_type, address, price):
        super().__init__(name, shop_type, address)
        self.price = price

    def shop_info(self):
        print('상점: {}\n유형: {}\n주소: {}\n요금: {}'.format(
            self.name,
            self.shop_type,
            self.address,
            self.price
        ))

# 다형성 및 덕 타이핑
# 다형성: 동일한 실행이지만, 다른 동작을 수행할 수 있도록 허용하는 것
class User:
    def __init__(self, name):
        self.name = name

    def eat(self,anything):
        anything.eat()

    def eat_something(self, something):
        something.eat()

    def eat_food(self, food):
        food.eat()

    def eat_drink(self, drink):
        drink.eat()


class Something:
    def __init__(self, name):
        self.name = name

    def eat(self):
        print('{}는 무엇인지 몰라 먹을 수 없다!'.format(self.name))

class Food(Something):
    def eat(self):
        print('{}를 먹었다. 배가 부르다'.format(self.name))

class Drink(Something):
    def eat(self):
        print('{}를 마셨다. 갈증이 해소된다.'.format(self.name))

```

```
from class_sample import Shop, PCroom
from class_sample import User, Something, Food, Drink

lotteria = Shop('롯데리아', '패스트푸드', '신사역')
xeno = PCroom('제노','PC방', '신사역', 1300)
xeno.shop_info()

user = User('박윤식')
s = Something('알 수 없는 무언가')
f = Food('햄버거')
d = Drink('제로콜라')

# user.eat_something(s)
# user.eat_food(f)
# user.eat_drink(d)

#다양성을 사용한 경우

user.eat(s)
user.eat(f)
user.eat(d)
```



## 실습



```
@property를 출력할 때는 ()이 아니라 =로 표현해야한다.	//예제 다시한번 살펴보기!!
```
---

# 정규표현식 (Regular Expressions)

특정한 패턴에 일치하는 복잡한 문자열을 처리할 때 사용하는 기법. 

파이썬에서는 표준 모듈 `re`를 사용해서 정규표현식을 사용할 수 있다.

```python
import re
result = re.match('Lux', 'Lux, the Lady of Luminosity')
```

위에서 `match`의 첫 번째 인자에는 패턴이 들어가며, 두 번째 인자에는 문자열 소스가 들어간다. `match()`는 소스와 패턴의 일치 여부를 확인하고, 일치할 경우 `Match object`를 반환한다.

조금 복잡하거나 자주 사용되는 패턴은 미리 **컴파일**하여 속도를 향상시킬 수 있다.

```python
pattern1 = re.compile('Lux')
```

컴파일된 패턴객체를 문자열 대신 첫 번째 인자로 사용 가능하다.


## match : 시작부터 일치하는 패턴 찾기

```python
>>> import re
>>> source = 'Lux, the Lady of Luminosity'
>>> m = re.match('Lux', source)
>>> if m:
...   print(m.group())
...
Lux
```

`match()`는 시작부분부터 일치하는 패턴만 찾기 때문에, `Lady`라는 패턴으로는 찾을 수 없다.

```python
>>> m = re.match('.*Lady', source)
>>> if m:
...   print(m.group())
...
Lux, the Lady
```

위 결과는 다음을 의미한다.

- `.`은 문자 1개를 의미
- `*`는 해당 패턴이 0회 이상 올 수 있다는 의미이다
- 따라서 `.*Lady`는 앞에 아무 문자열(또는 빈) 이후 Lady로 끝나는 패턴을 의미한다


## search : 첫 번째 일치하는 패턴 찾기

`*`패턴 없이 `Lady`만 찾을 경우, 문자열 전체에서 일치하는 부분을 찾는 `search()`를 사용한다.

```python
>>> m = re.search('Lady', source)
>>> if m:
...   print(m.group())
...
Lady
```

## findall : 일치하는 모든 패턴 찾기

```python
>>> m = re.findall('y', source)
>>> m
>>> ['y', 'y']
>>> m = re.findall('y..', source)
>>> m
['y o']
```

끝자리의 `y`는 뒤에 문자가 더 없으므로 포함되지 않으므로, `?`를 추가한다.  
`.`은 문자 1개를 의미하며, `?`는 0 또는 1회 반복을 사용한다. `.?`은 문자가 0 또는 1회 올 수 있음을 의미한다.

```python
>>> m = re.findall('y.?.?', source)
>>> m
['y o', 'y']
```

## split : 패턴으로 나누기

문자열의 `split()`메서드와 비슷하지만 패턴을 사용할 수 있다.

```python
>>> m = re.split('o', source)
>>> m
['Lux, the Lady ', 'f Lumin', 'sity']
```

## sub : 패턴 대체하기

문자열의 `replace()`메서드와 비슷하지만 패턴을 사용할 수 있다.

```python
>>> m = re.sub('o', '!', source)
>>> m
'Lux, the Lady !f Lumin!sity'
```

```
import re

source = 'Lux, the Lady of Luminosity'
m = re.match('Lady', source)
m = re.match('.*Lady', source)
m = re.search('g', source)
m = re.match(r'(.*)(Lady)(.*)', source)
l = re.findall('y.?.?', source)
print(l)

if m:
    print(m.groups())


print(source.split())
print(source.split('o'))
print(re.split('...y', source))
print(re.sub('...y', '!!!!', source))
```
```
➜  12.re python basic.py
['y o', 'y']
('Lux, the ', 'Lady', ' of Luminosity')
['Lux,', 'the', 'Lady', 'of', 'Luminosity']
['Lux, the Lady ', 'f Lumin', 'sity']
['Lux, the ', ' of Lumino', '']
Lux, the !!!! of Lumino!!!!

```



## 정규표현식의 패턴 문자

패턴|문자
---|---
\\d|숫자
\\D|비숫자
\\w|문자
\\W|비문자
\\s|공백 문자
\\S|비공백 문자
\\b|단어 경계 (\w와 \W의 경계)
\\B|비단어 경계

```python
import string
import re

source = 'Lux, the Lady of Luminosity'
m = re.match('Lady', source)
m = re.match('.*Lady', source)
m = re.search('g', source)
m = re.match(r'(.*)(Lady)(.*)', source)
l = re.findall('y.?.?', source)

printable = string.printable
print(printable)
print(re.findall('\w', printable))
print(re.findall('\W', printable))
print(re.findall('\d', printable))
print(re.findall('\D', printable))
print(re.findall(r'\s', printable))
print(re.findall(r'\S', printable))
print(re.findall(r'\b', printable))
print(re.findall(r'\B', printable))
```

## 정규표현식의 패턴 지정자 (Pattern specifier)

**expr**은 정규표현식을 말한다

패턴|의미
---|---
abc|리터럴 `abc`
(expr)|expr
expr1 \| expr2 | expr1 또는 expr2
`.` | `\n`을 제외한 모든 문자
`^` | 소스문자열의 시작
`$` | 소스문자열의 끝
expr`?` | 0 또는 1회의 expr
expr`*` | 0회 이상의 최대 expr
expr`*?`| 0회 이상의 최소 expr
expr`+` | 1회 이상의 최대 expr
expr`+?`| 1회 이상의 최소 expr
expr`{m}`| m회의 expr
expr`{m,n}`| m에서 n회의 최대 expr
expr`{m,n}?` | m에서 n회의 최소 expr
[abc] | a or b or c
[^abc] | not (a or b or c)
expr1(?=expr2) | 뒤에 expr2가 오면 expr1에 해당하는 부분
expr1(?=expr2) | 뒤에 expr2까 오지 않으면 expr1에 해당하는 부분
(?<=expr1)expr2 | 앞에 expr1이 오면 expr2에 해당하는 부분
(?<!expr1)expr2 | 앞에 expr1이 오지 않으면 expr2에 해당하는 부분

[점프 투 파이썬 - 정규표현식 (https://wikidocs.net/4309)](https://wikidocs.net/4309)




**스토리**

Born to the prestigious Crownguards, the paragon family of Demacian service, Luxanna was destined for greatness. She grew up as the family's only daughter, and she immediately took to the advanced education and lavish parties required of families as high profile as the Crownguards. As Lux matured, it became clear that she was extraordinarily gifted. She could play tricks that made people believe they had seen things that did not actually exist. She could also hide in plain sight. Somehow, she was able to reverse engineer arcane magical spells after seeing them cast only once. She was hailed as a prodigy, drawing the affections of the Demacian government, military, and citizens alike.

As one of the youngest women to be tested by the College of Magic, she was discovered to possess a unique command over the powers of light. The young Lux viewed this as a great gift, something for her to embrace and use in the name of good. Realizing her unique skills, the Demacian military recruited and trained her in covert operations. She quickly became renowned for her daring achievements; the most dangerous of which found her deep in the chambers of the Noxian High Command. She extracted valuable inside information about the Noxus-Ionian conflict, earning her great favor with Demacians and Ionians alike. However, reconnaissance and surveillance was not for her. A light of her people, Lux's true calling was the League of Legends, where she could follow in her brother's footsteps and unleash her gifts as an inspiration for all of Demacia.

```python
story = '''Born to the prestigious Crownguards, the paragon family of Demacian service, Luxanna was destined for greatness. She grew up as the family's only daughter, and she immediately took to the advanced education and lavish parties required of families as high profile as the Crownguards. As Lux matured, it became clear that she was extraordinarily gifted. She could play tricks that made people believe they had seen things that did not actually exist. She could also hide in plain sight. Somehow, she was able to reverse engineer arcane magical spells after seeing them cast only once. She was hailed as a prodigy, drawing the affections of the Demacian government, military, and citizens alike.

As one of the youngest women to be tested by the College of Magic, she was discovered to possess a unique command over the powers of light. The young Lux viewed this as a great gift, something for her to embrace and use in the name of good. Realizing her unique skills, the Demacian military recruited and trained her in covert operations. She quickly became renowned for her daring achievements; the most dangerous of which found her deep in the chambers of the Noxian High Command. She extracted valuable inside information about the Noxus-Ionian conflict, earning her great favor with Demacians and Ionians alike. However, reconnaissance and surveillance was not for her. A light of her people, Lux's true calling was the League of Legends, where she could follow in her brother's footsteps and unleash her gifts as an inspiration for all of Demacia.'''
```

위와같이 `story`변수에 스토리 문자열을 할당한다.

```python
re.findall('Lux', story)
re.findall('Lux|her|she', story)
re.findall('[Ll]ux|[Hh]er|[Ss]he', story)
re.findall('^Born', story)
re.findall('Demacia$', story)
re.findall('was', story)
re.findall('(?<=she) was', story)
re.findall('\w+(?<!she) was', story)
re.findall('\bwas\b', story)
re.findall(r'\bwas\b', story)
```

`\`로 시작하는 패턴 문자나, 정규표현식에서 `\`를 직접 사용해야 하는 경우 문자열의 **이스케이프**문을 사용하지 않고, 정규식 내에서 `\`로 해석됨을 나타내기 위해 앞에 `r`을 붙인다 (raw string으로 취급된다)

정규표현식의 패턴에는 항상 앞에 `r`을 붙인다고 생각하는 것이 좋다. (만약 정규표현식 내부에서 `\`를 쓰지 않을 경우, `r`을 붙임과 붙이지 않음은 같은 결과를 가져온다)

## 매칭 결과 그룹화

정규표현식 패턴중 괄호로 둘러싸인 부분이 있을 경우, 결과는 해당 괄호만의 그룹으로 저장된다.

Match객체의 `group()`함수는 매치된 전체 문자열을 리턴하며, `groups()`함수는 지정된 그룹 리스트를 리턴해준다.  
`group(0)`은 `group()`과 같은 동작을 하며, `group(숫자)`는 매치된 `숫자`번째의 그룹요소를 리턴해준다.

```python
s = re.search(r'\w+\w(was)', story)
s.groups()
s.group(0)
s.group(1)
```

`(?P<name>expr)` 패턴을 사용하면 매칭된 표현식 그룹에 이름을 붙여 사용할 수 있다.

```python
m = re.search(r'(?P<before>\w+)\s+(?P<was>was)\s+(?P<after>\w+)', story)
m.groups()
m.group('before')
m.group('was')
m.group('after')
```


## 최소일치와 최대일치

```python
<html><body><h1>HTML</h1></body></html>
```

위 항목을

```python
m = re.match(r'<.*>', html)
```

로 검색하면, `.*`표현식이 첫 번째 `>`에서 멈추는것이 아니라 맨 마지막 `>`까지 검색을 진행한다.  
`*`이나 `+`에 최소일치인 `?`를 붙여주면, 표현식 다음부분에 해당하는 문자열이 처음 나왔을 때 그 부분까지만 일치시키고 검색을 마친다.

## 실습

아래 실습들은 위의 `story`변수 문자열을 소스로 사용한다.

1. `{m}`패턴지정자를 사용해서 `a`로 시작하는 4글자 단어를 전부 찾는다.

```
>>> result = re.findall(r'\ba\w{3}\b', story)

```

2. r로 끝나는 모든 단어를 찾는다.

```
>>> result = re.findall(r'\w+r\b', story)
```
3. a,b,c,d,e중 아무 문자나 3번 연속으로 들어간 단어를 찾는다.
	> ex) b[eca]me
```
result = re.findall(r'\w*[abce]{3}\w*', story)

```

4. `re.sub`를 사용해서 `,`로 구분된 앞/뒤 단어에 대해 앞단어는 대문자화 시키고, 뒷단어는 대괄호로 감싼다. 이 과정에서, 각각의 앞/뒤에 `before`, `after`그룹 이름을 사용한다.

```
def re_change(m):
    return '{}{}[{}]'.format(m.group('before').upper(), m.group('center'), m.group('after'))

p = re.compile(r'(?P<before>\w+)(?P<center>\s*,\s*)(?P<after>\w+)')
result = re.sub(p, re_change, story)
print(result)
```