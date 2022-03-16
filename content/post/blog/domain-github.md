---
title: "도메인 구매 후, 깃헙 블로그 연동하기 🏠"
date: 2022-03-16T10:22:01+01:00
categories: 
- development
tags: 
- development
- front-end
- domain
- website
- github
- gitlab
- subdomain
- blog
- 깃헙블로그
- 도메인
- hostinger
- 호스팅어
- 서브도메인
- 네임서버
- dns
- nameserver
keywords: 
- development
- front-end
cover: ""
thumbnailImagePosition: right
thumbnailImage: https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/hostinger-3.png
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

{{< adsense >}}


# 도메인 구매 후, 깃헙 블로그 연동하기 🏠

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/hostinger-3.png)

## 도메인 구매

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/hostinger-2.png)

{{< alert info >}}
본인이 원하는 이름의 도메인으로 구매 하기!  
보통 아무도 사용하지 않는 경우, 9.99$  
{{< /alert >}}

## 웹 호스팅

웹 호스팅 가격은 싱글로 결제할 때 한달에 1.99$밖에 안된다.  
다른 곳과 비교할 때, 괜찮은 가격이어서 호스팅어로 결정..  
그리고 개인 웹사이트를 운영할 경우는 그냥 '싱글 single' 플랜을 선택해도 될것 같다.  
본인이 원하는 플랜 선택하여 앞에서 선택한 도메인이랑 같이 구매를 하면 된다.  
나는 도메인은 3년, 웹 호스팅은 4년? 정도 한꺼번에 결제했다.  
왜냐면 자꾸 갱신하는게 귀찮기 때문 ㅠㅠ  

한 10년짜리 하면 좋을 것 같은데 ㅋㅋ  

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/hostinger-1.png)

## 서브 도메인

서브 도메인은 예를 들어, blog.xxx.com 이런 식으로 도메인 이름 앞에   
추가로 붙는 것이다. tech.xxx.com 이런식으로 본인이 원하는 이름을 선택할 수 있다.  
나는 blog가 필요하기 때문에 blog 로 선택
호스팅어에서 서브도메인을 등록해주면 된다.  
싱글 플랜에서는 서브도메인이 2개밖에 안되므로 신중히 선택!  


![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/hostinger-5.png)


## 깃헙 블로그 연동

이제 앞의 단계가 끝났으면 가장 중요한 깃헙 블로그 연동이 남아 있다.  
나는 github.io 블로그를 운영하는데 도메인 이름을 바꿀 예정!  

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/hostinger-4.png)

여기 호스팅어에서 Domains 탭에 들어가면 DNS/Nameservers 하위 택을 눌러 들어간다.  

서브 도메인으로 연결해줄 경우, 아래와 같이  
Type은 CNAME으로  
Name은 본인이 원하는 이름으로  
Points to 는 깃헙 블로그 주소를 (xxx.github.io - xxx 부분이 깃헙 아이디)  
TTL은 기본으로 14400이 선택될 것이다.  

```
Type|Name|Poins to|TTL
CNAME blog haneulee.github.io 14400
```

메인 도메인으로 깃헙 블로그를 연동하고 싶으면
아래 링크에 자세히 설명되어 있다.

[github - custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
```
Type|Name|Poins to|TTL
A @ 185.199.108.153 14400
```

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/github-1.png)

그리고 깃헙에서 운영하는 깃헙블로그 프로젝트(haneulee.github.io)의 settings - Pages 탭에 들어가서  
Custom domain에 나의 서브 도메인 주소를 입력하고 Save 하면 된다.  


{{< alert info >}}
도메인 주소를 변경하면 반영되는데 좀 시간이 걸린다.....  
그래서 바로 적용이 되지 않고 호스팅 사이트마다 반영 시간이 다르기 때문에  
좀 기다려야 한다는 점 주의!!!  
{{< /alert >}}



## 깃랩 블로그 연동

나의 경우, 메인 도메인으로 포트폴리오 사이트를 운영하기 때문에 메인 도메인은 깃랩에 있는 프로젝트를 연결하기로 결정!!  

[gitlab - custom domain](https://bitek.dev/blog/custom-subdomain-namecheap-gitlab-pages/)

위 링크에 잘 설명되어 있는데 깃랩 프로젝트의 Settings - Pages 탭에 들어가서 새로운 Pages Domain을 등록해주면 된다.  
그럼 아래처럼 정보가 뜰텐데 이 도메인 정보를 호스팅 사이트 DNS에 등록해주면 된다.  

```
DNS : haneul-lee.com ALIAS haneulee.gitlab.io
Verification satus : _gitlab-pages-verification-code.haneul-lee.com TXT gitlab-pages-verification-code=xxxxxxxx
```

위 정보를 가지고, 
호스팅 사이트에 아래와 같이 DNS name 을 등록!!  

```
Type|Name|Poins to|TTL
A @ 35.185.44.232 14400
TXT @ gitlab-pages-verifaction-code=xxxxxxxx
```

도메인 적용은 시간이 좀 걸리므로  
맘 편히 가지고 기다리면 적용됨~~~~!!  
🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥  




---

참고 :
[hostinger 호스팅어](https://www.hostinger.com/),  
[github - custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site),  
[gitlab - custom domain](https://bitek.dev/blog/custom-subdomain-namecheap-gitlab-pages/)  
