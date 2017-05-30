Bootstrap을 django_app 하위에 static폴더를 만들어 bootstra폴더채로 넣는다.

>특정경로로 이동하기 위해서는 urls.py, settings.py에서 url의 설정을 변경해 줘야한다.


`settings.py`

```

# Build paths inside the project like this: os.path.join(BASE_DIR, ...)
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
print('BASE_DIR:', BASE_DIR)
# os.path.join을 사용해서 TEMPLATE_DIR변수에 django_app/templates폴더의 경로를 할당
TEMPLATE_DIR = os.path.join(BASE_DIR, 'templates')
print('TEMPLATE_DIR:', TEMPLATE_DIR)
# 위와 같은 방법으로 django_app/static폴더의 경로를 STATIC_DIR에 할당
STATIC_DIR = os.path.join(BASE_DIR, 'static')
print('STATIC_DIR:', STATIC_DIR)

...

# 이 경로로 시작하는 URL은 정적 파일들의 위치에서 파일을 찾아 리턴
STATIC_URL = '/static/'

# 이 리스트(또는 튜플)의 경로는 STATIC_URL로 요청된 파일을 찾는 폴더로 사용됨
STATICFILES_DIRS = {
    STATIC_DIR,
}
```

#### 내용 요약해서 보이기

`post_list.html`

```
 <p>{{post.text|truncatechars:150}}</p>
```



####해당 블로그 포스트 불러오기

#### `urls.py`

```
urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^$', views.post_list),
    # o /post/<pk>/
    # o /post/1/
    # o /post/42/
    # o /post/234/
    # x /post/234/asdf/
    # /post/ 로 시작하고 중간에 숫자개 이사을 가지고 /로 끝나는 정규표현식을 작성
    # url(r'^post/\d+/$', views.post_detail,)
    # views.post_detail(pk=<num>)
    url(r'^post/(?P<pk>\d+)/$', views.post_detail, )
]
```

`templates/blog/`폴더에 `post_detail.html` 생성
`post_list.html`의 내용을 `post_detail.html`에 붙여넣기한 다음 for 문을 삭제한다.

#### `post_detail.html`

```
{% load staticfiles %}
<!doctype html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Django Girls blog</title>
    <link rel="stylesheet" href="{% static 'bootstrap/css/bootstrap.css' %}">
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
  <div class="container">
      <div class="header">
        <div>
          <h1><a href="#">Django Girls Blog</a></h1>
          <h4>{{title}}</h4>
        </div>
      </div>

    <div>
        <div class="post-list">
          <div class="post">
              <h4><a href="">{{post.title}}</a></h4>
              <p class="text-right">published: {{post.published_date}}</p>
              <p>{{post.text}}</p>
          </div>
        </div>
    </div>
  </div>
</body>
</html>

```

#### `views.py`

```

def post_detail(request, pk):
    print('post_detail pk:', pk)
    # post라는 키값으로 pk또는 id값이 매개변수로 주어진 pk변수와 같은 Post객체를 전달
    # objects.get을 쓰세요
    context = {
        'post': Post.objects.get(pk=pk)
    }
    return render(request, 'blog/post_detail.html', context = context)
    
```

detail.html
base.html
post_list.html
연결

detail.html

```
{% extends 'blog/base.html' %}

{% block content %}
<div class="post-list">
  <div class="post">
      <h4><a href="">{{post.title}}</a></h4>
      <p class="text-right">published: {{post.published_date}}</p>
      <p>{{post.text}}</p>
  </div>
</div>
{% endblock %}

```

base.html

```
{% load staticfiles %}
<!doctype html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Django Girls blog</title>
    <link rel="stylesheet" href="{% static 'bootstrap/css/bootstrap.css' %}">
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
  <div class="container">
      <div class="header">
        <div>
          <h1><a href="#">Django Girls Blog</a></h1>
          <h4>{{title}}</h4>
        </div>
      </div>
      {% block content %}
      {% endblock %}
  </div>
</body>
</html>

```


post_list.html

