---
title: "브라우저 세션 & 쿠키 Browser Session & cookies 🍪"
date: 2021-06-11T13:50:39+09:00
categories: 
- development
- browser
tags: 
- development
- front-end
- browser
- 브라우저
- session
- cookie
- history
- web
keywords: 
- development
- front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/browser/img-1.png"
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

# 브라우저 세션 Browser Session  
![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/browser/img-1.png)

## Session
- 브라우저와 백엔드 사이의 memory or history
- 쿠키는 상태 데이터를 클라이언트에 저장했다면, 세션은 서버에 저장
- 세션은 기본적으로는 쿠키를 사용하지만 세션 id만 쿠키로 저장하고, 상태 데이터들은 세션 id를 id로하여 서버에 저장한다.
{{< adsense >}}


### stateless

server side에 client와 server의 동작, 상태정보를 저장하지 않는 형태, server의 응답이 client와의 세션 상태와 독립적임
장점 : 서버가 client정보를 저장관리 하지 않으므로 Scaling이 자유로움

ex)
UDP / HTTP : UDP는 TCP와 달리 Client의 세션 상태와 관계 없이 요청에 대한 응답만을 수행하고, server가 client의 정보를 저장하지 않는다.

### stateful

server side에 client와 server의 동작, 상태정보를 저장하는 형태, 세션 상태에 기반하여 server의 응답이 달라짐

ex)
TCP : TCP의 server와 client는 1. establishing connection, 2. Trasmitting data 3. Terminating connection 이라는 TCP handshake 과정을 통해서 연결되며 데이터를 전송하여, server가 client의 세션 정보를 저장한다.

{{< adsense >}}

# 브라우저 쿠키 Browser Cookies 


## Cookies
- 브라우저와 백엔드 사이의 memory or history
- 클라이언트 로컬에 저장되는 key-value 형태의 데이터
- 클라이언트에서 서버에 request할때 쿠키를 담아 보내면, 서버에서는 쿠키에서 상태 데이터를 읽고 클라이언트의 상태를 파악하여 그에 따른 response를 준다.

{{< adsense >}}


### 쿠키 vs 세션

||쿠키|세션|
|------|---|---|
|저장위치|클라이언트|서버|
|보안|안좋음|좋음|
|서버부하|없음|높음|
|생명주기|브라우저 종료시 유지|테스브라우저 종료시 소멸|
|속도|빠름|느림|

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/browser/img-2.png)

참고 : 
![https://velog.io/@makeitcloud/%EB%9E%80-Stateless-Stateful-%EC%9D%B4%EB%9E%80](https://velog.io/@makeitcloud/%EB%9E%80-Stateless-Stateful-%EC%9D%B4%EB%9E%80),
![https://velog.io/@damiano1027/CS-%EC%BF%A0%ED%82%A4Cookie%EC%99%80-%EC%84%B8%EC%85%98Session](https://velog.io/@damiano1027/CS-%EC%BF%A0%ED%82%A4Cookie%EC%99%80-%EC%84%B8%EC%85%98Session),