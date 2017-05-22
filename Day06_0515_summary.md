#Vim
-
####Vim		:	[wikipedia](https://ko.wikipedia.org/wiki/Vim)

###설치
```
brew install vim
```


###vim 실습

>`mkdir git-practice`
>
>`vim test.txt`



###vim config 설정
`vi ~/.vimrc`

```
synteax on
set tabstop=4
set expandtab
set softtabstop=4
set shiftwidth=4
set number
filetype indent on
```


###VIM 단축키

####삽입

키|기능
---|---
i|커서 위치에 Insert
I|줄 맨 앞에서 Insert
a|커서 다음에 Insert
A|줄 맨 뒤에서 Insert
o|커서 아래로 한 줄 띄우고 Insert
O|커서 위로 한 줄 띄우고 Insert


####이동

키|기능
---|---
w|단어 첫 글자 기준으로 다음으로 이동
W|공백 기준으로 다음(단어의 시작)으로 이동
b|단어 첫 글자 기준으로 이전으로 이동
B|공백 기준으로 이전으로 이동
e|단어 마지막 글자 기준으로 다음으로 이동
E|공백 기준으로 다음(단어의 끝)으로 이동
gg|문서 맨 앞으로 이동
G|문서 맨 아래로 이동
^|문장 맨 앞으로 이동
$|문장 맨 뒤로 이동



####검색

키|기능
---|---
/+`word`|해당 word를 검색, 'n'과 'N'으로 다음 / 이전 찾기

####편집

키|기능
---|---
dd|현재 줄 잘라내기
yy|현재 줄 복사하기
p|붙여넣기
u|실행취소 (Undo)
ctrl + r|재실행 (Redo)
v|Visual모드
d|삭제
y|복사
c|잘라내기

####저장

키|기능
---|---

:w|저장
:q|닫기
:q!|저장하지 않고 닫기
:wq|저장하고 닫기
:숫자|지정한 줄 번호로 이동


---

# git
-

###Git Book [git 사용법](https://git-scm.com/book/ko/v2/)

####git 최신버전 관리

>버전체크

```
git --version
```

>최신버전으로 업그레이드
```
brew install git
```


####Git 최초설정
#####사용자정보 입력
```
git config --global user.name "Yunsik Park"
git config --global user.email space214@gmail.com
```
#####편집기
```
git config --global core.editor vim
```
*git 홈페이지에 나와있는 book에는 emacs라는 편집기로 나와있는데 이 편집기는 쓰지 않는다.*

>git confit 설정 option 들을 볼 수 있다.
```
git config --list
```

<br>
>git help
>
```
git help [a, clone등의 도움말을 볼 수 있다.]
```


###zsh설치
```
brew install zsh zsh-completions
curl -L http://install.ohmyz.sh | sh
```

>확인법
>echo $SHELL

---


####zsh설정하기
기존에 zsh를 설정한 적이 없다면 다음과 같이 config를 로드해서 설정을 변경할 수 있다.


```
vim ~/.zshrc

```

####폴더 생성과 동시에 생성된 폴더의 경로로 바로 이동
```
take [폴더]
```


###자주사용하는 명령어 별칭 (alias)지정하기

####필수적으로 추가되어야 할 부분

```
export PYENV_ROOT=/usr/local/var/pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```


####alias
```
alias <사용할 명령어>="<명령어 내용>"

# Pycharm 실행
alias py ="open -a /Applications/PyCharm.app/Contents/MacOS/pycharm"
```

마지막줄에 다음을 입력

```
alias py="open -a /Applications/Pycharm\ CE.app/Contents/MacOS/pycharm"
alias md="open -a /Applications/MacDown.app/Contents/MacOS/MacDown"
alias atom="open -a /Applications/Atom.app/Contents/MacOS/atom"
```



```
alias mkd='function _mkd(){ mkdir -p -- "$1" && cd -P -- "$1" };_mkd'
```



###git 시작하기
>깃을 시작하기 위해 알림
>깃을 사용하기 위한 저장소를 만들어 주는 명령
>이 폴더는 깃으로 작업하겠다는 뜻
**```
git init
```**

####폴더 확인

```
ls -al
ls
l
```

####readme.md 파일 생성
```
touch README.md
```

####MacDown으로 실행
```
md README.md
```

####vim을 이용하여 내용 입력
```
vim readme.txt
```

####git 파일 올리기

```
git add READMD.md
git commit
```

**이때 vim이 실행되는데 가장 첫번째 줄에 comment를 꼭 작성해줘야 한다! 그렇지 않으면 업로드 되지 않음**

>comment작성후 저장하고 나와서 다음을 실행하여 확인한다.
>commit 된 내용을 보기 위한 명령어
>
```
git log
```

####커밋 한번에 하기

```
git add abc4.txt
git commit -m 'add abc4.txt'
```



####git 상태확인
>현재 Working 내용 상태확인
```
git status
```

###git삭제
>git설정을 실수 할 경우
>
```
rm -rf .git
```


