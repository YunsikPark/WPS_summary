# WSGI
>웹 서버 게이트웨이 인터페이스 [wiki](https://ko.wikipedia.org/wiki/%EC%9B%B9_%EC%84%9C%EB%B2%84_%EA%B2%8C%EC%9D%B4%ED%8A%B8%EC%9B%A8%EC%9D%B4_%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4)


* 웹 서버 게이트웨이 인터페이스(WSGI, Web Server Gateway Interface)는 웹서버와 웹 애플리케이션의 인터페이스를 위한 파이선 프레임워크다.

## 개요

 기존의 파이선 웹 애플리케이션 프레임워크는 웹서버를 선택하는데 있어서 제약이 있었다. 보통 CGI, FastCGI, mod_python 과 같은 커스텀API 중에 하나만 사용할 수 있도록 디자인 되었는데, WSGI는 그에 반하여 low-level로 만들어져서 웹서버와 웹 애플리케이션,프레임워크간의 벽을 허물었다.


## 구체적인 사항

WSGI는 서버와 게이트웨이 , 애플리케이션과 프레임워크 양단으로 나눠져있다. WSGI 리퀘스트를 처리하려면, 서버단에서 환경정보와 콜백함수를 애플리케이션단에 제공해야한다. 애플리케이션은 그 요청을 처리하고 미리 제공된 콜백함수를 통해 서버단에 응답한다. WSGI 미들웨어(라고 불린다.)가 WSGI 서버와 애플리케이션 사이를 보충해주는데, 이 미들웨어는 서버의 관점에서는 애플리케이션으로, 애플리케이션의 관점에서는 서버로 행동한다. 이 미들웨어는 다음과 같은 기능을 가진다.

* 환경변수가 바뀌면 타겟 URL에 따라서 리퀘스트의 경로를 지정해준다.
* 같은 프로세스에서 여러 애플리케이션과 프레임워크가 실행되게 한다.
* XSLT 스타일시트를 적용하는 것과 같이 전처리를 한다.

# Django

## requirements.txt

```
>>> pip freeze > requirements.txt
```

## Django migrations

* migrations 보기 
* 	* `./manage.py showmigrations`

* migration 되돌리기 
* 	* `./manage.py migrate polls 0001_initial`


* 필요없는 migration 지우기
* 	* `rm polls/migrations/002_auto_blablablabla..`


## QuerySet 수정
```
>>> from polls.models import Question, Choice
>>> Question.objects.all()
<QuerySet [<Question: What's up?>, <Question: What's your favorite game?>]>
>>> Question.objects.exclude(id=1).delete()
(1, {'polls.Choice': 0, 'polls.Question': 1})
>>> Question.objects.all()
<QuerySet [<Question: What's up?>]>
>>> 
```

## 오늘의 Git

> 커밋 메시지 수정

커밋하고 난 후 새로 만든 파일이나 수정한 파일을 가장 최근 커밋에 넣기위해서는 수정 또는 생성된 파일을 먼저  `git add <file name>`으로 추가 한 후 커밋을 다음 명령을 통해 이전 커밋내용에 포함 시킨다. **`git commit --amend`**

> Git TAG

프로젝트 진행 중 단위별 또는 버전별로 선언하기 위해 `git tag`명령을 이용하는데 다음과 같이 수행한다.

* git tag 지정하기

**```git tag -a <part1 또는 v1.0> -m '<DjangoTutorial Part1 등의 메시지>'```**


* git tag 푸쉬하기

**```git push origin <part1 또는 v1.0> ```**


