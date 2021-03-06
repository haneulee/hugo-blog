---
title: "NestJS ์์ E2E TEST ๐๐ปโโ๏ธ"
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
- ํ์คํธ์ฃผ๋๊ฐ๋ฐ
- ์ ์คํธ
- TDD
- ํ์ด์ค๋ถ
- ์๋ํฌ์๋ํ์คํธ
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


# E2E TEST ๐๐ปโโ๏ธ

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-jest.png)

## E2E Test (End To End Test) ๋ ?

๊ฐ๋ณ ๋ชจ๋ ๋ฐ ํด๋์ค์ ์ค์ ์ ๋๋ ๋จ์ ํ์คํธ์ ๋ฌ๋ฆฌ e2e ํ์คํธ๋ ์ต์ข ์ฌ์ฉ์๊ฐ ํ๋ก๋์๊ณผ ํจ๊ป ํ๊ฒ ๋  ์ํธ ์์ฉ์ ์ข๋ฅ์ ๋ ๊ฐ๊น์ด ๋ณด๋ค ์ขํฉ์ ์ธ ์์ค์์ ํด๋์ค์ ๋ชจ๋์ ์ํธ ์์ฉ์ ๋ค๋ฃน๋๋ค. 
๊ฐ API ์๋ํฌ์ธํธ์ ์ข๋จ ๊ฐ ํ์คํธ๋ ์์คํ์ ์ ๋ฐ์ ์ธ ๋์์ด ์ ํํ๊ณ  ํ๋ก์ ํธ ์๊ตฌ ์ฌํญ์ ์ถฉ์กฑํ๋์ง ํ์ธํ๋ ๋ฐ ๋์์ด ๋ฉ๋๋ค. 
NestJS๋ฅผ ์ฌ์ฉํ๋ฉด **[supertest](https://github.com/visionmedia/supertest)** ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ฌ์ฉํ์ฌ **HTTP ์์ฒญ**์ ์ฝ๊ฒ ์๋ฎฌ๋ ์ด์ํ  ์ ์์ต๋๋ค.

- Endpoint(์ข๋จ) ๊ฐ ํ์คํธ๋ก ์ฌ์ฉ์์ ์์ฅ์์ ์ฌ์ฉ์๊ฐ ์ฌ์ฉํ๋ ์ํฉ์ ๊ฐ์ ํ๊ณ  ํ์คํธ ํ๋ ๊ฒ
- ์ผ๋ฐ์ ์ผ๋ก ์น์ด๋ ์ดํ ๋ฑ์์ GUI๋ฅผ ํตํด ์๋๋ฆฌ์ค, ๊ธฐ๋ฅ ํ์คํธ ๋ฑ์ ์ํํ๋ค.
- ์ฌ์ฉ์์๊ฒ ์ง์ ์ ์ผ๋ก ๋ธ์ถ๋๋ ๋ถ๋ถ์ ์ ๊ฒํ๋ค.
- ์ ๋ ํ์คํธ๋ก ๋ถ๊ฐ๋ฅํ ์ฌ์ฉ์ ๊ด์ ์ ํ์คํธ๊น์ง ๊ฐ๋ฅํ๋ค.
- Endpoint ํ์คํธ๋ฅผ ํต๊ณผํ๋ฉด ๊ธฐ๋ฅ์ด ์ ์๋ํ๋ค๋ ๊ฒ์ด๋ฏ๋ก ๋ชจ๋  ํ์คํธ๋ฅผ ํ  ์ ์๋ค๋ฉด E2E Test๋ง์ด๋ผ๋ ํ๋ ๊ฒ์ด ์ข๋ค!
- ๋ฐฑ์๋ ๊ด์ ์์ ๊ฐ๋ฐํ REST API๋ฅผ ํ์คํธ ํ๊ธฐ ์ํด ์ค์ ๋ก ์๋ฒ์ ์์ฒญ์ ๋ณด๋ธ ๋ค ํด๋ผ์ด์ธํธ์์ ์ํ๋ ๋ฐ์ดํฐ๊ฐ ์ ์ก๋๋ ์ง ํ์ธํด์ผ ํ๋ค.

{{< hl-text yellow >}}
E2E ํ์คํธ๋ ํ๊ฒฝ์ ์์กดํ๋ ํ์คํธ์ด์ง๋ง, ๋จ์ ํ์คํธ๋ ์คํ ์ค์ธ ํ๊ฒฝ์ ์์กดํ๋ฉด ์ ๋๊ณ , ๋น ๋ฅด๊ฒ ์คํ๋์ด์ผ ํ๋ค. E2E ํ์คํธ์์๋ ๋ณดํต ํ์คํธ ๋ฐ์ดํฐ๋ฒ ์ด์ค๋ฅผ ์ฌ์ฉํ๊ณ , ํ์คํธ์ ์ ๋ขฐ์ฑ์ด ๋์ง๋ง ์๋๊ฐ ๋๋ฆฌ๋ค๋ ๋จ์ ์ด ์๋ค.
{{< /hl-text >}}



{{< adsense >}}

## NestJS

NestJS์์๋ ํน์  ๋๊ตฌ๋ฅผ ๊ฐ์ ํ์ง๋ ์์ง๋ง Jest๋ฅผ ๊ธฐ๋ณธ ํ์คํธ ํ๋ ์์ํฌ๋ก ์ ๊ณตํด์ฃผ๋ฉฐ ํ์คํ ํจํค์ง๋ ์ ๊ณตํ๊ธฐ ๋๋ฌธ์ ๊ฐ๋ฐ์๊ฐ ๋ค๋ฅธ ๋๊ตฌ๋ฅผ ์ฐพ๋๋ฐ ์๋ชจํ๋ ๋ฆฌ์์ค๋ฅผ ์ค์ผ ์ ์๋ค.

</br></br>
## ํ์คํธ ์ค์ ํ๊ธฐ

```ts

let podcastsRepository: Repository<Podcast>;
let episodesRepository: Repository<Episode>;
let usersRepository: Repository<User>;
```
ํ์คํธ ์ค์ ์ let์ผ๋ก repository๋ค์ด ์ด๊ธฐํ๋์ด์๋๋ฐ, ๋ฐ ๋ผ์ธ์ beforeAll์์ app๊ณผ repository๋ฅผ ์ด๊ธฐํ์ํค๊ธฐ ๋๋ฌธ์ let์ผ๋ก ์ ์ธ๋์ด ์์ต๋๋ค.
</br></br>
- repository ์ด๊ธฐํ

```ts
podcastsRepository = moduleFixture.get<Repository<Podcast>>(getRepositoryToken(Podcast));
```
๋๋จธ์ง episodeRepsitory, usersRepository ์ด๊ธฐํ ๋ฐฉ๋ฒ์ ๋ชจ๋ ๋์ผํฉ๋๋ค.
</br></br>
> [afterAll](https://jestjs.io/docs/api#afterallfn-timeout)
> - ํ์คํธ๋ฅผ ๋งค๋ฒ ์๋ก ์์ํ  ๋๋ง๋ค ๋ง๋  ๋ฐ์ดํฐ๋ค์ด ์์ฌ ์์ผ๋ฉด ๋ค์ ํ์คํธ์ ์ํฅ์ ๋ฏธ์น๊ธฐ ๋๋ฌธ์, databse์ drop ๋ช๋ น์ ๋ด๋ ค DB๋ฅผ ์ด๊ธฐํ์ํค๋ ๊ณผ์ ์ด ํ์ํฉ๋๋ค. ๊ทธ๋์ afterAll ์์์ ์ด ๊ณผ์ ์ ์ํํ๋๋ก ํฉ๋๋ค.
</br></br>

## ํ์คํธ ์ํ

e2eํ์คํธ๋ ํํ ์ข๋จ๊ฐ ํ์คํธ๋ก ๋ฒ์ญ์ด ๋๊ณ , ์ค์  ์ฌ์ฉ์๊ฐ ํ๋ํ๋ ๋ฐฉ์์ผ๋ก ํ์คํธ๋ฅผ ํ๋ค๊ณ  ์๊ฐํ์๋ฉด ๋ฉ๋๋ค. unit ํ์คํธ์ฒ๋ผ ๊ฐ์ง ๋ฐ์ดํฐ ๋ฒ ์ด์ค๋ฅผ ์ฌ์ฉํ์ง ์์ต๋๋ค.

```ts
const baseTest = () => request(app.getHttpServer()).post(GRAPHQL_ENDPOINT);
const publicTest = (query: string) => baseTest().send({ query });
const privateTest = (query: string) => baseTest().set('X-JWT', jwtToken).send({ query });
```
e2eํ์คํธ์์๋ request(app.getHttpServer()).post(GRAPHQL_ENDPOINT).send({query})๊ฐ ๊ณ์ ๋ฐ๋ณต๋  ๊ฒ์ด๋ฏ๋ก ํจ์๋ฅผ wrapping ํด๋์์ต๋๋ค. 
request๋ [supertest](https://github.com/visionmedia/supertest) ํจํค์ง์์ importํ ํจ์์ด๋ฉฐ, express test๋ฅผ ์ํด nestjs ํ๋ ์์ํฌ์ ํฌํจ ๋ ํจํค์ง์๋๋ค
</br></br>
privateTest์ ๋ณด์๋ฉด set('X-JWT', jwtToken)๋ ํค๋์ 'X-JWT'๋ผ๋ ์ด๋ฆ์ผ๋ก jwtToken์ ๋๊ฒจ์ฃผ๋ ๊ณผ์ ์๋๋ค.

```ts
describe('Podcasts Resolver', () => {
    describe('createPodcast', () => {
      it('should create a new podcast', () =>
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
๋ํํด ๋์ ํจ์์ **mutation ~** ๋ถ๋ถ์ ์ค์ ๋ก graphql ๋ฌธ์ด ๋ค์ด๊ฐ์์ต๋๋ค. ์ฃผ์ํ์ค ๋ถ๋ถ์ ${testPodcast.title} ์ด ๋ถ๋ถ์ธ๋ฐ ์๋ฐ์คํฌ๋ฆฝํธ์์๋ ์ ๋ ๊ฒ๋ง ํด๋ string์ผ๋ก ์ธ์ํ์ง๋ง, graphql์์๋ ๊ทธ๋ ์ง ์์ต๋๋ค. ์์ ๋ฐ์ดํ(')๋ ์๋๊ณ  ํฐ ๋ฐ์ดํ(")๋ก ๊ฐ์ธ์ฃผ์ด์ผ ํ์คํธ๋ก ์ธ์ํ๋ฏ๋ก ์ฃผ์ํ์์ผ ํฉ๋๋ค.

</br></br>
๋ ํ๊ฐ์ง ์ฃผ์ํด์ผ ํ  ์ ์ request.send...(์๋ฃจ์์ publicRest, privateTest) ์ด ์ฝ๋๋ค์ ๋ฐ๋์ ๋ฆฌํด๊ฐ์ผ๋ก ๋๊ฒจ์ฃผ์์ผ ํฉ๋๋ค. ๊ทธ๋ ์ง ์์ผ๋ฉด ํ์คํธ๋ ๋ฌด์กฐ๊ฑด success๋ก ๋์ค๊ธฐ ๋๋ฌธ์ ์ฃผ์ํ์์ผ ํฉ๋๋ค. ๋๋จธ์ง ๊ฒฐ๊ณผ๋ค๋ ์ํฅ์ ๋ฐ์ ์ ์๊ธฐ ๋๋ฌธ์ ๊ผญ ๋ฆฌํด๊ฐ์ผ๋ก ๋๊ธฐ์์ผ ํ๋ค๋ ๊ฒ์ ๊ธฐ์ตํ์์ผ ํฉ๋๋ค.
</br></br>

expect(200): 200์ post ๋ฉ์๋๋ก sendํจ์๋ฅผ ์ด์ฉํ์ฌ ๋ณด๋ธ request์ ๋ํ ์๋ต์ status code๋ฅผ ์๋ฏธํฉ๋๋ค. /graphql์ ์ ์์ ์ผ๋ก query๊ฐ ์ ๋ณด๋ด์ก์ผ๋ฉด, 200 ์ ์๋ต์ฝ๋๋ฅผ ๋ฐ์์ผ ํ๋ค๋ ์๋ฏธ์ธ๋ฐ, ์์์ ์ธ๊ธํ ํฐ ๋ฐ์ดํ๋ฅผ ์๋ตํ๊ณ  request ์์ฒญ์ ํ๋ฉด ํํ 400 ์๋ต์ฝ๋๋ฅผ ๋ง์ด ๋ฐ์ต๋๋ค.
</br></br>
ํ์คํธ ๋ฐฉ๋ฒ์ unit ํ์คํธ์ฒ๋ผ, ์ฑ๊ณต์ ์ผ๋ก ์ฒ๋ฆฌ ๋๋ ๊ฒฝ์ฐ, ์๋ฌ์ธ ๊ฒฝ์ฐ ์๋ฌ์ฒ๋ฆฌ ๋ฑ์ ๊ฒฝ์ฐ๊ฐ ์ ์ฒ๋ฆฌ๋๊ณ  ์๋ ํ์คํธ ํด๋ณด์๋ฉด ๋ฉ๋๋ค. 
unitํ์คํธ์๋ ๋ฌ๋ฆฌ ์ค์  DB ์ฌ์ฉ, ์ค์  graphql์ query ์์ฒญ์ ํ๋ค๋ ์  ๋ฑ์ด ๋ค๋ฆ๋๋ค.
</br></br>

```ts
describe('updatePodcast', () => {
      const rating = 3;
      let podcastId: number;
      
      beforeAll(async () => {
        const [podcast] = await podcastsRepository.find();
        podcastId = podcast.id;
      });

      it('should success to update Podcast', () => {
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
      it('should failed to update Podcast, becuase of getPodcast emitting error', () => {
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
      it('should fail to update Podcast, due to invalid payload', () => {
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
            expect(error).toBe('Rating must be between 1 and 5.');
          });
      });
    });
```



--- 

์ฐธ๊ณ  :

[supertest](https://github.com/visionmedia/supertest),
[nextJS ๊ณต์๋ฌธ์](https://docs.nestjs.com/fundamentals/testing#end-to-end-testing),
[](),