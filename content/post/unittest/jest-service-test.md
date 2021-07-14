---
title: "NestJS 에서 UNIT TEST 🏃🏻‍♀️"
date: 2021-07-12T10:30:49+09:00
categories:
  - development
tags:
  - development
  - front-end
  - unittest
  - jest
  - javascript
  - facebook
  - react
  - nextjs
  - 테스트주도개발
  - 제스트
  - TDD
  - 페이스북
  - 단위테스트
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-jest.png
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

# Jest

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-jest.png)

## NestJS 에서 UNIT TEST 🏃🏻‍♀️

### jwt.service.spec.ts

```ts
describe('JwtService', () => {
  let service: JwtService;

  beforeAll(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [
        JwtService,
        { provide: CONFIG_OPTIONS, useValue: jwtOptions },
      ],
    }).compile();
    service = module.get<JwtService>(JwtService);
  });

```

jwt service 는 jsonwebtoken 패키지 이외에는 달리 mocking 할 것이 없다.
</br>
jwt service가 제대로 준비 되었는지 확인하려면
</br>
{{< hl-text yellow >}}
it('should be defined',()=>{ expect(service).toBeDefined();});
{{< /hl-text >}}
</br>
이 코드로 확인해볼 수 있다.

```ts
jest.mock("jsonwebtoken", () => ({
  sign: jest.fn(() => MOCKED_TOKEN),
  verify: jest.fn(() => ({ id: TEST_ID })),
}));

describe("Test sign method", () => {
  it("should return MOCKED_TOKEN", () => {
    const token = service.sign(TEST_ID);

    expect(jwt.sign).toHaveBeenCalledTimes(1);
    expect(jwt.sign).toHaveBeenCalledWith({ id: TEST_ID }, TEST_PRIVATE);
    expect(token).toEqual(MOCKED_TOKEN);
    expect(typeof token).toEqual("string");
  });
});
```

jest.mock('jsonwebtoken', () => ...) 이 블럭은 jsonwebtoken 패키지를 mocking하는 것이다.
</br>
유닛테스트이기 때문에 jwt service 자체에만 집중해야 하기 때문에 이러한 영향을 줄 수 있는 패키지나 함수, 클래스들은 mocking하여 테스트의 도구로 이용한다.
</br>
밑에 expect(jwt.sign).toHaveBeenCalledTimes(1);은 jwt.sign이 단 한 번 호출 되는지 테스트로 확인하는 것이다.
</br>
expect와 실제와 다르면 테스트는 실패한다.
</br>
describe, it 을 적절히 잘 사용하면 테스트 코드 가독성이 높아진다. describe는 테스트할 대상에 대해 설명한다.
</br>
it(individual test), 그 대상을 개별적으로 테스트 하는 것을 의미한다.

### users.service.spec.ts

```ts
describe('UsersService', () => {
  let service: UsersService;
  let jwtService: JwtService;
  let userRepository: MockRepository<User>;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [
        UsersService,
        {
          provide: getRepositoryToken(User),
          useValue: mockRepository(),
        },
        {
          provide: JwtService,
          useValue: mockJwtService,
        },
      ],
    }).compile();

    service = module.get<UsersService>(UsersService);
    userRepository = module.get(getRepositoryToken(User));
    jwtService = module.get<JwtService>(JwtService);
  });
```

먼저 user service만 테스트해야 하는데, repository도 연결되어 있고, user 로그인 처리할 때 사용하는 jwt service도 연결되어 있습니다. user service에 집중해야 하는 단위 테스트이므로, 이것들은 mocking을 해야 합니다. jwtService는 jwt.service와 마찬가지로 여기서도 다시 mocking을 해주고, repository는 약간 생소하지만 위의 코드와 같이 설정을 해줍니다.

