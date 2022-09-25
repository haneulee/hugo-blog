---
title: "Hugo 블로그 시작"
date: 2021-05-17T11:48:31+09:00
categories:
  - blog
  - hugo
tags:
  - development
  - front-end
  - hugo
  - blog
  - 휴고
  - 블로그
keywords:
  - development
  - front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
# coverImage: /img/post/hugo/github-repo.png
metaAlignment: center
coverMeta: out
---

<!--toc-->

{{< alert info >}}
[휴고 공식 문서](https://gohugo.io/about/what-is-hugo/)
{{< /alert >}}

# hugo 소개

Hugo는 Go로 작성된 빠르고 현대적인 정적 사이트 생성기이며 웹 사이트를 다시 재미있게 만들 수 있도록 설계되었습니다.
Hugo는 범용 웹 사이트 프레임 워크입니다. 기술적으로 말해서 Hugo는 정적 사이트 생성기 입니다. 방문자 요청마다 페이지를 동적으로 구축하는 시스템과 달리 Hugo는 콘텐츠를 생성하거나 업데이트 할 때 페이지를 구축합니다. 웹 사이트는 편집하는 것보다 훨씬 더 자주보기 때문에 Hugo는 웹 사이트의 최종 사용자에게 최적의보기 경험을 제공하고 웹 사이트 작성자에게 이상적인 글쓰기 경험을 제공하도록 설계되었습니다.

Hugo로 구축 된 웹 사이트는 매우 빠르고 안전합니다. Hugo 사이트는 Netlify , Heroku , GoDaddy , DreamHost , GitHub Pages , GitLab Pages , Surge , Aerobatic , Firebase , Google Cloud Storage , Amazon S3 , Rackspace , Azure 및 CloudFront를 포함하여 어디서나 호스팅 할 수 있으며 CDN과 잘 작동합니다. Hugo 사이트는 데이터베이스 나 Ruby, Python 또는 PHP와 같은 값 비싼 런타임에 대한 종속성없이 실행됩니다.

우리는 Hugo를 거의 즉각적인 빌드 시간을 가진 이상적인 웹 사이트 생성 도구로 생각하고 변경이있을 때마다 다시 빌드 할 수 있습니다.

**<장점>**

- go 언어 사용
- 빠른 빌드
- 정적 페이지 생성
- 다양한 테마
- 한국어 지원 부족
- 사용자 늘고 있는 추세

## hugo 설치

- Mac (맥) 환경에서 설치

```
brew install hugo
hugo version
hugo new site quickstart
```

## hugo 테마 적용

[휴고 테마 사이트](https://themes.gohugo.io/)

```
cd quickstart
git init
// 테마 폴더에 깃 서브모듈 적용
// 나는 tranquilpeak 테마가 마음에 들어서 적용
git submodule add https://github.com/haneulee/hugo-tranquilpeak-theme.git themes/tranquilpeak

// config.toml 파일에서 theme를 해당 테마 이름으로 변경
echo theme = \"tranquilpeak\" >> config.toml
```

## hugo 포스트

**포스트는 archetypes 폴더의 default.md 를 똑같이 복사하여 새로 생성한다.**

```
hugo new [포스트상위폴더]/[포스트 제목].md
// ex) hugo new post/blog/hugo-blog.md
```

## hugo 로컬 실행

- 아래 명령어를 실행하면 http://localhost:1313/ 에서 나의 블로그를 확인해볼 수 있다.

```
▶ hugo server -D

                   | EN
+------------------+----+
  Pages            | 10
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  3
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Total in 11 ms
Watching for changes in /Users/bep/quickstart/{content,data,layouts,static,themes}
Watching for config changes in /Users/bep/quickstart/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

## public 폴더에 호스팅할 레파지토리 추가

 <!--adsense-->

먼저 hugo 블로그를 [사용자 아이디].github.io 주소로 올리고 싶을 때는
깃헙 레파지토리를 2개 생성해야한다.

1. 휴고 블로그 - hugo-blog
2. 블로그 호스팅 - haneulee.github.io

아래 이름으로 2개 생성한 다음, 아까 만들었던 quickstart 루트 디렉토리에서
휴고 블로그를 리모트로 추가한다.

```
git remote add origin "[휴고 블로그 레파지토리 주소]"
```

다음은 hugo 명령어를 실행할 때 public 폴더에 빌드된 파일들이 생성되는데
public 폴더에 블로그 호스팅 깃 레파지토리를 submodule 로 추가해야 한다.
먼저 public 폴더에 파일이 있으면 다 비워주고 submodule 설정을 한다.

```
git submodule add -b master https://github.com/haneulee/haneulee.github.io.git public
```

## 배포

```
// public 폴더에 빌드된 파일들이 생성된다.
hugo -D
```

배포는 github action 으로 자동 배포 해도 되는데
배포 파일을 따로 만들어서 실행해보기로 했다.
일단 deploy.sh 파일을 루트 디렉토리에 만든다음
아래 내용을 저장한다. 내용은 아까 만들었던 2개의 레파지토리에 업데이트 내용을 다 반영하는 것!

```
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
# theme 폴더 하위 테마 이름
hugo -t tranquilpeak

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..


# blog 저장소 Commit & Push
git add .

msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

git push origin master

```

실행은 루트 디렉토리에서 ./deploy.sh 를 하면 성공
블로그 호스팅 레파지토리에서는 setting > pages 에 들어가서
branch를 master로 설정하고 save를 해야 한다.

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-repo.png)

오류 없이 배포되면
[사용자 아이디].github.io 주소로 나의 블로그를 확인할 수 있다.

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png)

## 다른 환경에서 다운로드

```
git clone https://github.com/[사용자 아이디]/[휴고 블로그 레파지토리 이름].git
git submodule update --init --recursive

```
