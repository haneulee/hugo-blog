---
title: "Typeorm study 2 - Hash / JWT / Guard"
date: 2021-07-08T10:21:03+09:00
categories:
  - development
tags:
  - development
  - front-end
  - typeorm
  - nestjs
  - graphql
  - typescript
  - bcrypt
  - hash
  - jwt
  - guard
  - token
  - enum
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/typeorm/img-1.png
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

{{< adsense >}}

# Typeorm study 2 - Hash / JWT / Guard

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/typeorm/img-1.png)

## Enum Type (enumerated type)

Enum Type은 값을 지정하여 하나의 상수처럼 사용할 수 있다.
sqlite 디비에서는 enum type을 지원하지 않는다는 오류가 발생하는데
아래 코드처럼 @Column 데코레이터에 type을 'enum' 이 아니라 'simple-enum'으로 지정해주면 해결된다.

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/typeorm/img-2.png)

```ts
export enum UserRole {
  Host = 'Host',
  Listener = 'Listener',
}

registerEnumType(UserRole, { name: 'UserRole' });


@Column({ type: 'simple-enum', enum: UserRole })
  @Field(type => UserRole)
  role: UserRole;
```

[registerEnumType](https://docs.nestjs.com/graphql/unions-and-enums#code-first-1) 함수를 사용해 enum type을 등록해준다.

## password hash 처리

typeorm 에는 @BeforeInsert , @BeforeUpdate 데코레이터들이 저장 또는 변경되기 전에 패스워드를 hash 처리할 수 있다.
[bcrypt](https://www.npmjs.com/package/bcrypt) 패키지를 사용하여 hash 해준다.

```ts
    @BeforeInsert()
    @BeforeUpdate()
    async hashPassword(): Promise<void> {
        if (!this.password) {
            return;
        }
        try {
            this.password = await bcrypt.hash(this.password, 10);
        } catch (error) {
            console.log(error);
            throw new InternalServerErrorException();
        }
    }
```

## jwt 처리

```ts
@Module({})
@Global()
export class JwtModule {
  static forRoot(options: JwtModuleOptions): DynamicModule {
    return {
      module: JwtModule,
      providers: [
        {
          provide: CONFIG_OPTIONS,
          useValue: options,
        },
        JwtService,
      ],
      exports: [JwtService],
    };
  }
}
```

jforRoot method를 정의하는데 앞에 static으로 지정되어 있다.
이는 클래스 인스턴스를 만들지 않아도 JwtModule.forRoot() 이런식으로 사용할 수 있게끔 해주는 접근 제어자이다.

이렇게 정의한 custom value provider는 service 파일에서 이렇게 사용한다.

- constructor( **@Inject** (CONFIG_OPTIONS) private readonly options: JwtModuleOptions) {}

@Global 데코레이터는 import 하면 전역적으로 어디서든 사용할 수 있다.

```ts
@Injectable()
export class JwtMiddleware implements NestMiddleware {
  constructor(
    private readonly jwtService: JwtService,
    private readonly usersService: UsersService
  ) {}

  async use(req: Request, res: Response, next: NextFunction) {
    if ("x-jwt" in req.headers) {
      const token = req.headers["x-jwt"];
      try {
        const decoded = this.jwtService.verify(token.toString());
        if (typeof decoded === "object" && decoded.hasOwnProperty("id")) {
          const { user, ok } = await this.usersService.findById(decoded["id"]);
          if (ok) {
            req["user"] = user;
          }
        }
      } catch (error) {}
    }
    next();
  }
}
```

middleware에서 service를 사용하기 위해 constructor에서 parameter properties를 사용한다.
이렇게 생성한 middleware 아래와 같이 appModule에 추가해주면 된다.
참고: [Applying Middleware](https://docs.nestjs.com/middleware#applying-middleware)

```ts
export class AppModule {
  configure(consumer: MiddlewareConsumer) {
    consumer.apply(JwtMiddleware).forRoutes({
      path: "/graphql",
      method: RequestMethod.POST,
    });
  }
}
```

## 로그인 파트

```ts
const passwordCorrect = await user.checkPassword(password);
if (!passwordCorrect) {
  return {
    ok: false,
    error: "Wrong password",
  };
}

const token = this.jwtService.sign(user.id);
```

user의 checkPassword 메소드를 이용해서 우리가 입력한 패스워드와 hashing 시켜 놓은 password가 일치하는지 확인하는 로직이다.
그 다음에 const token = this.jwtService.sign(user.id)라는 코드로 우리의 user.id를 json web token으로 만든다.
생성된 토큰은 아래 사이트에서 확인해 볼 수 있다.

- 토큰 테스트 사이트 : [token.io](https://jwt.io/#debugger)

## [Guard](https://docs.nestjs.com/guards#guards)

nestjs 에서는 유저 인증, 권한부여를 위해서 guard라는 개념을 사용합니다.

```ts
@Injectable()
export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext) {
    const gqlContext = GqlExecutionContext.create(context).getContext();
    const user = gqlContext["user"];
    if (!user) {
      return false;
    }
    return true;
  }
}
```

graphql의 context에는 유저 인증 정보가 들어가 있습니다.
context에 user 정보를 넘겨주려면, graphql 모듈을 app 모듈에서 import 하는 단계에서 설정을 해줘야 합니다.

```ts
GraphQLModule.forRoot({
      autoSchemaFile: true,
      context: ({ req }) => {
        return { user: req['user'] };
      },
    }),
```

위에서 만든 AuthGuard는 @UseGuards 데코레이터를 이용하여 사용할 수 있습니다.

```ts
    @UseGuards(AuthGuard)
    @Query(returns => UserProfileOutput)
    seeProfile(
        @Args() userProfileInput: UserProfileInput,
    ): Promise<UserProfileOutput> {
        return this.usersService.findById(userProfileInput.userId);
    }
```

resolver위에 @UseGuards 데코레이터를 이용하면 유저 인증이 완성이 됩니다.
로그인 하지 않은 채로, 즉 로그인 토큰을 헤더에 제공하지 않은 상태로 해당 resolver를 사용하면 Forbidden Resource 에러가 발생하게 됩니다.

## 로그인 유저 정보 획득

```ts
export const AuthUser = createParamDecorator(
  (data: unknown, context: ExecutionContext) => {
    const gqlContext = GqlExecutionContext.create(context).getContext();
    const user = gqlContext["user"];
    return user;
  }
);
```

createParamDecorator는 context에서 user 정보를 리턴해주는 역할을 하는 데코레이터입니다.
사용방법은 me( **@AuthUser** () authUser: User): User 이런 식으로 사용할 수 있습니다.

참고 :
[nestJS](https://docs.nestjs.com/)
