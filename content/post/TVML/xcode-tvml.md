---
title: "XCODE TVML app"
date: 2021-05-21T10:20:38+09:00
categories: 
- development
- TVML
tags: 
- development
- front-end
- swift
- tvml
- tvos
- xcode
- ์ค์ํํธ
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcysiXz%2FbtqUl9XiOJr%2FOK52muaNh5GmEIVvkWHgOk%2Fimg.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

<!--toc-->

## XCODE TVML app ๐ฉ๐ปโ๐ป

xcode์์ tvml ์ํ ์ฑ์ ๋ง๋ค์ด ํ์คํธ ํด๋ณด๊ธฐย 


### STEP 1.

xcode ์ค์นย 

[developer.apple.com/xcode/downloads/](https://developer.apple.com/xcode/downloads/)


### STEP 2.

xcode ๋ฅผ ์ด๊ณ , create new project ๋ฅผ ํตํด tvOS ํญ์์ TVML App ์ ์ ํ ํ next ๋ฒํผ์ ๋๋ฅธ๋ค.ย 

๋ค์ product name๊ณผ language ๋ฑ์ ์ ํํ๋ค.ย 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcsN4SB%2FbtqUnJDJxcZ%2FEIZsfYW5I4TsNJMCXnh3ek%2Fimg.png)

{{< adsense >}}
### STEP 3.

ํฐ๋ฏธ๋์ ํตํด ํด๋น ํ๋ก์ ํธ ๋๋ ํ ๋ฆฌ๋ก ๊ฐ์ ์น์๋ฒ๋ฅผ ์คํํ๋ค.ย 

๋งฅ์ ๊ธฐ๋ณธ์ ์ผ๋ก python์ด ์ค์น ๋์ด ์์ผ๋ฏ๋ก

python -m SimpleHTTPServer 9001

๋๋ย 

ruby -run -ehttpd . -p9001

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmcRCi%2FbtqUf0fIhiI%2Fd5BoQBsVlRIjiJHZKH0dvk%2Fimg.png)

### STEP 4.

์๋ฎฌ๋ ์ดํฐ๋ฅผ apple tv 4k ๋ก ์ ํํ ํ,ย 

์๋จ ์ผ์ชฝ์ play ๋ฒํผ์ ํด๋ฆญํ๋ฉด ๋น๋๊ฐ ์คํ๋๋ค.ย 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAHQpy%2FbtqUmIrxrA1%2Fg1c4J4HKr06vvSzfewpGv1%2Fimg.png)

### ERRORย 

์ฒ์ ์คํํ๋ฉด ๋๋ฉ์ธ ๊ด๋ จ ์ค๋ฅ๊ฐ ๋ฐ์ํ๋ค.ย 

์น์๋ฒ๋ฅผ ๋ก์ปฌ๋ก ๋๋ ค์ http ๋ณด์ ์ค๋ฅ๊ฐ ๋ฐ์ํ์๊ธฐ ๋๋ฌธ์ ํด๋น ๋ผ์ธ์ ์ถ๊ฐํ๊ณ  YES ๋ก ๋ฐ๊ฟ์ค๋ค.ย 

๋ค์ play ๋ฒํผ์ ๋๋ฌ์ ์คํํ๋ฉด ์๋ฃ!

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fnmeyh%2FbtqUk0fdHQE%2FGZ0NYKckk3xKe8yakfKwZk%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcysiXz%2FbtqUl9XiOJr%2FOK52muaNh5GmEIVvkWHgOk%2Fimg.png)

