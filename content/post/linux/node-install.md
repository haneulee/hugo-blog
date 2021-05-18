---
title: "리눅스 nodejs, npm 설치"
date: 2021-05-18T12:37:15+09:00
categories: 
- development
- linux
- nodejs
tags: 
- development
- front-end
- linux
- nodejs
- npm
- 서버
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: ""
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

## 1\. Nodejs 설치

-   설치에 관련된 설명은 아래 링크를 참조하였습니다.

[https://nodejs.org/ko/download/package-manager/](https://nodejs.org/ko/download/package-manager/)

-   Nodejs 10버전을 설치하기 위하여 아래명령어를 실행합니다.

$ curl --silent --location [https://rpm.nodesource.com/setup\_10.x](https://rpm.nodesource.com/setup_8.x) | sudo bash --

!()[https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLXdlF%2FbtqF9miYdcH%2F96dCLQzg5wuxSEqGJYgAsk%2Fimg.png]

-   Node.js 설치 준비가 완료되었습니다. 아래의 명령어로 install 합니다.

$ yum install nodejs -y

-   설치를 확인합니다

$ node --version $ npm --version