---
title: "Express ๋? ๐๐ค "
date: 2021-05-26T14:07:54+09:00
categories:
  - development
  - express
tags:
  - development
  - front-end
  - express
  - nodeJS
  - ์๋ฒ
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

## ์ค๋ช

- Express๋ ์น ๋ฐ ๋ชจ๋ฐ์ผ ์ ํ๋ฆฌ์ผ์ด์์ ์ํ ์ผ๋ จ์ ๊ฐ๋ ฅํ ๊ธฐ๋ฅ์ ์ ๊ณตํ๋ ๊ฐ๊ฒฐํ๊ณ  ์ ์ฐํ Node.js ์น ์ ํ๋ฆฌ์ผ์ด์ ํ๋ ์์ํฌ์๋๋ค.
- ์์ ๋กญ๊ฒ ํ์ฉํ  ์ ์๋ ์๋ง์ HTTP ์ ํธ๋ฆฌํฐ ๋ฉ์๋ ๋ฐ ๋ฏธ๋ค์จ์ด๋ฅผ ํตํด ์ฝ๊ณ  ๋น ๋ฅด๊ฒ ๊ฐ๋ ฅํ API๋ฅผ ์์ฑํ  ์ ์์ต๋๋ค.
## ์ค์น

```
npm install express
```

## API

{{< adsense >}}

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
//GET ๋ฐฉ์์ METHOD
app.get("/", function (req, res) {
  res.send("hello getMethod");
});

//POST ๋ฐฉ์์ MEHTOD
app.post("/", function (req, res) {
  res.send("Hello postMethod");
});
```

### Router()

```js
import express from "express";

const testRouter = expres.Router(); // testRouter ์ธ์คํด์ค ์์ฑ

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

๋ฏธ๋ค์จ์ด ํจ์๋ ์์ฒญ ์ค๋ธ์ ํธ(req), ์๋ต ์ค๋ธ์ ํธ (res), ๊ทธ๋ฆฌ๊ณ  ์ ํ๋ฆฌ์ผ์ด์์ ์์ฒญ-์๋ต ์ฃผ๊ธฐ ์ค ๊ทธ ๋ค์์ ๋ฏธ๋ค์จ์ด ํจ์ ๋ํ ์ก์ธ์ค ๊ถํ์ ๊ฐ๋ ํจ์์๋๋ค. ๊ทธ ๋ค์์ ๋ฏธ๋ค์จ์ด ํจ์๋ ์ผ๋ฐ์ ์ผ๋ก next๋ผ๋ ์ด๋ฆ์ ๋ณ์๋ก ํ์๋ฉ๋๋ค.

๋ฏธ๋ค์จ์ด ํจ์๋ ๋ค์๊ณผ ๊ฐ์ ํ์คํฌ๋ฅผ ์ํํ  ์ ์์ต๋๋ค.
- ๋ชจ๋  ์ฝ๋๋ฅผ ์คํ.
- ์์ฒญ ๋ฐ ์๋ต ์ค๋ธ์ ํธ์ ๋ํ ๋ณ๊ฒฝ์ ์คํ.
- ์์ฒญ-์๋ต ์ฃผ๊ธฐ๋ฅผ ์ข๋ฃ.
- ์คํ ๋ด์ ๊ทธ ๋ค์ ๋ฏธ๋ค์จ์ด ํจ์๋ฅผ ํธ์ถ.

ํ์ฌ์ ๋ฏธ๋ค์จ์ด ํจ์๊ฐ ์์ฒญ-์๋ต ์ฃผ๊ธฐ๋ฅผ ์ข๋ฃํ์ง ์๋ ๊ฒฝ์ฐ์๋ next()๋ฅผ ํธ์ถํ์ฌ ๊ทธ ๋ค์ ๋ฏธ๋ค์จ์ด ํจ์์ ์ ์ด๋ฅผ ์ ๋ฌํด์ผ ํฉ๋๋ค. ๊ทธ๋ ์ง ์์ผ๋ฉด ํด๋น ์์ฒญ์ ์ ์ง๋ ์ฑ๋ก ๋ฐฉ์น๋ฉ๋๋ค.


```js
var express = require("express");
var app = express();

// ๋ฏธ๋ค์จ์ด ํจ์ ์์ฑ ํ ๋ณ์ ํ ๋น
var requestTime = function (req, res, next) {
  req.requestTime = Date.now();
  next();
};

// ๋ฏธ๋ค์จ์ด ํจ์๋ฅผ ๋ก๋ํ๋ ค๋ฉด ๋ฏธ๋ค์จ์ด ํจ์๋ฅผ ์ง์ ํ์ฌ app.use()๋ฅผ ํธ์ถ
// ๋ฃจํธ ๊ฒฝ๋ก ๋ผ์ฐํธ ๋ก๋ ์ ์ ๋จผ์  ๋ก๋ ๋๋ค.
app.use(requestTime); 

// ์ฝ๋ฐฑ ํจ์๋ ๋ฏธ๋ค์จ์ด ํจ์๊ฐ req(์์ฒญ ์ค๋ธ์ ํธ)์ ์ถ๊ฐํ๋ ํน์ฑ์ ์ฌ์ฉํ๋ค.
app.get("/", function (req, res) {
  var responseText = "Hello World!";
  responseText += "Requested at: " + req.requestTime + "";
  res.send(responseText);
});
app.listen(3000);
```

์ฐธ๊ณ  :
[https://developer.mozilla.org/ko/docs/Learn/Server-side/Express_Nodejs/Introduction](https://developer.mozilla.org/ko/docs/Learn/Server-side/Express_Nodejs/Introduction)
[https://expressjs.com/ko/](https://expressjs.com/ko/)
