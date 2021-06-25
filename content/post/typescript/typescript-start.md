---
title: "Typescript 시작하기"
date: 2021-06-25T16:37:27+09:00
categories: 
- development
- typescript
tags: 
- development
- front-end
- typescript
- javascript
keywords: 
- development
- front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/typescript/img-1.png"
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->
![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/typescript/img-1.png)

{{< adsense >}}

# Typescript

## Typescript 란 ?
### : 정적 타입 검사자 (TypeScript: A Static Type Checker)

마이크로소프트에서 구현한 JavaScript의 슈퍼셋(Superset) 프로그래밍 언어. 확장자로는 .ts를 사용하며, 컴파일의 결과물로 JavaScript 코드를 출력한다. 최종적으로 런타임에서는 이렇게 출력된 JavaScript 코드를 구동시키게 된다. TypeScript라는 이름답게 정적 타입을 명시할 수 있다는 것이 순수한 자바스크립트와의 가장 큰 차이점이다. 덕분에 개발 도구(IDE나 컴파일러 등)에게 개발자가 의도한 변수나 함수 등의 목적을 더욱 명확하게 전달할 수 있고, 그렇게 전달된 정보를 기반으로 코드 자동 완성이나 잘못된 변수/함수 사용에 대한 에러 알림 같은 풍부한 피드백을 받을 수 있게 되므로 순수 자바스크립트에 비해 어마어마한 생산성 향상을 꾀할 수 있다. 즉, '자바스크립트를 실제로 사용하기 전에 있을만한 타입 에러들을 미리 잡는 것' 이 타입스크립트의 사용 목적이다.

개발자와 도구 간의 상호작용에서 뿐만 아니라 개발자 간의 상호작용에서도 상당한 이점이 있는데, API를 구현하고 사용함에 있어 해당 API의 인풋과 아웃풋이 무엇인지 명확하게 표현할 수 있으므로, API 하나 쓰는데에도 일일이 매뉴얼을 찾아봐야 하거나 심하면 해당 API의 코드까지 뒤적거려봐야 하는 자바스크립트에 비해 효율적이다.


## Typescript 설치

```
npm i -g typescript
```


## Typescript 문법



참고 : 
[https://namu.wiki/w/TypeScript](https://namu.wiki/w/TypeScript),
[https://typescript-kr.github.io/](https://typescript-kr.github.io/)
