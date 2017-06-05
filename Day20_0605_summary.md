# models

## Django Documentation

* `pyenv virtualenv 3.6.1 django_documentation_env`
* 가상환경 삭제하기(`pyenv uninstall django_documentation_env`)
* `pyenv local django_documentation_env`
* `pip install django`
* `pip install `
* `django-admin startproject mysite`
* `mv mysite django_app`
* `cp ../django_tutorial/.gitignore .`django_tutorial폴더에 있는 .gitignore파일 복사
* `pip freeze > requirements.txt`
* `git init`
* `git remote add origin <깃 주소>`
* `git add -A`
* `git commit -m 'First commit'`
* `./manage.py startapp introduction_to_models`

`models.py`

```
from django.db import models

# Create your models here.
class Person(models.Model):
    SHIRT_SIZES = (
        ('S', 'Small'),
        ('M', 'Medium'),
        ('L', 'Large'),
    )
    name = models.CharField(max_length=60)
    shirt_size = models.CharField(max_length=1, choices=SHIRT_SIZES)
```

```
# INSTALLED_APPS에 이 모델이 속하는 app 추가
# makemigrations로 migrations생성
# migrate로 migration을 적용
# admin.py에 Person클래스 등록
# createsuperuser로 슈퍼유저 계정 생성
# runserver 후 admin접속해서 Person객체 생성 및 저장해보기
```

* `pip install django_extensions`
* INSTALLED\_APPS에 django_extensions 추가
* `./manage.py makemigrations`
* `./manage.py migrate`
* `pip install ipython`
* `./manage.py shell_plus`

>DB작성 by shell_plus on ipython

```
>> ManuFacturer.objects.create(name='BMW')
<ManuFacturer: BMW>

>> ManuFacturer.objects.create(name='Hyundai')
<ManuFacturer: Hyundai>

>> c = Car(name = '520d')
>> m = ManuFacturer.objects.get(name = 'BMW')
>> Car.objects.create(name='520d',manufacturer=m)
<Car: 520d>

>> c = Car.objects.get(id=1)
>> c
<Car: 520d>

>> c.manufacturer
<ManuFacturer: BMW>

>> type(c)
introduction_to_models.models.Car

>> type(c.manufacturer)
introduction_to_models.models.ManuFacturer



```