```
{% extends 'blog/base.html' %}

{% block content %}
<div class="post-list">
  {% for post in posts %}
  <div class="post">
      <h4><a href="/post/{{post.pk}}/">{{post.title}}</a></h4>
      <p class="text-right"><small>published: {{post.published_date}}</small></p>
      <p>{{post.text|truncatechars:150}}</p>
  </div>
  {% endfor %}
</div>
{% endblock %}

```

#### urls.py의 주소가 바뀌더라도 html값의 변경없이 주소만 바뀌게되는 함수

##### `urls.py`

```
...

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^$', views.post_list, name='post_list'),
    # o /post/<pk>/
    # o /post/1/
    # o /post/42/
    # o /post/234/
    # x /post/234/asdf/
    # /post/ 로 시작하고 중간에 숫자개 이사을 가지고 /로 끝나는 정규표현식을 작성
    # url(r'^post/\d+/$', views.post_detail,)
    # views.post_detail(pk=<num>)
    url(r'^post/(?P<pk>\d+)/$', views.post_detail, name='post_detail'),
]

...
```

##### `views.py`

```
...

def post_detail(request, pk):
    print('post_detail pk:', pk)
    # post라는 키값으로 pk또는 id값이 매개변수로 주어진 pk변수와 같은 Post객체를 전달
    # objects.get을 쓰세요
    context = {
        'post': Post.objects.get(pk=pk)
    }
    # with open('templates/blog/post_detail.html') as opentemplate:
    #     f = opentemplate.read()
    # return HttpResponse(f)
    return render(request, 'blog/post_detail.html', context = context)
    
...

```

##### `post_list.html`

```
...

<h4><a href="{% url 'post_detail' pk=post.pk %}">{{post.title}}</a></h4>

...

```
---

###[URL Dispatcher](https://docs.djangoproject.com/en/1.11/topics/http/urls/)


## post_create()
### POST Method 작성







`views.py`

```

from django.http import HttpResponse
from django.shortcuts import render, redirect
from django.utils import timezone
from django.contrib.auth import get_user_model
User = get_user_model()
from .models import Post



...


def post_list(request):
    # post 정렬하기
    posts = Post.objects.order_by('-created_date')
    
    
    ...
    


def post_create(request):
    if request.method == 'GET':
        context = {

    }
        return render(request, 'blog/post_create.html',context)
    elif request.method == 'POST':
        data = request.POST
        title = data['title']
        text = data['text']
        user = User.objects.first()
        # create 메소드를 쓰는 순간 DB에 저장된다
        post = Post.objects.create(
            author=user,
            title = title,
            text = text
        )
        # return HttpResponse(post)
        return redirect('post_detail', pk=post.pk)
        
...

```


`post_create.html`

```
<!-- blog/base.html을 확장하여
제목 (input type text)
내용 (textarea)
작성버튼 (button)
을 갖는 html을 작성 -->

{% extends 'blog/base.html' %}

{% block content %}

<div class="post-create">
  <form action="" method="post">
    {% csrf_token %}
    <input type="text" name="title" value="">
    <textarea name="text" rows="8" cols="80"></textarea>
    <button type = "submit">작성</button>
  </form>

</div>
{% endblock %}


```

### 

`forms.py`

```
from django import forms

class PostCreateForm(forms.Form):
    title = forms.CharField(
        label = '제목',
        max_length =10,
        required = True,
        widget = forms.TextInput(
            attrs = {
                'class':'form-control'
            }
        )
    )
    text = forms.CharField(
        label = '내용',
        widget=forms.Textarea(
            attrs = {
                'class':'form-control'
            }
        ),
        required=True
    )

```


`views.py`

