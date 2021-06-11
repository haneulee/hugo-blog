---
title: "Pug로 HTML 템플릿 만들기 🐶"
date: 2021-05-31T13:11:16+09:00
categories: 
- development
- pug
tags: 
- development
- front-end
- pug
- html
- 템플릿
- 개발
- express
- template
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/pug/img-1.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---
<!--toc-->
![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/pug/img-1.png)

# Pug


## Pug 란 ?
- Pug는 Haml의 영향을 많이 받고 Node.js 및 브라우저 용 JavaScript로 구현 된 고성능 템플릿 엔진이다.

이 프로젝트는 이전에 "Jade"로 알려졌습니다. 그러나 "Jade"는 등록 상표라는 것이 밝혀졌습니다. 결과적으로 이름 변경이 필요했습니다. 메인테이너들 사이의 토론 끝에 "Pug" 가이 프로젝트의 새 이름으로 선택되었습니다. 버전 2부터는 "pug"가 공식 패키지 이름입니다.

패키지 또는 앱에서 현재를 사용 jade하는 경우 걱정하지 마십시오. 모든 새 버전이 .NET에서 릴리스 될 예정이지만 해당 패키지 이름을 계속 사용할 수있는 권한을 확보했습니다.

이름을 바꾸기 전에는 이미 "Jade 2.0.0"에서 작업이 시작되었습니다. 
따라서 Pug 로의 이름 변경은 주요 버전 범프와 일치했습니다. 결과적으로 Jade에서 Pug로 업그레이드하는 것은 메이저 버전 범프가있는 다른 패키지를 업그레이드하는 것과 동일한 프로세스가 됩니다.

{{< adsense >}}



## 설치

```
npm i pug
```


## Pug 문법

1. pug 샘플
```pug
doctype html
html(lang="en")
  head
    title= pageTitle
    script(type='text/javascript').
      if (foo) bar(1 + 5)
  body
    h1 Pug - node template engine
    #container.col
      if youAreUsingPug
        p You are amazing
      else
        p Get on it!
      p.
        Pug is a terse and simple templating language with a
        strong focus on performance and powerful features.
```
2. 변환된 html
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Pug</title>
    <script type="text/javascript">
      if (foo) bar(1 + 5)
    </script>
  </head>
  <body>
    <h1>Pug - node template engine</h1>
    <div id="container" class="col">
      <p>You are amazing</p>
      <p>Pug is a terse and simple templating language with a strong focus on performance and powerful features.</p>
    </div>
  </body>
</html>
```

## Express 에서 pug 적용
- Express 에서 pug 를 사용하려면 먼저 아래와 같이 설정을 해줘야 한다. 
- "views"는 pug 파일 경로를 설정하는 것이다. 

```js
const app = express();

app.set("view engine", "pug");
app.set("views", process.cwd() + "/src/views");

// (localhost:4000/home 경로로 들어왔을 때, "home.pug" 파일을 렌더링하게 되어 있다. pageTitle은 템플릿 파일로 넘겨줄 변수
export const home = (req, res) => res.render("home", { pageTitle: "Home" });

```

{{< alert info >}}
아래처럼 기본 베이스 pug 파일(layout.pug)을 생성하고 다른 pug 파일(home.pug)에서 해당 템플릿을 사용할 수 있다. 
{{< /alert >}}

```pug
// layout.pug
doctype html
html(lang="ko")
    include partials/head.pug
    body
    include partials/header.pug
        main
            block content
    include partials/footer.pug
```

```pug
// home.pug
extends layout.pug

block content
    h1 Home
```




참고 : 
[공식 사이트](https://pugjs.org/api/getting-started.html),
[깃헙](https://github.com/pugjs/pug)


