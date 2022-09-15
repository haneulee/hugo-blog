---
title: "NestJS 프레임워크 - Entity & Resolver"
date: 2021-07-16T11:36:53+09:00
categories:
  - development
tags:
  - development
  - front-end
  - nestjs
  - typeorm
  - sql
  - eager
  - subscribe
  - entity
  - resolver
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

# NestJS 프레임워크 - Entity & Resolver

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/nestjs/img-1.png)

## Entity Setting (relation)

[eager](https://typeorm.io/#/eager-and-lazy-relations/eager-relations)

eager 데코레이터가 설정되어 있으면, N:1로 관계가 설정된 podcast의 데이터를 따로 설정 없이(이를테면, find 함수의 relation 사용)  
db에서 쉽게 가져올 수 있습니다.

```ts
import { ObjectType, Field } from "@nestjs/graphql";
import { IsString } from "class-validator";
import { Column, Entity, ManyToOne } from "typeorm";
import { CoreEntity } from "./core.entity";
import { Podcast } from "./podcast.entity";

@Entity()
@ObjectType()
export class Episode extends CoreEntity {
  @Column()
  @Field((type) => String)
  @IsString()
  title: string;

  @Column()
  @Field((type) => String)
  @IsString()
  category: string;

  @ManyToOne(() => Podcast, (podcast) => podcast.episodes, {
    onDelete: "CASCADE",
    eager: true,
  })
  @Field((type) => Podcast)
  podcast: Podcast;
}
```

review는 작성자(User)와 대상(Podcast)가 필요하고  
각각 리뷰와 1:N 관계가 필요하므로 위와 같이 entity를 작성할 수 있습니다.

```ts
@OneToMany(() => Episode, (episode) => episode.podcast)
  @Field((type) => [Episode])
  episodes: Episode[];

  @OneToMany(() => Review, (review) => review.podcast)
  @Field((type) => [Review])
  reviews: Review[];
```

podcast에서 episode와 review 1:N 관계 설정이 필요

```ts
@OneToMany(() => Review, (review) => review.creator, { eager: true })
  @Field((type) => [Review])
  reviews: Review[];

  @ManyToMany(() => Episode, { eager: true })
  @Field((type) => [Episode])
  @JoinTable()
  playedEpisodes: Episode[];

  @ManyToMany(() => Podcast, { eager: true })
  @Field(() => [Podcast])
  @JoinTable()
  subsriptions: Podcast[];
```

review, markEpisodeAsPlayed, subscribeToPodcast 구현을 위한 relation

<!--adsense-->

---

## Resolver

take, skip을 이용하여 pagination을 구현한 부분이 보이실 겁니다.  
또한 주의하셔야할 부분이 하나 있는데, where 옵션을 보시면 title: Like를 이용한 것이 보이실 건데,  
**sqlite**에는 case insensitive한 **ILIKE**가 없습니다.  
그래서 typeorm의 Like를 사용하셔도 case insensitive하게 find를 수행할 수 있으며  
또는, 위 코드의 주석문으로 처리한 **Raw(sql 문법사용할 수 있는 유틸함수)**를 이용하시면 됩니다.

```ts
async searchPodcasts({
    titleQuery,
    page
  }: SearchPodcastsInput): Promise<SearchPodcastsOutput> {
    try {
      const [podcasts, totalCount] = await this.podcastRepository.findAndCount({
        // where: { title: Raw((title) => `${title} LIKE ${titleQuery}`) },
        where: { title: Like(`%${titleQuery}%`) },
        take: 50,
        skip: (page - 1) * 50
      });
      if (!podcasts) {
        return { ok: false, error: "Could not find podcasts" };
      }
      return {
        ok: true,
        podcasts,
        totalCount,
        totalPages: Math.ceil(totalCount / 50)
      };
    } catch (err) {
      console.log(err);
      return this.InternalServerErrorOutput;
    }
  }

```

createReview mutation은 episode를 podcast에 추가할 때와 똑같이 구현해주면 됩니다.

```ts
async createReview(
    creator: User,
    { title, text, podcastId }: CreateReviewInput
  ): Promise<CreateReviewOutput> {
    try {
      const { ok, error: podcastFindErr, podcast } = await this.getPodcast(
        podcastId
      );
      if (!ok || podcastFindErr) {
        return { ok: false, error: podcastFindErr };
      }
      const review = this.reviewRepository.create({ title, text });
      review.podcast = podcast;
      review.creator = creator;
      const { id } = await this.reviewRepository.save(review);
      return { ok: true, id };
    } catch {
      return this.InternalServerErrorOutput;
    }
  }
```

toggleSubscribe으로 subscribe을 toggle할 수 있는 방식입니다.  
이미 구독이 있으면 구독에서 삭제하는 부분은 filter 함수를 이용하여 배열에서 삭제하도록 구현되어 있습니다.  
구독에 포함시키는 부분은 spread operator를 이용하여 구현되어 있습니다.

[some](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/some)  
[filter](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)  
[spread operator](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

```ts
async toggleSubscribe(
    user: User,
    { podcastId }: ToggleSubscribeInput
  ): Promise<ToggleSubscribeOutput> {
    try {
      const podcast = await this.podcasts.findOne({ id: podcastId });
      if (!podcast) {
        return { ok: false, error: "Podcast not found" };
      }
      if (user.subsriptions.some((sub) => sub.id === podcast.id)) {
        user.subsriptions = user.subsriptions.filter(
          (sub) => sub.id !== podcast.id
        );
      } else {
        console.log("foo");
        user.subsriptions = [...user.subsriptions, podcast];
      }
      await this.users.save(user);
      return { ok: true };
    } catch {
      return this.InternalServerErrorOutput;
    }
  }
```

playedEpisodes는 entity에 episode와 1:n 관계로 묶인 episode 배열입니다.  
해당 episode를 episodesEpisodes에 추가한 것입니다.

아래 코드와 달리 해당 에피소드를 이미 시청한 경우에는 추가시키지 않는 로직을 만드는 것도 괜찮아 보입니다.  
includes나, every 등을 이용하면 구현할 수 있습니다.

[includes](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)  
[every](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/every)

```ts
async markEpisodeAsPlayed(
    user: User,
    { id: episodeId }: MarkEpisodeAsPlayedInput
  ): Promise<MarkEpisodeAsPlayedOutput> {
    try {
      const episode = await this.episodes.findOne({ id: episodeId });
      if (!episode) {
        return { ok: false, error: "Episode not found" };
      }
      user.playedEpisodes = [...user.playedEpisodes, episode];
      await this.users.save(user);
      return { ok: true };
    } catch {
      return this.InternalServerErrorOutput;
    }
  }
```

---

참고 :
[nestJS 공식문서](https://docs.nestjs.com/)
