---
title: "NestJS 프레임워크 - Decorator"
date: 2021-07-15T10:15:13+09:00
categories:
  - development
tags:
  - development
  - front-end
  - nestjs
  - fullstack
  - nodejs
  - npm
  - decorator
  - guard
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/nestjs/img-1.png
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

# NestJS 프레임워크 - Decorator

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/nestjs/img-1.png)

{{< alert info >}}
NestJS는 ES7(혹은 타입 스크립트)에 새로 추가된 @ 데코레이터(Decorator)를 주로 이용한다.
{{< /alert >}}

---

## @Role 데코레이터

SetMetadata는 localstorage 처럼 metadata를 key/value로 저장 해줍니다.  
'roles'라는 key에 roles라는 변수를 값으로 metadata에 저장을 해 놓아서 어디서든 꺼내볼 수 있습니다.  
물론 우리는 AuthGuard에서 꺼내봅니다.

RoleType은 keyof typeof로 지정 해 놓을 수 있습니다.  
keyof 연산자는 피연산자의 키타입에 해당하는 타입을 리턴해줍니다.  
이를테면, let person: Person { name: 'Jarid', age: 35} 라는 오브젝트에서 let personProp: keyof Person;으로 정의하면 personProp이 가질 수 있는 값은 Person의 key 값이 ”name”|”age”가 됩니다.

먼저 **Union of literal types**이라는 개념을 이해하면 좋은데,
type Greeting = 'Hello';  
에서 Greeting 타입은 'Hello' 하나만 가능하지만,

type Greeting = 'Hello'|'Hi'|'Welcome';  
에서 Greeting 타입은 'Hello', 'Hi', 'Welcome' 이 세가지 값을 가질 수 있습니다.

enum에서도 union of literal types를 이용할 수 있습니다.  
enum을 union of literal types로 만들기 위해 사용하는 것이 **keyof typeof** 입니다.  
아래에서는 추가적으로 'Any'타입까지 추가시켰으므로, keyof typeof UserRole | 'Any'로 사용한 것입니다.

```ts
import { UserRole } from "src/users/entities/user.entity";
import { SetMetadata } from "@nestjs/common";

export type AllowedRoles = keyof typeof UserRole | "Any";

export const Role = (roles: AllowedRoles[]) => SetMetadata("roles", roles);
```

## APP_GUARD

```ts
import { Module } from "@nestjs/common";
import { APP_GUARD } from "@nestjs/core";
import { AuthGuard } from "./auth.guard";

@Module({
  providers: [
    {
      provide: APP_GUARD,
      useClass: AuthGuard,
    },
  ],
})
export class AuthModule {}
```

@Role 데코레이터와 @UseGuards ([AuthGuard](https://docs.nestjs.com/security/authentication#enable-authentication-globally)) 를 같이 사용하는것은 좋지 않다.  
그래서 nestjs 에서 제공해주는 APP_GUARD 상수를 이용해서 UseGuards 사용을 줄일 수 있습니다.  
위와 같이 auth 모듈 설정을 해주면, 더이상 UseGuard는 사용하지 않으셔도 됩니다  
대신에 Auth module을 App 모듈에서 꼭 import 해주셔야 합니다.

<!--adsense-->

## AuthGuard

SetMetadata로 넘겨준 'roles'라는 키를 가진 metadata를 AuthGuard가 작동할 때 값을 가져와서 role이 어떤지 확인 해야 합니다.  
constructor에 보면 어김없이 나오는 parameter properties가 보입니다.

reflector라는 property가 Reflector 클래스 타입으로 설정되었습니다.  
this.reflector.get<AllowedRoles> 에서 SetMetadata로 넘겨준 'roles' 키에 해당하는 값을 얻어올 수 있습니다.

Role을 설정 안해주면 public resolver로 취급할 수 있다는 의미입니다.  
[https://developer.mozilla.org/ko/docs/Glossary/Falsy](https://developer.mozilla.org/ko/docs/Glossary/Falsy)

Role 값들을 얻어 오려면 메타데이터를 설정을 해줘야 하는데, 앞에 코드처럼 우리는 @Role 데코레이터를 이용하여 설정하기로 했습니다.  
사용을 할 때 원하는 resolver 위에 사용해주면 됩니다.

```ts
import { CanActivate, ExecutionContext, Injectable } from "@nestjs/common";
import { GqlExecutionContext } from "@nestjs/graphql";
import { Reflector } from "@nestjs/core";
import { AllowedRoles } from "./role.decorator";
import { User } from "src/users/entities/user.entity";

@Injectable()
export class AuthGuard implements CanActivate {
  constructor(private readonly reflector: Reflector) {}

  canActivate(context: ExecutionContext) {
    const roles = this.reflector.get<AllowedRoles>(
      "roles",
      context.getHandler()
    );
    if (!roles) {
      return true;
    }
    const gqlContext = GqlExecutionContext.create(context).getContext();
    const user: User = gqlContext["user"];
    if (!user) {
      return false;
    }
    if (roles.includes("Any")) {
      return true;
    }
    return roles.includes(user.role);
  }
}
```

## Resolver 에서 @Role 데코레이터 사용

getAllPodcasts에는 @Role 이 없는데, createPodcast에는 @Role 이 있습니다.  
전자는 Role이 없으므로, 우리의 AuthGuard 코드에 보면, true를 리턴하게 되므로 public한 resolver로 볼 수 있습니다.  
로그인하지 않아도 팟캐스트들을 검색할 수 있습니다.

반면에 createPodcast를 보면 Role이 있는데 'Host'여야 한다는 의미로 AuthGuard에서 처리 해줄 수 있습니다.  
로그인 하지 않거나 Listener인 유저에게 Forbidden Resource 에러가 발생하게 됩니다.

```ts
 @Query((returns) => GetAllPodcastsOutput)
  getAllPodcasts(): Promise<GetAllPodcastsOutput> {
    return this.podcastsService.getAllPodcasts();
  }

  @Mutation((returns) => CreatePodcastOutput)
  @Role(["Host"])
  createPodcast(
    @Args("input") createPodcastInput: CreatePodcastInput
  ): Promise<CreatePodcastOutput> {
    return this.podcastsService.createPodcast(createPodcastInput);
  }
```

---

참고 :
[https://docs.nestjs.com/guards](https://docs.nestjs.com/guards)
