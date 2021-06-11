---
title: "리액트 절대 경로 설정하기"
date: 2021-05-18T12:26:22+09:00
categories: 
- development
- react
tags: 
- development
- front-end
- react
- 리액트
- 절대경로
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImage: ""
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

<!--toc-->

# 리액트 절대 경로 설정하기

Web을 개발하다보면 폴더와 파일의 depth가 깊어지는 경우가 있다.

이런 경우 파일 import시에 ../../components/sign/logout 식으로 ../가 많아져서 복잡하고 번거로워진다.

그러나 절대경로를 설정하면 components/sign/logout 으로 간단히 작성할 수 있다는 사실!

나는 src 폴더를 기준으로 절대경로를 설정하였다.

방법은 아래와 같다.

{{< adsense >}}


## **| Linux, Mac 에서 설정하기**

프로젝트의 package.json 로 이동 후, scripts의 start, build 부분을 다음과 같이 수정한다.

```
"start": "NODE_PATH=src/ react-scripts start",
"build": "NODE_PATH=src/ react-scripts build",
```

## **| Window 에서 설정하기**

여기서는 cross-env가 필요하다.

먼저 다음 command를 이용해 cross-env를 설치해준다.

```
yarn add cross-env
```

그리고 프로젝트의 package.json으로 이동 후, scripts의 start, build 부분을 다음과 같이 수정한다.

```
"start": "cross-env NODE_PATH=src/ react-scripts start",
"build": "cross-env NODE_PATH=src/ react-scripts build",
```

## **| 기타**

처음에 NODE\_PATH를 설정할 때 src로 설정했더니 빌드시에 경로를 제대로 못 잡아서 src/로 잡아주었더니 해결되었다.

