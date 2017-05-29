>[djangogirls 문서](https://tutorial.djangogirls.org/ko/django_models/)

##장고 모델


## 객체(Object)

프로그래밍 개발 방법 중에는 객체 지향 프로그래밍(object oriented programming)이라 부르는 개념이 있어요. 이 개발 방법은 프로그램이 어떻게 작동해야 하는지 모든 것을 하나하나 지시하는 것 대신, 모델을 만들어 그 모델이 어떤 역할을 가지고 어떻게 행동해야 하는지 정의하여 서로 알아서 상호작용할 수 있도록 만드는 것입니다.

그렇다면 객체란 무엇일까요? 객체란 **속성(변수)**과 **행동(함수)**을 모아놓은 것이라 할 수 있어요. 객체란 개념이 낯설게 느껴지지만, 예를 들어보면 별것 아님을 알게 될 거에요.



어플리케이션 만들기

잘 정돈된 상태에서 시작하기 위해, 프로젝트 내부에 별도의 애플리케이션을 만들어볼 거에요. 처음부터 모든 것이 잘 준비되어있다면 훌륭하죠. 애플리케이션을 만들기 위해 콘솔 창(djangogirls 디렉토리에서 manage.py 파일)에서 아래 명령어를 실행하세요.

```
(myvenv) ~/djangogirls/django_app$ ./manage.py startapp blog

```

djangogirls 폴더에서 pycharm 실행

터미널 실행 후 

```
$ cat .python-version		//

$ pyenv activate djangogirls_env		

```
Preference -> Project Interpreter 에서

`usr/local/var/pyenv/versions/djangogirls_env`
지정

django_app 폴더 우클릭 후 
Mark Directory as -->> Source Root 지정

애플리케이션을 생성한 후 장고에 사용해야 한다고 알려줘야 합니다. 이 역할을 하는 파일이 mysite/settings.py입니다. 이 파일 안에서 INSTALLED_APPS를 열어, )바로 위에 'blog'를 추가하세요. 최종 결과물은 아래와 다음과 같을 거예요. :

`mysite/settings.py`

```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog',		// 추가
]
```

수정후 
django_app 폴더에서 git commit

```
$ git add -A
$ git commit -m 'add blog app'
```


블로그 글 모델 만들기

모든 Model 객체는 blog/models.py 파일에 선언하여 모델을 만듭니다. 이 파일에 우리의 블로그 글 모델도 정의할 거에요.

blog/models.py 파일을 열어서 안에 모든 내용을 삭제한 후 아래 코드를 추가하세요.


`blog/models.py`

```
from django.db import models
from django.utils import timezone

#from : class // import : method



class Post(models.Model):
    author = models.ForeignKey('auth.User')
    title = models.CharField(max_length=200)
    text = models.TextField()
    created_date = models.DateTimeField(
            default=timezone.now)
    published_date = models.DateTimeField(
            blank=True, null=True)

    def publish(self):
        self.published_date = timezone.now()
        self.save()

    def __str__(self):
        return self.title

```

##데이터베이스에 모델을 위한 테이블 만들기
>변경사항을 데이터베이스에 반영
```
$ ./manage.py migrate
```

##sqlite brower설치
>`http://sqlitebrowser.org/`
>   
sqlite brower앱 실행 후 django_app폴더의 `db.sqlite3`열기


##터미널
>장고에서 기본 앱이 있는데 어떤 것을 할 것인지는 모르기때문에 migration을 실행하고 `makemigrations` 을 통해 작성하기 위한 중간과정을 위한 단계
>또다시 `./manage.py migrate`를 실행하여 변경된 사항 저장

```
$ ./manage.py makemigrations
```

```
./manage.py migrate

python manage.py migrate
```
위의 두 명령은 같은 효과를 보인다.

`./`은 사전에 설정 되어 있는 설정값이 적용이 되기때문에 가능하지만 만약 설정되어있지 않으면 오류를 일으킨다.




#장고 관리자

관리자 화면을 한국어로 변경하길 원할 경우 'settings.py'중 LANGUAGE\_CODE = 'en-us'를 LANGUAGE\_CODE = 'ko'로 바꾸세요.

