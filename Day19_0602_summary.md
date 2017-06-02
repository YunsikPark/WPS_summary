## 주의 사항 about Debug
>퍼블리싱할 때에는 settings.py의 DEBUG=True 기본값으로 되어있는데 이를 False로 바꾸거나 지워줘야한다 그렇지 않으면 모든 오류메시지가 공개되어 외부로부터 치명적인 공격을 받을 수 있다.

## Pycharm Keymap settings
* 같은 내용의 태그 선택하기

 : keymap search에서 add selection for next occurence 
 기본 ctrol + G 설정되어 있음
atom이랑 같이하려면 command + D
 이렇게하려면 code 비교하는 단축키도 바꿔야함

 
* 태그 포함시키기

 : keymap search에서 surround with emmet
atom이랑 똑같이 단축키 control + W
 
 
## 디버그 창 만들기
 
1. 관련된 태그라인의 왼쪽을 클릭한 후 
2. 오른쪽위 화살표를 누른 후 
3. 왼쪽위의 + 를 클릭하여 python을 선택
4. unnamed 를 Django runserver를 타입 후
5. 오른쪽 script에 해당 프로젝트의 manage.py를 선택 
6. script parameter에 runserver를 타입 
7. 브라우저 실행하여 관련태그 실행을 하면 단계별로 디버그를 확인



# *런칭할 때 staticfiles는 다른 서버에 있어야 함.*


## 장고 admin base.html 위치

>**External Libraries > site-packages > contrib > admin > template**




## 오늘의 Git

####이미 등록된 태그 삭제하기

* commit만 되어 있는 경우
`git tag -d part5`

* push까지 되어 있는 경우`git push origin :refs/tags/part5`