</br></br>
코드를 보시면 jwt.service.spec.ts와는 달리 users.service.spec.ts에서는 beforeAll이 아니라 [beforeEach](https://jestjs.io/docs/setup-teardown)로 모듈을 초기화했습니다.
</br></br>
이 둘의 차이는 뭘까요?
</br></br>
테스트를 진행하기 전에 앞의 jwt 테스트에서 한 것처럼 세팅이 필요합니다. 세팅을 매 테스트마다 할 것인지 또는 전체 테스트에서 한 번만해도 되는지의 차이입니다.
</br></br>
예를 들어, mocking한 respository 같은 경우에는 createAccount 테스트에도 사용할 수가 있고, seeProfile, editProfile 테스트하는 경우에도 모두 사용가능한데, 매번 사용횟수나 들어 간 변수들을 초기화하지 않으면 테스트가 꼬일 수 밖에 없습니다. 그래서 user.service를 테스트할 때에는 beforeAll이 아니라 beforeEach가 되는 것입니다.
</br></br>

{{< adsense >}}

```ts
async createAccount({
    email,
    password,
    role,
  }: CreateAccountInput): Promise<CreateAccountOutput> {
    try {
      const exists = await this.users.findOne({ email });
      // test 1
      if (exists) {
        return { ok: false, error: `There is a user with that email already` };
      }
      const user = this.users.create({
        email,
        password,
        role,
      });
      await this.users.save(user);

      // test 2
      return {
        ok: true,
        error: null,
      };
    } catch {
        // test 3
      return {
        ok: false,
        error: 'Could not create account',
      };
    }
  }
```

</br></br>
1의 경우 - 이미 존재하는 이메일이 있을 경우에는 creatAccount가 실패해야 합니다.
</br>
2의 경우 - 정상적으로 계정이 만들어져야 하는 경우입니다.
</br>
3의 경우 - findOne이나 save 메소드에서 에러가 발생하여 catch로 넘어가는 경우입니다.
</br></br>
위의 createAccount에서는 위의 logic들을 판단해야만 코드 모든 부분들을 테스트 하는 것으로 볼 수 있습니다.
그래서 테스트는
</br></br>

```ts
it('should success to create User', async () => { ...
it('should fail because of user existing', async () => { ...
it('should fail because of saving failed', async () => { ...
```

</br>
이렇게 세 가지 로직으로 테스트를 할 수 있습니다.
그러면 createAccount에 대한 test coverage가 전부 채워집니다.
</br></br>
위의 it(individual test) 코드를 조금더 살펴 보면 테스트가 어떤 식으로 진행이 되어야 하는지 감을 잡을 수 있습니다.

> it('should success to create user', ...

</br>
createAccount를 호출해서 성공적으로 계정 만드는 것을 테스트 하는 것입니다.
service의 로직만 테스트하는 것이므로 respository는 흉내내기를 해야 합니다.
users.service.spec.ts 상단 코드에 보면 이미 userRepository를 흉내내고 설정을 해놨습니다.
beforeEach를 통해서 매 테스트마다 초기화가 되기 때문에 걱정하지 않고 테스트 안에서 리턴 값을 흉내낼 수 있습니다.
</br></br>

> userRepository.findOne.mockResolvedValueOnce(null);

</br>
user repository의 findOne값을 흉내낸 것입니다.
mockResolvedValue는 Promise를 리턴합니다. Promise의 resolve값이 null이라는 뜻이 되겠습니다. 실제 db라면 db 연결이나 상태에 따라 값을 리턴 못할 수도 있고 연결이 안될 수도 있기 때문에 유닛 테스트라는 의미가 살지 않기 때문에 어떤 경우라도 db와는 관계 없이 null 값을 resolve로 넘겨준다는 뜻이 됩니다.
</br></br>

> userRepository.create.mockReturnValueOnce(hostArgs);

</br>

create는 typeorm repository에서 Promise로 리턴을 하는 것이 아니라, 엔티티 객체를 리턴해줍니다. 세이브 되기 이전 값입니다. 그래서 create는 resolve 값을 리턴하는 것이 아닙니다. 그냥 객체를 리턴해주기 때문에 위와 같이 설정을 해주면 되겠습니다.

</br></br>

> userRepository.save.mockResolvedValue(TEST_HOST);

findOne과 마찬가지로 resolve 값을 리턴해줍니다. 성공적으로 만들어진 경우이므로 db에 성공적으로 저장된 값을 리턴하는 repository의 save 메소드를 흉내낸 것입니다.

</br></br>

```ts
describe("createAccount Testing", () => {
  it("should success to create User", async () => {
    userRepository.findOne.mockResolvedValueOnce(null);
    userRepository.create.mockReturnValueOnce(hostArgs);
    userRepository.save.mockResolvedValue(TEST_HOST);

    const result = await service.createAccount(hostArgs);

    expect(userRepository.findOne).toHaveBeenCalledTimes(1);
    expect(userRepository.findOne).toHaveBeenCalledWith({
      email: hostArgs.email,
    });
    expect(userRepository.create).toHaveBeenCalledTimes(1);
    expect(userRepository.create).toHaveBeenCalledWith(hostArgs);
    expect(userRepository.save).toHaveBeenCalledTimes(1);
    expect(userRepository.save).toHaveBeenCalledWith(hostArgs);
    expect(result).toMatchObject({ ok: true, error: null });
  });
});
```

createAccount가 호출되었습니다. 우리가 설정해 놓은 값에 의하면 위 코드는 findOne을 호출해서 이미 존재하는 이메일 계정이 없음을 확인하고 create 메소드를 호출해서 entity를 만들고, save 메소드를 호출해서 db에 엔티티를 저장하는 로직으로 흘러 갈 것입니다.
우리가 만든 createAccount가 위의 로직대로 흘러간다고 기대하였으므로, 실제로 그렇게 호출이 되었나 확인만 해주면 테스트를 성공적으로 한 것입니다.
</br></br>
위의 로직대로 findOne이 호출되었는가(toHaveBeenCalledTimes), 파라미터는 제대로 입력 되었는가(toHaveBeenCalledWith), create는 제대로 호출되었는가, save는 제대로 호출되었고, 결과가 우리가 원하는 값(toMatchObject)이 나오는가?를 jest에서 판단을 해주기 때문에 createAccount가 정상적으로 작동하는 경우 테스트가 끝난 것입니다.
</br></br>
createAccount를 모두 테스트하려면, 앞에서 언급드린 대로, 이미 이메일 계정이 이미 있는 경우와, save 메소드가 실패할 경우를 모두 테스트해야 full coverage를 완성할 수 있습니다.
</br>

참고 :
[jset 공식문서](https://jestjs.io/docs/api),
[jset mocking](https://www.daleseo.com/jest-fn-spy-on/),
