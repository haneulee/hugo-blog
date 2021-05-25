---
title: "disqus 에서 utterances로 변경 - hugo 블로그 댓글 추가하기 ✨💬✨"
date: 2021-05-25T14:36:24+09:00
categories: 
- development
- blog
tags: 
- development
- front-end
- blog
- utterances
- disqus
- comment
- 블로그
- 댓글
- 광고
- hugo
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/img-7.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

<!--toc-->


# disqus에서 utterances로 변경하기

hugo를 사용하여 블로그를 만든 뒤, 
댓글 기능을 disqus를 사용하여 만들었는데 몇일 뒤에 보니 
댓글 부분에 여러 광고가 다닥다닥 붙어 있었다.......
무료 라이센스로 사용하는 경우 광고가 붙는다고 되어 있음 ㅠ

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/img-1.png)

구글 애드센스 광고만해도 많을텐데 댓글까지 광고가 있으면 
너무 많을 것 같았다. 또한, 검색해보니 disqus는 무겁다는 의견이 상당히 많았다. 

따라서 disqus를 제거하고, 
개발자들이 많이 사용하는 utterances를 달아보기로 하였다. 

utterances는 아주 재미있는 프로젝트인데 GitHub의 이슈 검색 API를 사용해서 해당 글과 연결된 이슈가 없으면 새로 만들고 이미 있으면 기존의 이슈를 사용한다. 
그리고 해당 이슈에 달리는 댓글을 Primer를 이용해서 GitHub과 유사한 UI로 댓글을 보여준다.

## 깃헙에 블로그 댓글 레파지토리 생성
나는 blog-comment 이름으로 새로 레파지토리를 생성하였다. 


## 댓글 기능 사용할 레파지토리 선택

[https://utteranc.es/](https://utteranc.es/)에 접속하여 configuration 부분에 있는
 utterances app 를 클릭하고 install 한 다음, 댓글 기능을 사용할 레파지토리를 선택한다. 
 나의 경우, blog-comment 로 선택했음

***configuration***

```
Repository
Choose the repository utterances will connect to.

Make sure the repo is public, otherwise your readers will not be able to view the issues/comments.
Make sure the utterances app is installed on the repo, otherwise users will not be able to post comments.
If your repo is a fork, navigate to its settings tab and confirm the issues feature is turned on.

repo:
owner/repo
A public GitHub repository. This is where the blog post issues and issue-comments will be posted.
```

## script 파일 만들기
다시 [https://utteranc.es/](https://utteranc.es/)에 접속하여
***Blog Post ↔️ Issue Mapping*** 섹션에서 원하는 것을 선택한다. 

Issue Label은 댓글로 생성된 이슈에 label을 달지, 단다면 어떤 label을 달지 선택하는 것입니다. 저는 comment로 작성했습니다.
Theme을 선택합니다. 저는 default 옵션을 사용했습니다. label은 이모티콘으로 생성 (✨💬✨)
하단에 생성된 코드를 복사합니다.

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/img-2.png)
![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/img-3.png)

## 댓글 script 추가
다음은 hugo theme에 맞게 해당 script를 적절한 위치에 삽입하면 된다. 
나의 경우 theme 폴더 내의 layouts/partials/post/utterances.html 를 만들고 아래처럼 추가해주었다. 

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/img-4.png)

```
<div style="margin-top:200px;">
    <script src="https://utteranc.es/client.js"
        repo="haneulee/blog-comment"
        issue-term="pathname"
        label="✨💬✨"
        theme="github-dark"
        crossorigin="anonymous"
        async>
    </script>
</div>

```

그리고 post 하위 부분에 해당 html을 추가해주었고,

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/img-5.png)

테마 자체에 disqus 설정 부분이 있었는데 이는 config.toml 에서 주석처리 해주었다. 

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/img-6.png)

로컬 서버를 돌려보니 아래와 같이 이쁘게 댓글 기능이 추가되었다!!

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/blog/img-7.png)