```
from django.http import HttpResponse
from django.shortcuts import render, redirect
from django.utils import timezone
from django.contrib.auth import get_user_model
User = get_user_model()
from .models import Post

from .forms import PostCreateForm

def post_list(request):
    # posts 변수에 ORM을 이용해서 전 Post의 리스트(쿼리셋)를 대입
    #post 정렬하기
    posts = Post.objects.order_by('-created_date')

    # posts 변수에 ORM을 사용해서 전달할 쿼리셋이
    # posts의 published_date가 timezone.now()보다
    # 작은 갓을 가질 때만 해당하도록 필터를 사용한다.
    # posts =Post.objects.filter(
    #     published_date__lte = timezone.now()
    # )
    context = {
        'title' : 'PostList from post_list view',
        'posts' : posts,
    }
    return render(request, 'blog/post_list.html', context = context)

def post_detail(request, pk):
    print('post_detail pk:', pk)
    # post라는 키값으로 pk또는 id값이 매개변수로 주어진 pk변수와 같은 Post객체를 전달
    # objects.get을 쓰세요
    context = {
        'post': Post.objects.get(pk=pk)
    }
    # with open('templates/blog/post_detail.html') as opentemplate:
    #     f = opentemplate.read()
    # return HttpResponse(f)
    return render(request, 'blog/post_detail.html', context = context)

def post_create(request):
    if request.method == 'GET':
        form = PostCreateForm()
        context = {
            'form':form,
        }
        return render(request, 'blog/post_create.html',context)
    elif request.method == 'POST':
        # Form클래스의 생성자에 POST데이터를 전달하여 Form 인스턴스를 생성
        form = PostCreateForm(request.POST)
        # Form인스턴스의 유효성을 검사하는 is_valid메서드
        if form.is_valid():
            title = form.cleaned_data['title']
            text = form.cleaned_data['text']
            user = User.objects.first()
            post = Post.objects.create(
                author=user,
                title = title,
                text = text
            )
            # return HttpResponse(post)
            return redirect('post_detail', pk=post.pk)

        else:
            context = {
                'form':form,
            }
            return render(request, 'blog/post_create.html', context)


```




### 수정 템플릿

`forms`

```
from django import forms

class PostCreateForm(forms.Form):
    title = forms.CharField(
        label = '제목',
        max_length =10,
        required = True,
        widget = forms.TextInput(
            attrs = {
                'class':'form-control'
            }
        )
    )
    text = forms.CharField(
        label = '내용',
        widget=forms.Textarea(
            attrs = {
                'class':'form-control'
            }
        ),
        required=True
    )

```

`views.py`

```
...


def post_modify(request, pk):
    post = Post.objects.get(pk = pk)
    if request.method == 'POST':
        # POST요청(request)가 올 경우, 전달받은 데이터의 title, text값을 사용해서
        # 해당하는 Post 인스턴스 (post)의 title, text속성값에 더ㅠ어씌우고
        # DB에 업데이트하는 save()메서드 실행
        data = request.POST
        # extra) 장고폼을 사용하는 형태로 업데이트
        title = data['title']
        text = data['text']
        post.title = title
        post.text = text
        post.save()
        # 기존 post인스턴스를 업데이트 한 후, 다시 글 상세화면으로 이동
        return redirect('post-detail', pk=post.pk)
    elif request.method == 'GET':
        # pk에 해당하는 Post인스턴스를 전달
        # extra) 장고폼을 'form'키로 전달해서 구현
        context = {
            'post': post,
        }
        return render(request, 'blog/post_modify.html', context)


...


```


`urls.py`

```

...

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^$', views.post_list, name='post_list'),
    # o /post/<pk>/
    # o /post/1/
    # o /post/42/
    # o /post/234/
    # x /post/234/asdf/
    # /post/ 로 시작하고 중간에 숫자개 이사을 가지고 /로 끝나는 정규표현식을 작성
    # url(r'^post/\d+/$', views.post_detail,)
    # views.post_detail(pk=<num>)
    url(r'^post/(?P<pk>\d+)/$', views.post_detail, name='post_detail'),
    url(r'^post/(?P<pk>\d+)/modify/$', views.post_modify, name='post_mdoify'),
    url(r'^post/create/$', views.post_create, name='post_create')
]


```

`modify.html`

```

{% extends 'blog/base.html' %}
{% block content %}
<a href="{% url 'post_list' %}" class="btn btn-primary pull-right">List</a>

<form action="/post/create/" method="post">
  {% csrf_token %}

  <input type="text" name="title" value="{{ post.title }}">
  <textarea name="text" id="" cols="30" rows="10">{{post.text}}</textarea>
  <button type="submit" class="btn btn-primary btn-block">수정</button>
</form>
</div>
{% endblock %}

```



