---
title: "Git - 이미 commit한 author 수정하기"
date: 2021-05-24T18:09:54+09:00
categories: 
- development
- git
tags: 
- development
- front-end
- git
- author
- commit
- 커밋수정
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/git/img-2.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---
<!--toc-->

# git config user.email 수정

```
git config --global user.email "이메일"
git config --global user.name "이름"
```

# author(이름)을 바꿀 commit 지정
git rebase 명령을 통해 author을 바꿀 커밋을 선택해준다.

```
// ~ 뒤에 입력한 숫자는 4번째 커밋까지 선택
git rebase -i HEAD~4
```
 

그럼 아래와 같은 vi 화면이 뜨는데 변경할 커밋의 pick => e로 변경해주고 :wq 를 눌러 저장, 종료해준다.
![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/git/img-2.png)

```
git rebase -i HEAD~4
```

 

# 변경할 author 입력
git commit --amend --author="아이디 <이메일>" 입력

```
git commit --amend --author="haneulee <lovesky4294@gmail.com>"
```
 

 

# git rebase --continue,  git push origin master
github repository에 이름 수정 내역 반영

```
git rebase --continue

git push origin master
```
 

참고 :
[https://korband.tistory.com/34](https://korband.tistory.com/34)


{{< adsense >}}