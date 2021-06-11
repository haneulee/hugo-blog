---
title: "NextJS 서버 사이드 렌더링 👩🏻‍💻"
date: 2021-05-26T14:32:39+09:00
categories: 
- development
- nextjs
tags: 
- development
- front-end
- nextjs
- 서버사이드렌더링
- 프론트엔드
- 프레임워크
- 정적사이트
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/nextjs/img-1.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---


<!--toc-->

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/nextjs/img-1.png)

# NextJS

## Next.js는 무엇인가?
{{< adsense >}}
Next.js는 리액트를 SSR(Server-Side rendering) 방식을 구현할 수 있도록 도와주는 프레임워크이다.
정확하게는, SSR과 CSR의 각 장점을 조합하여 동작하게 된다.


## SSR과 CSR의 차이
기본적으로 처음 웹 화면을 접속하면, DOM과 스크립트 코드, 리소스 등 해당 웹 페이지를 구성하기 위해 필요로 한 모든 요소들을 서버에서 로드하게 된다.

SSR은 화면에서 보여줄 특정 페이지의 View를 서버 단에서 렌더링을 한 후, 클라이언트에게 제공된다. View를 빠르게 렌더링 후에 사용자에게 미리 웹 화면으로 보여주고, 이후에 웹 페이지를 동작하게 하거나 구성하는 리소스들을 로드하도록 한다. 그러면 사용자는 첫 화면을 보게 되면, 아직은 기능이 동작하지는 않지만 매우 빠른 로딩처럼 느낄 수가 있기 때문이다.

대신 다른 페이지로 넘어갈 때는, 넘어가려는 페이지를 다시 요청, 렌더링을 해야 하므로 CSR보다 느리다는 단점이 있다.

반대로 CSR은 모든 페이지의 View를 클라이언트로 로드 후에 렌더링을 하게 되므로, 로딩 시간이 SSR보다 느리다.
하지만 다른 페이지로 넘어갈 때, 이미 모든 페이지가 렌더링이 되어 있기 때문에 SSR보다 빠르게 동작한다.

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/nextjs/img-2.png)


## Next.js의 렌더링 동작 원리
SSR의 장점은 접속하려는 페이지의 View를 빠르게 렌더링하고 사용자에게 보여줌으로써, 처음 화면 로딩 시간이 빠르다는 것이다. 
그래서 Next.js에서는 링크를 통한 접속이나 주소를 통한 접속은 SSR 방식을 이용하게 된다.
CSR의 장점은 이미 클라이언트에서 전체 페이지가 렌더링이 되어 있어 페이지 전환이 빠르다. 그래서 이벤트를 통한 페이지 접속은 CSR 방식으로 일어나도록 되어있다.



참고 :
[NextJS 공식문서](https://nextjs.org/)