**git파일을 생성하면 untracted file로 생성되는데
이를 깃 관리를 하기 위해서는 git add로 추가를해준다
그리고 나서 commit을 시켜줘야하는데 이를 하지 않으면 단순히 new파일만 인식하게 되므로 commit을 반드시 해준다.**

###모든파일을 git에 추가하기

```
git add --all
git add -A
```

>stage 영역에서 어떤 내용이 변경 되었는지 확인하는 법
```
git diff --staged
```

<br>
>modified 영역에서 어떤 내용이 변경 되었는지 확인하는 법
>
```
git diff
```


>내용 출력만 하기
>
```
echo lorem asdfeon asij ef
```



>파일을 생성하면서 내용 넣기
>
```
echo 'show me the money' > abc4.txt. 
```


>cat: 내용 출력해주기
>
```
cat abc4.txt
```



###파일 무시하기

`.gitignore`파일만들어 설정한다
>*.swp 파일 무시하기

```
vi .gitignore

*.swp
```



---

###[Staged와 Unstaged 상태의 변경 내용을 보기](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%88%98%EC%A0%95%ED%95%98%EA%B3%A0-%EC%A0%80%EC%9E%A5%EC%86%8C%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%98%EA%B8%B0)
단순히 파일이 변경됐다는 사실이 아니라 어떤 내용이 변경됐는지 살펴보려면 `git status` 명령이 아니라 `git diff` 명령을 사용해야 한다. 보통 우리는 '수정했지만, 아직 Staged 파일이 아닌 것?'과 '어떤 파일이 Staged 상태인지?'가 궁금하기 때문에 `git status` 명령으로도 충분하다. 더 자세하게 볼 때는 `git diff` 명령을 사용하는데 Patch처럼 어떤 라인을 추가했고 삭제했는지가 궁금할 때 사용한다. `git diff`는 나중에 더 자세히 다룬다.

`README` 파일을 수정해서 Staged 상태로 만들고 `CONTRIBUTING.md` 파일은 그냥 수정만 해둔다. 이 상태에서 `git status` 명령을 실행하면 아래와 같은 메시지를 볼 수 있다.

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```


`git diff`명령을 실행하면 수정했지만 아직 staged 상태가 아닌 파일을 비교해 볼 수 있다.

```
$ git diff
diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
index 8ebb991..643e24f 100644
--- a/CONTRIBUTING.md
+++ b/CONTRIBUTING.md
@@ -65,7 +65,8 @@ branch directly, things can get messy.
 Please include a nice description of your changes when you submit your PR;
 if we have to read the whole diff to figure out why you're contributing
 in the first place, you're less likely to get feedback and have your change
