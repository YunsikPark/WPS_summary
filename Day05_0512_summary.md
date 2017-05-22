#Day5 - Summary
> 2017.05.12 FRI	
> **박윤식**

-

#[tumblebug 사이트](https://tumblbug.com/projects)
##html

```
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>tumblbug projects</title>
  <link rel="stylesheet" href="css/normalize.css">
  <link rel="stylesheet" href="css/base.css">
  <link rel="stylesheet" href="css/projects.css">
  <link rel="stylesheet" href="css/common.css">
</head>
<body>
  <div id="wrap">
    <div id="header">
      <nav class="top-nav">
        <ul class="top-nav-left-list">
          <li class="menu-logo"><a href="#"><img src="images/logo.png" alt="logo"></a></li>
          <li class="menu-item"><a href="#">프로젝트 둘러보기</a></li>
          <li class="menu-item"><a href="#">프로젝트 올리기</a></li>
          <li class="menu-item"><a href="#">도움말</a></li>
        </ul>
        <ul class="top-nav-right-list">
          <li class="menu-search">
            <img src="images/search.png" alt="search">
            <input type="text">
          </li>
          <li class="menu-item"><a href="#">로그인</a></li>
          <li class="menu-btn"><a href="#" class="btn btn-theme">가입하기</a></li>
        </ul>
      </nav>

    </div>

    <div class="container clearfix">
      <section class="container-section">
        <header>
          <h1>모두보기</h1>
        </header>
        <ul class="project-list">
          <li class="project-card">
            <img class="card-image" src="images/ogri.png" alt="">
            <div class="card-top">
              <p class="card-title">신비한 동물분양 : 오그리 &amp; 도그리 인형</p>
              <p class="card-owner">GEP의 프로젝트</p>
              <p class="card-description">사랑스러운 동물친구 오그리 도그리오의 특별한 일상</p>
            </div>
            <div class="card-bottom clearfix">
              <div class="card-bottom-section card-bottom-left">
                <p class="card-bottom-title">모인금액</p>
                <p class="card-bottom-content">120,299,509원
                  <span class="card-bottom-content-percent">1415%</span>
                </p>
              </div>
              <div class="card-bottom-section card-bottom-right">
                <p class="card-bottom-title">남은시간</p>
                <p class="card-bottom-content">17일</p>
              </div>
            </div>
          </li>

          <li class="project-card">
            <img class="card-image" src="images/ogri.png" alt="">
            <div class="card-top">
              <p class="card-title">신비한 동물분양 : 오그리 &amp; 도그리 인형</p>
              <p class="card-owner">GEP의 프로젝트</p>
              <p class="card-description">사랑스러운 동물친구 오그리 도그리오의 특별한 일상</p>
            </div>
            <div class="card-bottom clearfix">
              <div class="card-bottom-section card-bottom-left">
                <p class="card-bottom-title">모인금액</p>
                <p class="card-bottom-content">120,299,509원
                  <span class="card-bottom-content-percent">1415%</span>
                </p>
              </div>
              <div class="card-bottom-section card-bottom-right">
                <p class="card-bottom-title">남은시간</p>
                <p class="card-bottom-content">17일</p>
              </div>
            </div>
          </li>

          <li class="project-card">
            <img class="card-image" src="images/ogri.png" alt="">
            <div class="card-top">
              <p class="card-title">신비한 동물분양 : 오그리 &amp; 도그리 인형</p>
              <p class="card-owner">GEP의 프로젝트</p>
              <p class="card-description">사랑스러운 동물친구 오그리 도그리오의 특별한 일상</p>
            </div>
            <div class="card-bottom clearfix">
              <div class="card-bottom-section card-bottom-left">
                <p class="card-bottom-title">모인금액</p>
                <p class="card-bottom-content">120,299,509원
                  <span class="card-bottom-content-percent">1415%</span>
                </p>
              </div>
              <div class="card-bottom-section card-bottom-right">
                <p class="card-bottom-title">남은시간</p>
                <p class="card-bottom-content">17일</p>
              </div>
            </div>
          </li>

          <li class="project-card">
            <img class="card-image" src="images/ogri.png" alt="">
            <div class="card-top">
              <p class="card-title">신비한 동물분양 : 오그리 &amp; 도그리 인형</p>
              <p class="card-owner">GEP의 프로젝트</p>
              <p class="card-description">사랑스러운 동물친구 오그리 도그리오의 특별한 일상</p>
            </div>
            <div class="card-bottom clearfix">
              <div class="card-bottom-section card-bottom-left">
                <p class="card-bottom-title">모인금액</p>
                <p class="card-bottom-content">120,299,509원
                  <span class="card-bottom-content-percent">1415%</span>
                </p>
              </div>
              <div class="card-bottom-section card-bottom-right">
                <p class="card-bottom-title">남은시간</p>
                <p class="card-bottom-content">17일</p>
              </div>
            </div>
          </li>

          <li class="project-card">
            <img class="card-image" src="images/ogri.png" alt="">
            <div class="card-top">
              <p class="card-title">신비한 동물분양 : 오그리 &amp; 도그리 인형</p>
              <p class="card-owner">GEP의 프로젝트</p>
              <p class="card-description">사랑스러운 동물친구 오그리 도그리오의 특별한 일상</p>
            </div>
            <div class="card-bottom clearfix">
              <div class="card-bottom-section card-bottom-left">
                <p class="card-bottom-title">모인금액</p>
                <p class="card-bottom-content">120,299,509원
                  <span class="card-bottom-content-percent">1415%</span>
                </p>
              </div>
              <div class="card-bottom-section card-bottom-right">
                <p class="card-bottom-title">남은시간</p>
                <p class="card-bottom-content">17일</p>
              </div>
            </div>
          </li>

          <li class="project-card">
            <img class="card-image" src="images/ogri.png" alt="">
            <div class="card-top">
              <p class="card-title">신비한 동물분양 : 오그리 &amp; 도그리 인형</p>
              <p class="card-owner">GEP의 프로젝트</p>
              <p class="card-description">사랑스러운 동물친구 오그리 도그리오의 특별한 일상</p>
            </div>
            <div class="card-bottom clearfix">
              <div class="card-bottom-section card-bottom-left">
                <p class="card-bottom-title">모인금액</p>
                <p class="card-bottom-content">120,299,509원
                  <span class="card-bottom-content-percent">1415%</span>
                </p>
              </div>
              <div class="card-bottom-section card-bottom-right">
                <p class="card-bottom-title">남은시간</p>
                <p class="card-bottom-content">17일</p>
              </div>
            </div>
          </li>

          <li class="project-card">
            <img class="card-image" src="images/ogri.png" alt="">
            <div class="card-top">
              <p class="card-title">신비한 동물분양 : 오그리 &amp; 도그리 인형</p>
              <p class="card-owner">GEP의 프로젝트</p>
              <p class="card-description">사랑스러운 동물친구 오그리 도그리오의 특별한 일상</p>
            </div>
            <div class="card-bottom clearfix">
              <div class="card-bottom-section card-bottom-left">
                <p class="card-bottom-title">모인금액</p>
                <p class="card-bottom-content">120,299,509원
                  <span class="card-bottom-content-percent">1415%</span>
                </p>
              </div>
              <div class="card-bottom-section card-bottom-right">
                <p class="card-bottom-title">남은시간</p>
                <p class="card-bottom-content">17일</p>
              </div>
            </div>
          </li>

        </ul>
      </section>
      <aside class="container-aside">
        <h3><img class="mark" src="images/mark.png" alt="">분야별 프로젝트</h3>
      </aside>
    </div>
    <footer></footer>
  </div>

</body>
</html>


```