방금 막 모델링 한 글들을 장고 관리자에서 추가하거나 수정, 삭제할 수 있어요.

이제 blog/admin.py 파일을 열어서 내용을 다음과 같이 바꾸세요.

`blog/admin.py`

```
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

>터미널에서 다음을 실행 후 브라우저에서 127.0.0.1:8000/admin 실행

`./manage.py runserver`


>아직 id와 pw가 없다.
이를 위해 새로운 터미널을 실행 후 다음을 입력하여 id와 pw를 설정한다.

```
django_app>> ./manage.py createsuperuser
```

>로그인 후 테스트 블로그 포스트를 작성한다.
작성한 포스트를 확인하기 위해서는 DBBrowser에서 데이터보기 항목에 작성한 테이블인 blog_post	를 선택하면 작성한 내용을 확인 할 수 있다.


#URL

장고 URL은 어떻게 작동할까요?

코드 에디터에서 mysite/urls.py파일을 열면 아래 내용이 보일 거에요.

`
mysite/urls.py
`

```
"""mysite URL Configuration

[...]
"""
from django.conf.urls import url
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', admin.site.urls),
]
```

#정규표현식(Regex)


장고가 URL을 뷰에 매칭시키는 방법이 궁금하죠? 이 부분은 조금 어렵게 느껴질 수 있어요. 장고는 regex를 사용하는데, 이는 정규표현식(regular expressions)의 줄임말입니다. 정규식은 정말 (아주!) 많은 검색 패턴의 규칙을 가지고 있어요. 정규식은 어려운 내용이라 자세하게 알아보지 않을 거에요.

URL패턴 만드는 방법이 궁금하다면, 다음 표기법을 확인하세요. 이 중 몇 가지 규칙만 사용할 거에요.

```
^ : 문자열이 시작할 떄
$ : 문자열이 끝날 때
\d : 숫자
: 바로 앞에 나오는 항목이 계속 나올 때
() : 패턴의 부분을 저장할 때
```

이외에도 문자열을 이용해 url을 만들 수 있어요.

http://www.mysite.com/post/12345/라는 사이트가 있다고 합시다. 여기에서 12345는 글 번호를 의미합니다.

뷰마다 모든 글 번호을 일일이 매기는 것은 정말 힘들죠. 정규표현식으로 url패턴을 만들어 숫자값과 매칭되게 할 수 있어요. 이렇게 말이죠. `^post/(\d+)/$. 어떤 뜻인지 하나씩 살펴봅시다.`

* ^post/ : url이(오른쪽부터) post/로 시작합니다.
* (\d+) : 숫자(한 개 이상)가 있습니다. 이 숫자로 조회하고 싶은 게시글을 찾을 수 있어요.
* / : / 뒤에 문자가 있습니다.
* $ : url 마지막이 /로 끝납니다.



`url.py`

```
from django.conf.urls import url
from django.contrib import admin
from blog import views

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^$', views.post_list),
]

```

`view.py`

```
from django.http import HttpResponse
from django.shortcuts import render

# Create your views here.
def post_list():
    return HttpResponse('Post List')



```

* **[HttpResponse](https://docs.djangoproject.com/en/1.11/ref/request-response/)** http protocal을 통해서 ()안의 내용을 출력

#장고 뷰 만들기

`view.py`

```
from django.http import HttpResponse
from django.shortcuts import render

# Create your views here.
def post_list(request):
   
    return render(request, 'blog/post_list.html')

```


django_app폴더에 templates폴더를 만들고 그안에 blog폴더를 다시 만들고 post_list.html파일을 만든다.

`django_app/mysite/settings.py`

```

# Build paths inside the project like this: os.path.join(BASE_DIR, ...)
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
print('BASE_DIR:', BASE_DIR)
# os.path.join을 사용해서 TEMPLATE_DIR변수에 django_app/templates폴더의 경로를 할당
TEMPLATE_DIR = os.path.join(BASE_DIR, 'templates')
print('TEMPLATE_DIR:', TEMPLATE_DIR)
```
```

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [
            TEMPLATE_DIR
        ],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```


####git commit

```
django_app>>

