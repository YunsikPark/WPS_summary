## atom scss

```
>>> brew upgrade node
```
이후 scss 오류시 다음을 실행한다.

```
>>> sudo chown -R $USER:$(id -gn $USER) /Users/archys/.config
```

그래도 안되면

```
>>> sudo chown -R $USER /usr/local
```

그리고 나서

```
>>> npm install node-sass -g
```

실행

