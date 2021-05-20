---
title: "Git 오류 fatal: refusing to merge unrelated histories"
date: 2021-05-20T10:45:13+09:00
categories: 
- development
- git
tags: 
- development
- front-end
- git
- push
- error
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

git clone 후, git push 하는 과정 중에 

다음과 같이 오류가 날 경우가 있다. 

이는 push 하기 전에 git pull 을 먼저 실행해야 하는데 그 전에 수정했던 어떤 커밋과 꼬여 오류가 날 경우..

```
fatal: refusing to merge unrelated histories
```

이럴 때는 

아래처럼 실행하주고, 

다시 git push를 하면 해결됨

```
git pull origin 브런치명 --allow-unrelated-histories
```