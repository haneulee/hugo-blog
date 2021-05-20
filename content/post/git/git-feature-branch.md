---
title: "Git Feature 브랜치 생성 & push"
date: 2021-05-18T16:01:06+09:00
categories: 
- development
- git
tags: 
- development
- front-end
- git
- feature
- branch
- 피처
- 브랜치
- 깃
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


# branch 생성

```
$ git branch <branchName>
```

# 생성한 브랜치로 이동

```
$ git checkout <branchName>
```

```
// 브랜치 생성 & 체크아웃
$ git checkout -b <branchName>
```

# 원격 저장소에 push 하기

로컬에서만 생성한 branch를 upstream branch로 만든다.

```
$ git push --set-upstream origin <branchName>
```
