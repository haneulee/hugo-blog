---
title: "Express 란? 🚀🤔 "
date: 2021-05-26T14:07:54+09:00
categories:
  - development
  - express
tags:
  - development
  - front-end
  - express
  - nodeJS
  - 서버
  - server
keywords:
  - development
  - front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/express/img-1.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

<!--toc-->

# Express

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/express/img-1.png)

## 설명

- Express는 웹 및 모바일 애플리케이션을 위한 일련의 강력한 기능을 제공하는 간결하고 유연한 Node.js 웹 애플리케이션 프레임워크입니다.
- 자유롭게 활용할 수 있는 수많은 HTTP 유틸리티 메소드 및 미들웨어를 통해 쉽고 빠르게 강력한 API를 작성할 수 있습니다.

## 설치

```
npm install express
```

## API

```js
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`);
});
```

### get() & post()

```js
//GET 방식의 METHOD
app.get("/", function (req, res) {
  res.send("hello getMethod");
});

//POST 방식의 MEHTOD
app.post("/", function (req, res) {
  res.send("Hello postMethod");
});
```

### Router()

```js
import express from "express";

const testRouter = expres.Router(); // testRouter 인스턴스 생성

//default index route
testRouter.get("/", function (req, res) {
  res.send("Hi!! Home!!");
});

//main route
testRouter.get("/main", function (req, res) {
  res.send("Hi!! Main!!");
});
//end route
testRouter.get("/end", function (req, res) {
  res.send("Hi!! end!!");
});

export default teestRouter;
```

### middleware
![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/express/img-2.png)

미들웨어 함수는 요청 오브젝트(req), 응답 오브젝트 (res), 그리고 애플리케이션의 요청-응답 주기 중 그 다음의 미들웨어 함수 대한 액세스 권한을 갖는 함수입니다. 그 다음의 미들웨어 함수는 일반적으로 next라는 이름의 변수로 표시됩니다.

미들웨어 함수는 다음과 같은 태스크를 수행할 수 있습니다.
- 모든 코드를 실행.
- 요청 및 응답 오브젝트에 대한 변경을 실행.
- 요청-응답 주기를 종료.
- 스택 내의 그 다음 미들웨어 함수를 호출.

현재의 미들웨어 함수가 요청-응답 주기를 종료하지 않는 경우에는 next()를 호출하여 그 다음 미들웨어 함수에 제어를 전달해야 합니다. 그렇지 않으면 해당 요청은 정지된 채로 방치됩니다.


```js
var express = require("express");
var app = express();

// 미들웨어 함수 작성 후 변수 할당
var requestTime = function (req, res, next) {
  req.requestTime = Date.now();
  next();
};

// 미들웨어 함수를 로드하려면 미들웨어 함수를 지정하여 app.use()를 호출
// 루트 경로 라우트 로드 전에 먼저 로드 된다.
app.use(requestTime); 

// 콜백 함수는 미들웨어 함수가 req(요청 오브젝트)에 추가하는 특성을 사용한다.
app.get("/", function (req, res) {
  var responseText = "Hello World!";
  responseText += "Requested at: " + req.requestTime + "";
  res.send(responseText);
});
app.listen(3000);
```

참고 :
[https://developer.mozilla.org/ko/docs/Learn/Server-side/Express_Nodejs/Introduction](https://developer.mozilla.org/ko/docs/Learn/Server-side/Express_Nodejs/Introduction)
[https://expressjs.com/ko/](https://expressjs.com/ko/)
