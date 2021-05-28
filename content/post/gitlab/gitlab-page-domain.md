---
title: "gitlab pages에 나의 도메인 연결하기"
date: 2020-02-13T22:20:42+09:00
categories: 
- development
- gitlab
tags: 
- development
- front-end
- gitlab
- 깃랩
- 도메인
- 깃랩페이지
- 블로그
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FB7wAZ%2FbtqBUTZRU2a%2FZkVPDNukK7yJTuC8it3Mv1%2Fimg.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

먼저 gitlab repository를 새로 만들고 , 

정적 웹페이지 든 spa 이든 프로젝트 폴더를 만들고 

.gitlab-ci.yml 파일을 새로 만들어서 아래와 같이 입력한다. 

```
image: node:latest

cache:
  paths:
    - node_modules/

before_script:
  - npm install

# test:
#   stage: test
#   script:
#     - CI=true npm test

pages:
  stage: deploy
  script:
    - CI=true npm run build
    - rm -rf public
    - mv build public
  artifacts:
    paths:
      - public # GitLab pages serve from a 'public' directory
  only:
    - master # run on master branch
```

그리고 git push 를 하면 자동으로 위와 같이 빌드를 하게되고, 해당 웹사이트에서 자동으로 배포되는 것을 알 수 있다. 

보통 프로젝트 이름은 _**사용자아이디.gitlab.io**_

이 페이지로 들어가면 웹사이트를 확인할 수 있다. 

<추가 설명>

[https://velog.io/@wickedev/Gitlab-CICD-%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC-bljzphditt](https://velog.io/@wickedev/Gitlab-CICD-%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC-bljzphditt)

그리고 나의 도메인으로 이 페이지가 보여지기 위해서

도메인을 연결해야 한다. 

gitlab프로젝트 에서 설정 > 페이지 메뉴로 들어가면,

아래와 같이 new Domain버튼을 누르고 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdVmYFg%2FbtqBUS00PcU%2FLDg2QEamgfgzriDV9T6wV0%2Fimg.png)

도메인 이름을 적은 뒤 create new domain버튼을 눌러주면 된다. 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FB7wAZ%2FbtqBUTZRU2a%2FZkVPDNukK7yJTuC8it3Mv1%2Fimg.png)
좀 기다리면 도메인이 연동되고, 

해당 도메인으로 깃랩 페이지가 연결되어 해당 페이지를 볼 수 있다.


{{< adsense >}}