-merged in.
+merged in. Also, split your changes into comprehensive chunks if your patch is
+longer than a dozen lines.

 If you are starting to work on a particular area, feel free to submit a PR
 that highlights your work in progress (and note in the PR title that it's
```
이 명령은 워킹 디렉토리에 있는 것과 Staging Area에 있는 것을 비교한다. 그래서 수정하고 아직 Stage 하지 않은 것을 보여준다.

만약 커밋하려고 Staging Area에 넣은 파일의 변경 부분을 보고 싶으면 git diff --staged 옵션을 사용한다. 이 명령은 저장소에 커밋한 것과 Staging Area에 있는 것을 비교한다.

```
$ git diff --staged
diff --git a/README b/README
new file mode 100644
index 0000000..03902a1
--- /dev/null
+++ b/README
@@ -0,0 +1,4 @@
+My Project
```


꼭 잊지 말아야 할 것이 있는데 git diff 명령은 마지막으로 커밋한 후에 수정한 것들 전부를 보여주지 않는다. git diff`는 Unstaged 상태인 것들만 보여준다. 이 부분이 조금 헷갈릴 수 있다. 수정한 파일을 모두 Staging Area에 넣었다면 `git diff 명령은 아무것도 출력하지 않는다.

CONTRIBUTING.md 파일을 Stage 한 후에 다시 수정해도 git diff 명령을 사용할 수 있다. 이때는 Staged 상태인 것과 Unstaged 상태인 것을 비교한다.


```

```

git diff 명령으로 Unstaged 상태인 변경 부분을 확인할 수 있다.

```

```

Staged 상태인 파일은 git diff --cached 옵션으로 확인한다. --staged 와 --cached 는 같은 옵션이다.

```

```

-
####변경사항 커밋하기
```
$ git commit
```

####Staging Area 생략하기
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md

no changes added to commit (use "git add" and/or "git commit -a")
$ git commit -a -m 'added new benchmarks'
[master 83e38c7] added new benchmarks
 1 file changed, 5 insertions(+), 0 deletions(-)
```

####파일 삭제하기
Git에서 파일을 제거하려면 git rm 명령으로 Tracked 상태의 파일을 삭제한 후에(정확하게는 Staging Area에서 삭제하는 것) 커밋해야 한다. 이 명령은 워킹 디렉토리에 있는 파일도 삭제하기 때문에 실제로 파일도 지워진다.

Git 명령을 사용하지 않고 단순히 워킹 디렉터리에서 파일을 삭제하고 git status 명령으로 상태를 확인하면 Git은 현재 "Changes not staged for commit"(즉, Unstaged 상태)라고 표시해준다.

```
$ rm grit.gemspec
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    deleted:    grit.gemspec

no changes added to commit (use "git add" and/or "git commit -a")
```

그리고 **`git rm`** 명령을 실행하면 삭제한 파일은 Staged 상태가 된다.

```
$ git rm grit.gemspec
rm 'grit.gemspec'
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    deleted:    grit.gemspec
```


####파일 이름 변경하기

Git은 다른 VCS 시스템과는 달리 파일 이름의 변경이나 파일의 이동을 명시적으로 관리하지 않는다. 다시 말해서 파일 이름이 변경됐다는 별도의 정보를 저장하지 않는다. Git은 똑똑해서 굳이 파일 이름이 변경되었다는 것을 추적하지 않아도 아는 방법이 있다. 파일의 이름이 변경된 것을 Git이 어떻게 알아내는지 살펴보자.

이렇게 말하고 Git에 `mv` 명령이 있는 게 좀 이상하겠지만, 아래와 같이 파일이름을 변경할 수 있다.

```
$ git mv file_from file_to
```


---



Link걸기
>나중에 다시 수업진행

```
ln -s 원본 만들링크

ln -s ~/Dropbox/zsh/.zshrc ~/.zshrc
```

```
git --git-dir ~/Dropbox/zsh/.git log
git --git-dir ~/Dropbox/zsh/.git add -A && git -git-dir ~/Dropbox.zsh/.git commit $1 && git --git-dir ~/............
```


---

#커밋 히스토리 조회하기

###커밋 히스토리 조회하기

새로 저장소를 만들어서 몇 번 커밋을 했을 수도 있고, 커밋 히스토리가 있는 저장소를 Clone 했을 수도 있다. 어쨌든 가끔 저장소의 히스토리를 보고 싶을 때가 있다. Git에는 히스토리를 조회하는 명령어인 `git log`가 있다.

이 예제에서는 “simplegit” 이라는 매우 단순한 프로젝트를 사용한다. 아래와 같이 이 프로젝트를 Clone 한다.

```
$ git clone https://github.com/schacon/simplegit-progit

```

이 프로젝트 디렉토리에서 git log 명령을 실행하면 아래와 같이 출력된다.

```
$ git log
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    removed unnecessary test

commit a11bef06a3f659402fe7563abf99ad00de2209e6
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 10:31:28 2008 -0700

    first commit
    
```

특별한 아규먼트 없이 git log 명령을 실행하면 저장소의 커밋 히스토리를 시간순으로 보여준다. 즉, 가장 최근의 커밋이 가장 먼저 나온다. 그리고 이어서 각 커밋의 SHA-1 체크섬, 저자 이름, 저자 이메일, 커밋한 날짜, 커밋 메시지를 보여준다.

원하는 히스토리를 검색할 수 있도록 git log 명령은 매우 다양한 옵션을 지원한다. 여기에서는 자주 사용하는 옵션을 설명한다.

여러 옵션 중 `-p`는 굉장히 유용한 옵션이다. `-p`는 각 커밋의 diff 결과를 보여준다. 다른 유용한 옵션으로 `-2`가 있는데 최근 두 개의 결과만 보여주는 옵션이다:

```
$ git log -p -2
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number

diff --git a/Rakefile b/Rakefile
index a874b73..8f94139 100644
--- a/Rakefile
+++ b/Rakefile
@@ -5,7 +5,7 @@ require 'rake/gempackagetask'
 spec = Gem::Specification.new do |s|
     s.platform  =   Gem::Platform::RUBY
     s.name      =   "simplegit"
-    s.version   =   "0.1.0"
+    s.version   =   "0.1.1"
     s.author    =   "Scott Chacon"
     s.email     =   "schacon@gee-mail.com"
     s.summary   =   "A simple gem for using Git in Ruby code."

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    removed unnecessary test

diff --git a/lib/simplegit.rb b/lib/simplegit.rb
index a0a60ae..47c6340 100644
--- a/lib/simplegit.rb
+++ b/lib/simplegit.rb
@@ -18,8 +18,3 @@ class SimpleGit
     end

 end
-
-if $0 == __FILE__
-  git = SimpleGit.new
-  puts git.show
-end
\ No newline at end of file

```

이 옵션은 직접 diff를 실행한 것과 같은 결과를 출력하기 때문에 동료가 무엇을 커밋했는지 리뷰하고 빨리 조회하는데 유용하다. 또 git log 명령에는 히스토리의 통계를 보여주는 옵션도 있다. --stat 옵션으로 각 커밋의 통계 정보를 조회할 수 있다.

```
$ git log --stat
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number

 Rakefile | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    removed unnecessary test

 lib/simplegit.rb | 5 -----
 1 file changed, 5 deletions(-)

commit a11bef06a3f659402fe7563abf99ad00de2209e6
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 10:31:28 2008 -0700

    first commit

 README           |  6 ++++++
 Rakefile         | 23 +++++++++++++++++++++++
 lib/simplegit.rb | 25 +++++++++++++++++++++++++
 3 files changed, 54 insertions(+)
```



