---
title: "티스토리 Code Block"
date: 2020-02-09T13:15:32+09:00
thumbnailImagePosition: left
thumbnailImage: https://blog.kakaocdn.net/dn/m42J6/btqBRwvm8CS/RwybAlxm2zeLp2zEk32w91/img.png
categories: ["development", "codeblock"]
tags: ["code", "block", "티스토리", "코드블럭"]
keywords: ["AWS", "Route53"]
cover: ""
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

개발 블로그를 작성하다보면 코드 블럭을 사용하는 경우가 많다. 

그런데 아래처럼 코드블럭이 그냥 일반 텍스트처럼 나와 매우 가독성이 떨어진다. 

따라서 티스토리 블로그의 코드블럭 스타일을 변경하기로 했다. 

![](https://blog.kakaocdn.net/dn/GrZYu/btqBNMNomxQ/f9wfkU88g7Umz5L3CsjyR0/img.png)


**2가지 방법이 있는데, **

**1\. 관리페이지 > 플러그인 > 코드블럭 > 마음에 드는 스타일 설정**

**2\. 스킨편집 > html 편집 > 'head'태그 안에 Highlight.js 임포트**

2번 방법은

먼저 아래 코드를 <head>태그 안에 넣으면 됨!

[https://highlightjs.org/static/demo/](https://highlightjs.org/static/demo/)에서 마음에 드는 데모 스타일을 고르고 아래 코드에서 default.min.css 에서 default를 다른 스타일 이름으로 변경하면 된다. 


```html
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.5.0/styles/default.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.5.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>
```
{{< adsense >}}

![](https://blog.kakaocdn.net/dn/m42J6/btqBRwvm8CS/RwybAlxm2zeLp2zEk32w91/img.png)

2번 방법을 따라해보았지만 이상하게 스타일이 변경되지 않았다. 

따라서 1번 방법으로 설정!

내가 원하는 테마는 Darcular 였기 때문에 플러그인으로 쉽게 변경할 수 있었다. 

![](https://blog.kakaocdn.net/dn/zBpLt/btqBQ2nKxw1/H8M1NjN6KDoNJJ7zQBxw3k/img.png)

