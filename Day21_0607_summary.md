## ipython
### autoreload

```
>>> %load_ext autoreload
>>> %autoreload 2
```

#### Usage
The following magic commands are provided:

##### %autoreload
Reload all modules (except those excluded by %aimport) automatically now.

##### %autoreload 0
Disable automatic reloading.

##### %autoreload 1
Reload all modules imported with %aimport every time before executing the Python code typed.

##### %autoreload 2
Reload all modules (except those excluded by %aimport) every time before executing the Python code typed.

##### %aimport
List modules which are to be automatically imported or not to be imported.

##### %aimport foo
Import module ‘foo’ and mark it to be autoreloaded for %autoreload 1

##### %aimport -foo
Mark module ‘foo’ to not be autoreloaded.


## python 내장함수

### hasattr
* 문자열이 있는지 확인할 수 있는 파이썬 내장함수

## 오늘의 Git

> 이미 push한 데이터를 같은 commit으로 덮어 씌우기 

```
>>> git commit --amend
>>> git push origin master --force
```

>`>>> git add -A` 사용 후 특정파일만 제외 시키기

```
>>> git reset django_app/introduction_to_models/models/multi_table_inheritance.py

```

### ForeignKey 또는 ManyToManyField에서 related\_name 또는 related\_query\_name을 사용하는 경우

* oreignKey 또는 ManyToManyField에서 related\_name 또는 related_query_name을 사용하는 경우 필드의 고유 한 역 이름 및 쿼리 이름을 항상 지정해야합니다. 이 클래스의 필드는 매번 속성 (related\_name 및 related\_query\_name 포함)에 대해 동일한 값을 가질 때마다 각 하위 클래스에 포함되므로 일반적으로 추상 기본 클래스에서 문제가 발생합니다.
* `%(class)s`: 필드가 사용되는 하위 클래스의 하위 사례 이름으로 대체
* `%(app_label)s`: 하위 클래스가 포함 된 하위 사례 이름으로 바뀝니다. 설치된 각 응용 프로그램 이름은 고유해야하며 각 응용 프로그램 내의 모델 클래스 이름도 고유해야하므로 결과 이름이 달라집니다.


