---
title: "NestJS μμ UNIT TEST ππ»ββοΈ"
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
  - νμ€νΈμ£Όλκ°λ°
  - μ μ€νΈ
  - TDD
  - νμ΄μ€λΆ
  - λ¨μνμ€νΈ
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

## NestJS μμ UNIT TEST ππ»ββοΈ

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

jwt service λ jsonwebtoken ν¨ν€μ§ μ΄μΈμλ λ¬λ¦¬ mocking ν  κ²μ΄ μλ€.
</br>
jwt serviceκ° μ λλ‘ μ€λΉ λμλμ§ νμΈνλ €λ©΄
</br>
{{< hl-text yellow >}}
it('should be defined',()=>{ expect(service).toBeDefined();});
{{< /hl-text >}}
</br>
μ΄ μ½λλ‘ νμΈν΄λ³Ό μ μλ€.

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

jest.mock('jsonwebtoken', () => ...) μ΄ λΈλ­μ jsonwebtoken ν¨ν€μ§λ₯Ό mockingνλ κ²μ΄λ€.
</br>
μ λνμ€νΈμ΄κΈ° λλ¬Έμ jwt service μμ²΄μλ§ μ§μ€ν΄μΌ νκΈ° λλ¬Έμ μ΄λ¬ν μν₯μ μ€ μ μλ ν¨ν€μ§λ ν¨μ, ν΄λμ€λ€μ mockingνμ¬ νμ€νΈμ λκ΅¬λ‘ μ΄μ©νλ€.
</br>
λ°μ expect(jwt.sign).toHaveBeenCalledTimes(1);μ jwt.signμ΄ λ¨ ν λ² νΈμΆ λλμ§ νμ€νΈλ‘ νμΈνλ κ²μ΄λ€.
</br>
expectμ μ€μ μ λ€λ₯΄λ©΄ νμ€νΈλ μ€ν¨νλ€.
</br>
describe, it μ μ μ ν μ μ¬μ©νλ©΄ νμ€νΈ μ½λ κ°λμ±μ΄ λμμ§λ€. describeλ νμ€νΈν  λμμ λν΄ μ€λͺνλ€.
</br>
it(individual test), κ·Έ λμμ κ°λ³μ μΌλ‘ νμ€νΈ νλ κ²μ μλ―Ένλ€.

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

λ¨Όμ  user serviceλ§ νμ€νΈν΄μΌ νλλ°, repositoryλ μ°κ²°λμ΄ μκ³ , user λ‘κ·ΈμΈ μ²λ¦¬ν  λ μ¬μ©νλ jwt serviceλ μ°κ²°λμ΄ μμ΅λλ€. user serviceμ μ§μ€ν΄μΌ νλ λ¨μ νμ€νΈμ΄λ―λ‘, μ΄κ²λ€μ mockingμ ν΄μΌ ν©λλ€. jwtServiceλ jwt.serviceμ λ§μ°¬κ°μ§λ‘ μ¬κΈ°μλ λ€μ mockingμ ν΄μ£Όκ³ , repositoryλ μ½κ° μμνμ§λ§ μμ μ½λμ κ°μ΄ μ€μ μ ν΄μ€λλ€.

