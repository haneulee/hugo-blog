---
title: "리액트 뒤로가기 Bfcache"
date: 2022-10-06T13:22:12+02:00
categories:
  - development
tags:
  - development
  - front-end
  - 리액트 뒤로가기 Bfcache
  - react
  - bfcache
  - cache
  - logout
  - 로그아웃
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: "https://web-dev.imgix.net/image/admin/Qoeb8x3a11BdGgRzYJbY.png?auto=format&w=1600"
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

![](https://web-dev.imgix.net/image/admin/Qoeb8x3a11BdGgRzYJbY.png?auto=format&w=1600)

# 리액트 뒤로가기 Bfcache 처리하기

<!--adsense-->

## BF cache 란 ?

- bfcache는 인메모리 캐시로, 자바스크립트 힙까지 포함해 페이지 전체를 완전히 캐시로 저장해버리는 것을 의미한다.
- 전체 페이지가 메모리 안에 있기 때문에, 사용자가 이전페이지로 돌아가고자 했을 때 빠르게 전체 페이지를 보여줄 수 있다.

{{< videoPlay src="https://i.ytimg.com/vi_webp/cuPsdRckkF0/hqdefault.webp" >}}

## 이슈

- 사용자가 로그아웃 후에 뒤로가기 버튼을 클릭하여 전 페이지로 돌아왔을 때 BF cache 때문에 서버에서 리소스를 다운로드 하지 않아 authentication 체크하는 부분이 실행되지 않음
- 로그아웃을 하고 뒤로가기를 하면 사용자가 이용하던 페이지를 볼 수 없게 하거나 로그인 페이지로 이동해야 함

## 해결방법

```
const pageShowHandler = useCallback(
    (event: PageTransitionEvent) => {
      if (event.persisted) {
        window.location.reload();
      }
    },
    [location]
  );

  useEffect(() => {
    window.addEventListener("pageshow", pageShowHandler);
    return () => {
      window.removeEventListener("pageshow", pageShowHandler);
    };
  }, [pageShowHandler]);
```

- 브라우저의 pageshow 이벤트를 사용하여 이전페이지로 돌아왔을 때 BF cache가 있는지 확인 (window.persisted)
- 있다면 페이지를 다시 리로드 하도록 수정
  - reload() 대신 원하는 API 콜 또는 다른 로직을 넣을 수 있다.

---

참고 :
[https://web.dev/bfcache/](https://web.dev/bfcache/)
[https://yceffort.kr/2020/11/back-forward-cache](https://yceffort.kr/2020/11/back-forward-cache)
