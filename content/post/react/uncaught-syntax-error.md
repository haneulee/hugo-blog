---
title: "React Uncaught Syntax Error: unexpected token '<' 리액트 에러"
date: 2023-01-13T14:25:20+01:00
categories:
  - development
tags:
  - development
  - front-end
  - Uncaught Syntax Error
  - react
  - unexpected token
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: "https://res.cloudinary.com/dtlpko2wf/image/upload/v1673618292/blog/Screen_Shot_2023-01-09_at_12.09.02_PM_px2qew.png"
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

![](https://res.cloudinary.com/dtlpko2wf/image/upload/v1673618292/blog/Screen_Shot_2023-01-09_at_12.09.02_PM_px2qew.png)

# React Uncaught Syntax Error: unexpected token '<' 리액트 에러

<!--adsense-->

새로운 피쳐를 작업한 후에 배포까지 잘 완료했다고 생각했는데

다음날 사이트를 접속하면 빈 화면만 보이는 것을 발견했다.

개발자 도구에 보이는 에러는

{{< alert info >}}
Uncaught SyntaxError: Unexpected token '<'  
{{< /alert >}}

## 원인

얼핏 드는 생각으로는 JS 파일을 잘 못 읽어서 생기는 문제인 것 같았다.

구글링을 해보니 리액트 개발할 때 꽤나 자주 발생하는 오류이다.

원인으로는 상황에 따라 여러가지 일 수 있으나

브라우저의 캐싱때문에 index.html 파일이 배포 전의 파일이라 배포 전 번들링한 js파일을 참조하고 있어 발생하기도 한다.

'새로고침'을 통해 파일을 제대로 불러와서 해결되기도 한다.

또는, 웹팩에서 발생하거나 변수오류 등 여러가지가 있다.

## 해결

### 방법 1.

index.html 파일의 `<head>` 태그 안에 아래 코드를 넣는다.  
하지만 base href 때문에 라우팅 사이드 이펙트 이슈가 있는 확인해야 한다.

```
<base href="/">
```

### 방법 2. 

index.html의 `<script>` 태그에 경로 설정이 잘 되어 있는지 확인해본다.  
```
// src의 "." 을 제거한다.  
<script src="./static/js/main.dfd.js">
```


### 방법 3.

리액트의 package.json 파일에 "homepage" 프로퍼티를 추가한다.

```
"homepage": ".",
```

### 방법 4.

새로 배포된 파일을 참조할 수 있도록 캐시를 안하도록 설정한다.  
index.html 파일 `<head>` 태그 안에 메타 정보를 추가한다.

```
<meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate">
<meta http-equiv="Pragma" content="no-cache">
<meta http-equiv="Expires" content="0">
```


나는 일단 첫번째 방법으로 했더니 바로 해결되었다.  

---

참고 :
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Unexpected_token](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Unexpected_token)
[https://developer.mozilla.org/en-US/docs/Web/HTML/Element/base](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/base)
