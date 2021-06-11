---
title: "Githup SSH  키 생성 및 등록"
date: 2021-05-21T10:30:25+09:00
categories: 
- development
- github
tags: 
- development
- front-end
- github
- git
- ssh
- key
- ssh인증
- 개인키
- 공개키
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5at4r%2Fbtq4HHWbxKj%2FtxkRe5QG0TkjAlHB09uRAK%2Fimg.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

<!--toc-->

## Github에서 SSH key 생성

```console
// 홈 디렉토리 이동
cd ~

// ssh 키 디렉토리 생성
mkdir ~/.ssh
chmod 700 ~/.ssh
cd .ssh

{{< adsense >}}

// ssh 사용자 키 생성
ssh-keygen -t rsa -b 4096 -C “lovesky4294@gmail.com”

// 아래와 같이 뜨면 "엔터" 입력
Generating public/private rsa key pair.
Enter file in which to save the key (/home/user/.ssh/id_rsa):

// 아래와 같이 뜨면 비밀먼호 두번 입력
Enter passphrase (empty for no passphrase): 
Enter same passphrase again:
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FclbTFB%2Fbtq4BxHN5gr%2FNZHG8WR6QKczxD0Vu7fJR0%2Fimg.png)

키 생성 완료 !!

ls -l 입력하여 생성된 키 확인 !

id\_rsa 는 개인키, id\_rsa.pub 은 공개키 (개인키는 절대 공개하면 안됨)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRddA5%2Fbtq4H0nGtyH%2F7IDEsz1lCBH1GzHv0InE8k%2Fimg.png)

## 공개키 등록 & 복사

```
// 공개키 출력 (ssh-rsa 부터 이메일까지 복사)
cat ~/.ssh/id_rsa.pub

eval $(ssh-agent -s)
// ssh-add를 사용해 개인키를 ssh-agent에 등록함 (비밀번호 입력)
ssh-add ~/.ssh/id_rsa
```


![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJxTkr%2Fbtq4EtxEOJF%2FXedFUpWTQKjTwiKpiHhG41%2Fimg.png)

## github 에 공개키 등록

깃헙 설정에 들어가서 SSH and GPG keys 클릭하여 

new SSH key 를 클릭한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcmvA4f%2Fbtq4F18FjEs%2FUxAX31nUqc7D1Ld1SB0jnk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5at4r%2Fbtq4HHWbxKj%2FtxkRe5QG0TkjAlHB09uRAK%2Fimg.png)

Key 안에 복사했던 공개키를 붙여넣고, 타이틀 지정