##SCSS
###_variables.scss
```
$color-text-a: #868686;
$color-text-h: #645353;
$color-text-common: #676363;
$color-bg-common: #ebeae5;

$color-theme: #fa6b69;


```

###projects.scss
```
@import 'variables';
$top-nav-height: 60px;

nav.top-nav {
  background-color: white;
  height: $top-nav-height;
  padding: 0 32px;

  ul{
    height:$top-nav-height;
    &.top-nav-left-list{
      float: left;
    }

    &.top-nav-right-list{
      float: right;
    }

    li{
      height: $top-nav-height;
      line-height: $top-nav-height;
      float: left;
      &.menu-logo, &.menu-search{
        img {
          vertical-align: middle;
        }
      }
      &.menu-logo {
        margin: 0 20px 0 0;
      }
      &.menu-search {
        margin: 0 10px 0 0;
        transition: 1s;
        input {
          display: none;
          width: 0;
        }
        &:hover {
          input {
            display: inline-block;
            width: 100px;
          }
        }
      }
      &.menu-item {
        a {
          display: inline-block;
          height: $top-nav-height;
          padding: 0 10px;
          box-sizing: border-box;
          transition: 120ms;
          img {
            vertical-align: middle;
          }
          &:hover {
            color: $color-theme;
            border-bottom: 5px solid $color-theme;
          }
        }
      }
      &.menu-btn {
        margin: 0 0 0 10px;
        a:hover {
          background-color:red;
        }
      }
    }
  }
}

.container {
  width: 960px;
  margin: 0 auto;
  padding-top: 39px;
  padding-bottom: 78px;

  section.container-section {
    float: left;
    width: 720px;
    background-color: $color-bg-common/*rgba(255, 0, 0, 0.3)*/;

    header {
      margin: 0 10px;
    }
  }
  aside.container-aside {
    float: left;
    margin-left: 20px;
    width: 220px;
    // background-color: rgba(0, 255, 0, 0.3);
    > h3{
      .mark {
        margin: 0 5px;
        vertical-align: middle;
      }
    }
  }
  section.container-section ul.project-list {

    li.project-card {
      float: left;
      width: 220px;
      margin: 0 10px 26px;
      // height: 50px;
      background-color: #fff;
      border: 1px solid #dcdcdc;
      border-radius: 4px;
      box-sizing: border-box;

      p {margin: 0;}

      img.card-image {
        max-width: 100%;
        border-radius: 3px 3px 0 0;
      }
      .card-top {
        height: 139px;
        padding: 13px 19px 0;
        border-bottom: 3px solid $color-theme;

        .card-title {
          font-size: 14px;
          color: $color-text-h;
          line-height: 1.375;
        }
        .card-owner {
          font-size: 12.56px;
          color: #433;
          margin: 3px 0 0;
        }
        .card-description {
          font-size: 12.56px;
          margin: 8px 0 0;
          line-height: 1.685;
        }
      }
      .card-bottom{
        padding: 13px 19px;
        .card-bottom-section {
          float: left;
          font-size: 12px;

          p.card-bottom-title {
            margin-bottom: 0.5em;
          }
          p.card-bottom-content {
            color: $color-text-h;
            font-weight: 500;

            .card-bottom-content-percent {
              color: $color-theme;
              margin-left: 5px;
            }
          }
        }

        .card-bottom-left {
          width:70%;
        }
        .card-bottom-right {
          width: 30%;
        }
      }
    }
  }
}
```


###base.scss
```
@import 'variables';
html {

}
body {
  background-color: $color-bg-common;
  color: $color-text-common;
}
ul, ol{
  list-style-type: none;
  margin: 0;
  padding: 0;
}
a {
  text-decoration: none;
  color: $color-text-a;
}
h1, h2, h3, h4, h5, h6 {
  color: $color-text-h;
}


```

###common.scss

```
@import 'variables';
.clearfix::after {
  content: '';
  display: block;
  clear: both;
}

.btn {
  box-sizing: border-box;
  border: 2px solid $color-text-common;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  text-align: center;
  text-decoration: none;
  padding: 5px 17px;
}

.btn-theme {
  border-color: $color-theme;
  color: $color-theme;
}

// @media screen ()  `XA2QQQ;''`


```