</br></br>
μ½λλ₯Ό λ³΄μλ©΄ jwt.service.spec.tsμλ λ¬λ¦¬ users.service.spec.tsμμλ beforeAllμ΄ μλλΌ [beforeEach](https://jestjs.io/docs/setup-teardown)λ‘ λͺ¨λμ μ΄κΈ°ννμ΅λλ€.
</br></br>
μ΄ λμ μ°¨μ΄λ λ­κΉμ?
</br></br>
νμ€νΈλ₯Ό μ§ννκΈ° μ μ μμ jwt νμ€νΈμμ ν κ²μ²λΌ μΈνμ΄ νμν©λλ€. μΈνμ λ§€ νμ€νΈλ§λ€ ν  κ²μΈμ§ λλ μ μ²΄ νμ€νΈμμ ν λ²λ§ν΄λ λλμ§μ μ°¨μ΄μλλ€.
</br></br>
μλ₯Ό λ€μ΄, mockingν respository κ°μ κ²½μ°μλ createAccount νμ€νΈμλ μ¬μ©ν  μκ° μκ³ , seeProfile, editProfile νμ€νΈνλ κ²½μ°μλ λͺ¨λ μ¬μ©κ°λ₯νλ°, λ§€λ² μ¬μ©νμλ λ€μ΄ κ° λ³μλ€μ μ΄κΈ°ννμ§ μμΌλ©΄ νμ€νΈκ° κΌ¬μΌ μ λ°μ μμ΅λλ€. κ·Έλμ user.serviceλ₯Ό νμ€νΈν  λμλ beforeAllμ΄ μλλΌ beforeEachκ° λλ κ²μλλ€.
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
1μ κ²½μ° - μ΄λ―Έ μ‘΄μ¬νλ μ΄λ©μΌμ΄ μμ κ²½μ°μλ creatAccountκ° μ€ν¨ν΄μΌ ν©λλ€.
</br>
2μ κ²½μ° - μ μμ μΌλ‘ κ³μ μ΄ λ§λ€μ΄μ ΈμΌ νλ κ²½μ°μλλ€.
</br>
3μ κ²½μ° - findOneμ΄λ save λ©μλμμ μλ¬κ° λ°μνμ¬ catchλ‘ λμ΄κ°λ κ²½μ°μλλ€.
</br></br>
μμ createAccountμμλ μμ logicλ€μ νλ¨ν΄μΌλ§ μ½λ λͺ¨λ  λΆλΆλ€μ νμ€νΈ νλ κ²μΌλ‘ λ³Ό μ μμ΅λλ€.
κ·Έλμ νμ€νΈλ
</br></br>

```ts
it('should success to create User', async () => { ...
it('should fail because of user existing', async () => { ...
it('should fail because of saving failed', async () => { ...
```

</br>
μ΄λ κ² μΈ κ°μ§ λ‘μ§μΌλ‘ νμ€νΈλ₯Ό ν  μ μμ΅λλ€.
κ·Έλ¬λ©΄ createAccountμ λν test coverageκ° μ λΆ μ±μμ§λλ€.
</br></br>
μμ it(individual test) μ½λλ₯Ό μ‘°κΈλ μ΄ν΄ λ³΄λ©΄ νμ€νΈκ° μ΄λ€ μμΌλ‘ μ§νμ΄ λμ΄μΌ νλμ§ κ°μ μ‘μ μ μμ΅λλ€.

> it('should success to create user', ...

</br>
createAccountλ₯Ό νΈμΆν΄μ μ±κ³΅μ μΌλ‘ κ³μ  λ§λλ κ²μ νμ€νΈ νλ κ²μλλ€.
serviceμ λ‘μ§λ§ νμ€νΈνλ κ²μ΄λ―λ‘ respositoryλ νλ΄λ΄κΈ°λ₯Ό ν΄μΌ ν©λλ€.
users.service.spec.ts μλ¨ μ½λμ λ³΄λ©΄ μ΄λ―Έ userRepositoryλ₯Ό νλ΄λ΄κ³  μ€μ μ ν΄λ¨μ΅λλ€.
beforeEachλ₯Ό ν΅ν΄μ λ§€ νμ€νΈλ§λ€ μ΄κΈ°νκ° λκΈ° λλ¬Έμ κ±±μ νμ§ μκ³  νμ€νΈ μμμ λ¦¬ν΄ κ°μ νλ΄λΌ μ μμ΅λλ€.
</br></br>

> userRepository.findOne.mockResolvedValueOnce(null);

</br>
user repositoryμ findOneκ°μ νλ΄λΈ κ²μλλ€.
mockResolvedValueλ Promiseλ₯Ό λ¦¬ν΄ν©λλ€. Promiseμ resolveκ°μ΄ nullμ΄λΌλ λ»μ΄ λκ² μ΅λλ€. μ€μ  dbλΌλ©΄ db μ°κ²°μ΄λ μνμ λ°λΌ κ°μ λ¦¬ν΄ λͺ»ν  μλ μκ³  μ°κ²°μ΄ μλ  μλ μκΈ° λλ¬Έμ μ λ νμ€νΈλΌλ μλ―Έκ° μ΄μ§ μκΈ° λλ¬Έμ μ΄λ€ κ²½μ°λΌλ dbμλ κ΄κ³ μμ΄ null κ°μ resolveλ‘ λκ²¨μ€λ€λ λ»μ΄ λ©λλ€.
</br></br>

> userRepository.create.mockReturnValueOnce(hostArgs);

</br>

createλ typeorm repositoryμμ Promiseλ‘ λ¦¬ν΄μ νλ κ²μ΄ μλλΌ, μν°ν° κ°μ²΄λ₯Ό λ¦¬ν΄ν΄μ€λλ€. μΈμ΄λΈ λκΈ° μ΄μ  κ°μλλ€. κ·Έλμ createλ resolve κ°μ λ¦¬ν΄νλ κ²μ΄ μλλλ€. κ·Έλ₯ κ°μ²΄λ₯Ό λ¦¬ν΄ν΄μ£ΌκΈ° λλ¬Έμ μμ κ°μ΄ μ€μ μ ν΄μ£Όλ©΄ λκ² μ΅λλ€.

</br></br>

> userRepository.save.mockResolvedValue(TEST_HOST);

findOneκ³Ό λ§μ°¬κ°μ§λ‘ resolve κ°μ λ¦¬ν΄ν΄μ€λλ€. μ±κ³΅μ μΌλ‘ λ§λ€μ΄μ§ κ²½μ°μ΄λ―λ‘ dbμ μ±κ³΅μ μΌλ‘ μ μ₯λ κ°μ λ¦¬ν΄νλ repositoryμ save λ©μλλ₯Ό νλ΄λΈ κ²μλλ€.

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

createAccountκ° νΈμΆλμμ΅λλ€. μ°λ¦¬κ° μ€μ ν΄ λμ κ°μ μνλ©΄ μ μ½λλ findOneμ νΈμΆν΄μ μ΄λ―Έ μ‘΄μ¬νλ μ΄λ©μΌ κ³μ μ΄ μμμ νμΈνκ³  create λ©μλλ₯Ό νΈμΆν΄μ entityλ₯Ό λ§λ€κ³ , save λ©μλλ₯Ό νΈμΆν΄μ dbμ μν°ν°λ₯Ό μ μ₯νλ λ‘μ§μΌλ‘ νλ¬ κ° κ²μλλ€.
μ°λ¦¬κ° λ§λ  createAccountκ° μμ λ‘μ§λλ‘ νλ¬κ°λ€κ³  κΈ°λνμμΌλ―λ‘, μ€μ λ‘ κ·Έλ κ² νΈμΆμ΄ λμλ νμΈλ§ ν΄μ£Όλ©΄ νμ€νΈλ₯Ό μ±κ³΅μ μΌλ‘ ν κ²μλλ€.
</br></br>
μμ λ‘μ§λλ‘ findOneμ΄ νΈμΆλμλκ°(toHaveBeenCalledTimes), νλΌλ―Έν°λ μ λλ‘ μλ ₯ λμλκ°(toHaveBeenCalledWith), createλ μ λλ‘ νΈμΆλμλκ°, saveλ μ λλ‘ νΈμΆλμκ³ , κ²°κ³Όκ° μ°λ¦¬κ° μνλ κ°(toMatchObject)μ΄ λμ€λκ°?λ₯Ό jestμμ νλ¨μ ν΄μ£ΌκΈ° λλ¬Έμ createAccountκ° μ μμ μΌλ‘ μλνλ κ²½μ° νμ€νΈκ° λλ κ²μλλ€.
</br></br>
createAccountλ₯Ό λͺ¨λ νμ€νΈνλ €λ©΄, μμμ μΈκΈλλ¦° λλ‘, μ΄λ―Έ μ΄λ©μΌ κ³μ μ΄ μ΄λ―Έ μλ κ²½μ°μ, save λ©μλκ° μ€ν¨ν  κ²½μ°λ₯Ό λͺ¨λ νμ€νΈν΄μΌ full coverageλ₯Ό μμ±ν  μ μμ΅λλ€.
</br>

μ°Έκ³  :
[jset κ³΅μλ¬Έμ](https://jestjs.io/docs/api),
[jset mocking](https://www.daleseo.com/jest-fn-spy-on/),
