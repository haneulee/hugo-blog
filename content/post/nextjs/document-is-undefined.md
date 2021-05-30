---
title: "NextJS - document is not defined 오류"
date: 2021-05-30T16:51:26+09:00
categories: 
- development
- nextjs
tags: 
- development
- front-end
- nextjs
- document
- 프론트엔드
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/nextjs/img-3.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---
<!--toc-->
{{< adsense >}}


![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/nextjs/img-3.png)

# document is not defined 오류 해결방법

- 서버사이드 렌더링인 nextJS를 사용할 때는 window 또는 Document 객체를 사용할 수 없다. 


## 해결 방법

### 첫번째
- window 오브젝트가 있는지 확인하는 조건문을 추가하여 렌더링 된 다음에 document 코드를 실행하도록 한다.

```
if (typeof window === 'object') {
// Check if document is finally loaded
   document.addEventListener("DOMContentLoaded", function () {
       alert('Finished loading')
     });
  }
```

### 두번째
- nextJS는 react를 사용할 수 있기 때문에 react에서 컴포넌트가 마운트 또는 업데이트 된 다음에 동작하는 componentDidMount 또는 useEffect 훅을 사용하여 체크한다.
```
import {useEffect} from "react";

useEffect(() => {
    alert('Finished loading');
  }, []);
```

### 세번째
- process.browser는 지금 deprecated 되었으므로 process.client를 사용해서 렌더링 여부를 확인한다.
```
if (process.browser) {
    document.addEventListener("DOMContentLoaded", function () {
       alert('Finished loading');
     });
   }
```


참고 : 
[https://dev.to/typicoul/fixing-next-js-referenceerror-document-is-not-defined-2jgi](https://dev.to/typicoul/fixing-next-js-referenceerror-document-is-not-defined-2jgi)


