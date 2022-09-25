---
title: "NestJS 에서 E2E TEST 🏃🏻‍♀️"
date: 2021-07-14T14:40:42+09:00
categories:
  - development
tags:
  - development
  - front-end
  - e2e
  - jest
  - javascript
  - facebook
  - react
  - nextjs
  - supertest
  - endtoendtest
  - 테스트주도개발
  - 제스트
  - TDD
  - 페이스북
  - 엔드투엔드테스트
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

# E2E TEST 🏃🏻‍♀️

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-jest.png)

## E2E Test (End To End Test) 란 ?

개별 모듈 및 클래스에 중점을 두는 단위 테스트와 달리 e2e 테스트는 최종 사용자가 프로덕션과 함께 하게 될 상호 작용의 종류에 더 가까운 보다 종합적인 수준에서 클래스와 모듈의 상호 작용을 다룹니다.
각 API 엔드포인트의 종단 간 테스트는 시스템의 전반적인 동작이 정확하고 프로젝트 요구 사항을 충족하는지 확인하는 데 도움이 됩니다.
NestJS를 사용하면 **[supertest](https://github.com/visionmedia/supertest)** 라이브러리를 사용하여 **HTTP 요청**을 쉽게 시뮬레이션할 수 있습니다.

- Endpoint(종단) 간 테스트로 사용자의 입장에서 사용자가 사용하는 상황을 가정하고 테스트 하는 것
- 일반적으로 웹이나 어플 등에서 GUI를 통해 시나리오, 기능 테스트 등을 수행한다.
- 사용자에게 직접적으로 노출되는 부분을 점검한다.
- 유닛 테스트로 불가능한 사용자 관점의 테스트까지 가능하다.
- Endpoint 테스트를 통과하면 기능이 잘 작동한다는 것이므로 모든 테스트를 할 수 없다면 E2E Test만이라도 하는 것이 좋다!
- 백엔드 관점에서 개발한 REST API를 테스트 하기 위해 실제로 서버에 요청을 보낸 뒤 클라이언트에서 원하는 데이터가 전송되는 지 확인해야 한다.

{{< hl-text yellow >}}
E2E 테스트는 환경에 의존하는 테스트이지만, 단위 테스트는 실행 중인 환경에 의존하면 안 되고, 빠르게 실행되어야 한다. E2E 테스트에서는 보통 테스트 데이터베이스를 사용하고, 테스트의 신뢰성이 높지만 속도가 느리다는 단점이 있다.
{{< /hl-text >}}

<!--adsense-->

## NestJS

NestJS에서는 특정 도구를 강제하지는 않지만 Jest를 기본 테스트 프레임워크로 제공해주며 테스팅 패키지도 제공하기 때문에 개발자가 다른 도구를 찾는데 소모하는 리소스를 줄일 수 있다.

</br></br>

## 테스트 설정하기

```ts
let podcastsRepository: Repository<Podcast>;
let episodesRepository: Repository<Episode>;
let usersRepository: Repository<User>;
```

테스트 설정에 let으로 repository들이 초기화되어있는데, 밑 라인의 beforeAll에서 app과 repository를 초기화시키기 때문에 let으로 선언되어 있습니다.
</br></br>

- repository 초기화

```ts
podcastsRepository = moduleFixture.get<Repository<Podcast>>(
  getRepositoryToken(Podcast)
);
```

나머지 episodeRepsitory, usersRepository 초기화 방법은 모두 동일합니다.
</br></br>

> [afterAll](https://jestjs.io/docs/api#afterallfn-timeout)
>
> - 테스트를 매번 새로 시작할 때마다 만든 데이터들이 쌓여 있으면 다음 테스트에 영향을 미치기 때문에, databse에 drop 명령을 내려 DB를 초기화시키는 과정이 필요합니다. 그래서 afterAll 안에서 이 과정을 수행하도록 합니다.
>   </br></br>

## 테스트 수행

e2e테스트는 흔히 종단간 테스트로 번역이 되고, 실제 사용자가 행동하는 방식으로 테스트를 한다고 생각하시면 됩니다. unit 테스트처럼 가짜 데이터 베이스를 사용하지 않습니다.

```ts
const baseTest = () => request(app.getHttpServer()).post(GRAPHQL_ENDPOINT);
const publicTest = (query: string) => baseTest().send({ query });
const privateTest = (query: string) =>
  baseTest().set("X-JWT", jwtToken).send({ query });
```

e2e테스트에서는 request(app.getHttpServer()).post(GRAPHQL_ENDPOINT).send({query})가 계속 반복될 것이므로 함수를 wrapping 해놓았습니다.
request는 [supertest](https://github.com/visionmedia/supertest) 패키지에서 import한 함수이며, express test를 위해 nestjs 프레임워크에 포함 된 패키지입니다
</br></br>
privateTest에 보시면 set('X-JWT', jwtToken)는 헤더에 'X-JWT'라는 이름으로 jwtToken을 넘겨주는 과정입니다.

```ts
describe("Podcasts Resolver", () => {
  describe("createPodcast", () => {
    it("should create a new podcast", () =>
      publicTest(`
            mutation {
              createPodcast(input: {
                title: "${testPodcast.title}",
                category: "${testPodcast.category}",
              }) {
                ok
                id
              }
            }
          `)
        .expect(200)
        .expect((res) => {
          expect(res.body.data.createPodcast.ok).toBe(true);
          expect(res.body.data.createPodcast.id).toBe(1);
        }));
  });
});
```

</br></br>
래핑해 놓은 함수에 **mutation ~** 부분에 실제로 graphql 문이 들어가있습니다. 주의하실 부분은 ${testPodcast.title} 이 부분인데 자바스크립트에서는 저렇게만 해도 string으로 인식하지만, graphql에서는 그렇지 않습니다. 작은 따옴표(')도 아니고 큰 따옴표(")로 감싸주어야 텍스트로 인식하므로 주의하셔야 합니다.

</br></br>
또 한가지 주의해야 할 점은 request.send...(솔루션은 publicRest, privateTest) 이 코드들은 반드시 리턴값으로 넘겨주셔야 합니다. 그렇지 않으면 테스트는 무조건 success로 나오기 때문에 주의하셔야 합니다. 나머지 결과들도 영향을 받을 수 있기 때문에 꼭 리턴값으로 넘기셔야 한다는 것을 기억하셔야 합니다.
</br></br>

expect(200): 200은 post 메소드로 send함수를 이용하여 보낸 request에 대한 응답의 status code를 의미합니다. /graphql에 정상적으로 query가 잘 보내졌으면, 200 의 응답코드를 받아야 한다는 의미인데, 위에서 언급한 큰 따옴표를 생략하고 request 요청을 하면 흔히 400 응답코드를 많이 받습니다.
</br></br>
테스트 방법은 unit 테스트처럼, 성공적으로 처리 되는 경우, 에러인 경우 에러처리 등의 경우가 잘 처리되고 있나 테스트 해보시면 됩니다.
unit테스트와는 달리 실제 DB 사용, 실제 graphql에 query 요청을 한다는 점 등이 다릅니다.
</br></br>

```ts
describe("updatePodcast", () => {
  const rating = 3;
  let podcastId: number;

  beforeAll(async () => {
    const [podcast] = await podcastsRepository.find();
    podcastId = podcast.id;
  });

  it("should success to update Podcast", () => {
    return publicTest(`
            mutation {
              updatePodcast(input: { id: ${podcastId}, payload: { rating: ${rating} } }) {
                ok
              }
            }
          `)
      .expect(200)
      .expect((res) => {
        const {
          body: {
            data: {
              updatePodcast: { ok },
            },
          },
        } = res;
        expect(ok).toBe(true);
      });
  });
  it("should failed to update Podcast, becuase of getPodcast emitting error", () => {
    const errorPodcastId = 1000;
    return publicTest(`
            mutation {
              updatePodcast(input: { id: ${errorPodcastId}, payload: { rating: ${rating} } }) {
                ok
                error
              }
            }
          `)
      .expect(200)
      .expect((res) => {
        const {
          body: {
            data: {
              updatePodcast: { ok, error },
            },
          },
        } = res;
        expect(ok).toBe(false);
        expect(error).toBe(`Podcast with id ${errorPodcastId} not found`);
      });
  });
  it("should fail to update Podcast, due to invalid payload", () => {
    const errorRating = 10;
    return publicTest(`
            mutation {
              updatePodcast(input: { id: ${podcastId}, payload: { rating: ${errorRating} } }) {
                ok
                error
              }
            }
          `)
      .expect(200)
      .expect((res) => {
        const {
          body: {
            data: {
              updatePodcast: { ok, error },
            },
          },
        } = res;
        expect(ok).toBe(false);
        expect(error).toBe("Rating must be between 1 and 5.");
      });
  });
});
```

---

참고 :

[supertest](https://github.com/visionmedia/supertest),
[nextJS 공식문서](https://docs.nestjs.com/fundamentals/testing#end-to-end-testing),
[](),