$ git add/blog/admin.py
$ git add blog/models.py
$ git add blog/migrations/
$ git commit -m 'Create Post model, admin register Post'
```

```
django_app>>

$ git add -A
$ git commit -m 'TEMPLATE_DIR setting, and post_list view'
```

###ORM(Object-relational mapping)



장고안에서 orm 을 파이썬 언어처럼 쓸 수 있다.
데이터베이스를 객체 지향 처럼 쓸 수 있게 해준다.


##장고 쉘

```
django_app>>

$ ./manage.py shell

```

```
$ from blog.models import Post
$ Post.objects.all()

$ pl = Post.objects.all()
$ pl.query
$ print(pl.query)

```

게시물 작성

```
$ Post.objects.create(title='Test Title', text = 'Test Text')

```
이와 같이하면 오류가 뜬다..

```
$ from django.contrib.auth.models import User

$ user = User.objects.get(id = 1)
$ user
<User: archys>

$ Post.objects.create(title = 'Test Title', text = 'Test Text', author = user)

<Post : Test Title>
```

```
$ Post.objects.all()
```
이렇게 추가된 것을 확인 할 수 있다.

## 필터링하기

```
$ Post.objects.filter(title__contains='test')
```
title에 'test'가 포함된 단어를 찾는다.

####게시일을 기준으로 작성한 글을 필터링하기

filter는 해당조건을 찾아 리스트형태로 가져온다.

```
$ from django.utils import timezone
$ Post.objects.filter(published_date__lte = timezone.now())
```


get은 해당조건에 일치하는 하나.한개를 가져와서 인스턴스로 가져와 쓸수 있게 해준다.

```
$ post = Post.objects.get(title = 'Test Title')
$ post
<Post: Test Title>
```
위에서 찾은 post(타임라인)을 기준으로 필터링하기

```
$ post.publish()
$ Post.objects.filter(published_date__lte = timezone.now())
```

 
 ---
 
# 템플릿 동적 데이터
---

# 쿼리셋

---

보통 데이터를 전달할 때에는 딕셔너리로 전달한다.
`view.py`

```
from django.http import HttpResponse
from django.shortcuts import render

def post_list(request):
    context = {
        'title' : 'PostList from post_list view',

    }
    return render(request, 'blog/post_list.html', context = context)


```

`post_list.html`

```
...
   <div>
        <h1><a href="#">Django Girls Blog</a></h1>
        <h3>{{title}}</h3>
    </div>
...

```

`views.py`

```

from django.shortcuts import render
from .models import Post


def post_list(request):
    # posts 변수에 ORM을 이용해서 전체 Post의 리스트(쿼리셋)를 대입
    posts = Post.objects.all()
    context = {
        'title' : 'PostList from post_list view',
        'posts' : posts,
    }
    return render(request, 'blog/post_list.html', context = context)





```

```
...
   <div>
        <h1><a href="#">Django Girls Blog</a></h1>
        <h3>{{title}}</h3>
    </div>

    <div>
        {% for post in posts %}
        <div>
            <h3 style="color:skyblue">{{post.title}}</h3>
            <p style="color:pink">{{post.text}}</p>
        </div>
        {% endfor %}

    </div>...
```

filter / timezone적용하기

```
from django.shortcuts import render
from django.utils import timezone

from .models import Post


def post_list(request):
    # posts 변수에 ORM을 이용해서 전체 Post의 리스트(쿼리셋)를 대입
    # posts = Post.objects.all()

    # posts 변수에 ORM을 사용해서 전달할 쿼리셋이
    # posts의 published_date가 timezone.now()보다
    # 작은 갓을 가질 때만 해당하도록 필터를 사용한다.
    posts =Post.objects.filter(
        published_date__lte = timezone.now()
    )
    context = {
        'title' : 'PostList from post_list view',
        'posts' : posts,
    }
    return render(request, 'blog/post_list.html', context = context)


```


