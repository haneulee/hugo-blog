---
title: "Aws Certificate Manager"
date: 2020-02-13T19:28:20+09:00
categories: 
- development
- aws
tags: 
- development
- front-end
- aws
- certificate manager
- ssl
- 보안
- 인증서
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

aws Certificate Manager 에서는 무료로 ssl 공인 인증서를 받을 수 있다.

ssl 인증서는 https로 웹사이트를 통신하기 위해서 

꼭 필요한 것이다. 

aws 서비스에서 certificate Manager 혹은 ssl 으로 검색하면 아래와 같이 공인 인증서에 체크하고,

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbA8xSr%2FbtqBVe3N1CT%2FEO8KMTG2b9ecPEMGX3oZTK%2Fimg.png)

도메인 이름을 등록하고,

여기서는 \*.test.com 또는 [test.com](http://test.com), [www.test.com](http://www.test.com) 이렇게 입력해도 좋다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdqLxWN%2FbtqBVM0c7z6%2FKWZNuAEST0ljF2eHpoXaW1%2Fimg.png)


dns 검증을 선택하고, 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FR9zwd%2FbtqBYfGGseY%2F4LLVI5mAiKYg4awqwuUxuk%2Fimg.png)


태그는 그냥 다음으로 넘어가고, 

확인 및 요청을 누르면 

무료 ssl 인증서를 신청하게 된다. 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FunfTZ%2FbtqBXHcAz6Y%2FFivB8QSJKO0tnkgXXGJk60%2Fimg.png)

신청이 완료되고, 인증서 목록에서 하위에 route 53에서 레코드 생성을 해줘야 

자동으로 내가 가지고 있는 도메인에 연동이 되어 

https://로도 접속이 가능하게 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbFYnBt%2FbtqBWB4ZAMi%2F4CNXT8e1pcmH1Zue2UL7Pk%2Fimg.png)



{{< adsense >}}