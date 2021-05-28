---
title: "NestJS 프레임워크"
date: 2021-05-21T10:23:15+09:00
categories: 
- development
- nestjs
tags: 
- development
- front-end
- nestjs
- fullstack
- nodejs
- npm
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://blog.kakaocdn.net/dn/dU9G4a/btqSKMKcVQr/MUn4YGbhr6gae83cSs6LCk/img.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

<!--toc-->

![](https://blog.kakaocdn.net/dn/dU9G4a/btqSKMKcVQr/MUn4YGbhr6gae83cSs6LCk/img.png)
## NestJS:

Nest (NestJS)는 효율적이고 확장 가능한[Node.js](https://nodejs.org/)서버 측 애플리케이션을 구축하기위한 프레임 워크입니다.프로그레시브 JavaScript를 사용하고[TypeScript](http://www.typescriptlang.org/)로 빌드되고 완전히 지원하며 (하지만 여전히 개발자가 순수 JavaScript로 코딩 할 수 있음) OOP (Object Oriented Programming), FP (Functional Programming) 및 FRP (Functional Reactive Programming) 요소를 결합합니다.

내부적으로 Nest는[Express](https://expressjs.com/)(기본값)와같은 강력한 HTTP 서버 프레임 워크를 사용하며 선택적으로 [Fastify](https://github.com/fastify/fastify)를 사용하도록 구성 할 수도 있습니다!

Nest는 이러한 일반적인 Node.js 프레임 워크 (Express / Fastify) 위에 추상화 수준을 제공하지만 API를 개발자에게 직접 노출합니다.이를 통해 개발자는 기본 플랫폼에서 사용할 수있는 수많은 타사 모듈을 자유롭게 사용할 수 있습니다.

```
npm install -g @nestjs/cli

nest --version

nest new blog-backend
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcMiXnd%2Fbtq3VhMnbBt%2FgkQzODtQMgfJcivYOSwZOK%2Fimg.png)

### nest 프로젝트 생성 시, npm 선택하기

mongoose : nestJS가 mongoDB를 사용하기 위한 패키지

```
// change directory
cd blog-backend

// install dependency
npm install --save @nestjs/mongoose mongoose

npm run start:dev

```

## Database 

### install MongoDB 

```
brew tap mongodb/brew

brew install mongodb-community@4.4

sudo mongod --dbpath=/Users/<user>/data/db

```

```
// blog-backend/src/app.module.ts

import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { MongooseModule } from '@nestjs/mongoose'; // add this
@Module({
  imports: [
    MongooseModule.forRoot('mongodb://localhost/nest-blog-project', { useNewUrlParser: true }),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

### 데이터베이스 스키마 & 인터페이스 생성

```
// /blog-backend/src/blog/dto/create-post.dto.ts

export class CreatePostDTO {
  readonly title: string;
  readonly description: string;
  readonly body: string;
  readonly author: string;
  readonly date_posted: string;
}
```

### nestJS DTO & 모듈 생성

```
nest generate module blog
```

### nestJS 서비스 & 컨트롤러 생성

```
nest generate service blog

nest generate controller blog
```

#### 컨트롤러 :

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvVU7h%2Fbtq3YMx8KTb%2FoN9KqyWXCyJSYkzj1cs4b1%2Fimg.png)

참고 :

[docs.nestjs.com/](https://docs.nestjs.com/)

[becomereal.tistory.com/56?category=1093528](https://becomereal.tistory.com/56?category=1093528)



{{< adsense >}}