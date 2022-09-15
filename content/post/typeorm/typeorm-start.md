---
title: "Typeorm Start "
date: 2021-07-05T13:56:56+09:00
categories:
  - development
tags:
  - development
  - front-end
  - typeorm
  - nestjs
  - graphql
  - schema
  - entity
  - typescript
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

<!--adsense-->

# Typeorm

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/typeorm/img-1.png)

## ORM (Object Relational Mapping)

ORM (Object-relational mapping)은 객체지향 프로그래밍(Object-Oriented-Programming) 과 관계형 데이터베이스(Relational-Database)사이의 호환되지 않는 데이터를 변환하는 시스템이다. 객체지향 프로그래밍은 Class를 사용하고 관계형 데이터베이스는 Table을 사용한다.

### 장점

- 선언, 할당, 종료 같은 부수적인 코드가 없거나 급격히 줄어든다.
- 각종 객체에 대한 코드를 별도로 작성하기 떄문에 코드의 가독성을 올려준다.
- SQL 의 절차, 순차적인 접근 방식이 아닌 객체 접근 방식이다.

### 단점

- 완벽하게 ORM 서비스구현이 어려울수있다.
- 사용하기에 편리함은 있지만 설계가 복잡하다.
- 프로젝트 복잡성과난이도레따라 퍼포먼스의 큰차이가 있다.

## TypeOrm

TypeOrm 이란 TypeScript 와 JavaScript(ES5 , ES6 , ES7) 용 ORM이다.
MySQL, PostgreSQL, MariaDB, SQLite, MS SQL Server, Oracle, WebSQL 데이터베이스를 지원한다.

## entity 설정

nestjs에서 typeorm을 사용하려면 repository를 이용하기 위해 typeorm의 data mapper 패턴을 사용합니다.

```ts
import { Episode } from './episode.entity';
import { ObjectType, Field, InputType } from '@nestjs/graphql';
import { IsString, IsNumber } from 'class-validator';
import { Column, Entity, OneToMany, PrimaryGeneratedColumn } from 'typeorm';

@InputType({ isAbstract: true })
@ObjectType()
@Entity()
export class Podcast {
  @PrimaryGeneratedColumn()
  @Field((_) => Number)
  @IsNumber()
  id: number;
...
```

- @Entity 데코레이터 : TypeORM에게 Entity임을 알려준다.
- @Column 데코레이터 : TypeORM에서 db 필드 설정을 해주는 데코레이터

또한 graphql의 object type, input type임을 역시 데코레이터를 이용하여 알려주고, input type이나 object type에 name을 지정해주어서 중복 이름을 갖지 않도록 합니다.

## entity 등록 설정

src/app.module.ts의 imports에 보면 TypeOrmModule.forRoot 안에 entity를 꼭 등록하고 사용해야 한다.

```ts
@Module({
  imports: [
    PodcastsModule,
    GraphQLModule.forRoot({ autoSchemaFile: true }),
    TypeOrmModule.forRoot({
      type: "sqlite",
      database: "db.sqlite",
      logging: true,
      synchronize: true,
      entities: [Podcast, Episode],
    }),
  ],
  controllers: [],
  providers: [],
})
export class AppModule {}
```

src/podcast/podcast.module.ts의 imports에 TypeOrmModule.forFeature에도 사용 등록을 해야 한다.

```ts
@Module({
  imports: [TypeOrmModule.forFeature([Podcast, Episode])],
  providers: [PodcastsService, PodcastsResolver, EpisodeResolver],
})
export class PodcastsModule {}
```

service에서 사용하려면 repository를 설정해주어야 한다.

```ts
@Injectable()
export class PodcastsService {
  constructor(
    @InjectRepository(Podcast)
    private readonly podcasts: Repository<Podcast>,

    @InjectRepository(Episode)
    private readonly episodes: Repository<Episode>,
  ) {}

```

## Relation 설정

데이터베이스의 관계에는 1:1, 1:N, N:N이 있습니다.
TypeORM에서는 @OneToOne , @OneToMany / @ManyToOne , @ManyToMany 데코레이터를 이용해서 관계를 설정할 수 있습니다.

```ts
@Field((type) => [Episode], { nullable: true })
  @OneToMany((type) => Episode, (episode) => episode.podcast)
  episodes: Episode[];

@ManyToOne((type) => Podcast, (podcast) => podcast.episodes, {
    cascade: true,
  })
  podcast: Podcast;
```

Podcast에는 여러개의 Episode가 있습니다. 하지만 Episode는 한 개의 Podcast에 속할 수 있지, 다른 Podcast에 속할 순 없습니다.
그래서 1:N 관계는 Podcast 쪽에서는 @OneToMany , 반대로 Episode에는 @ManyToOne 데코레이터를 사용하여 설정을 해주면 됩니다.

그런데, Podcast의 OneToMany 끝 부분을 보면, {cascade: true} 라고 되어 있습니다.
[cascade](https://orkhan.gitbook.io/typeorm/docs/relations#cascades) 옵션이 true 값이면, podcast에 연결된 episode는 save를 하지 않아도 db에 자동으로 저장이 됩니다.
Episode에는 onDelete: "CASCADE"라고 되어 있습니다. 레퍼런스 오브젝트가 삭제되었을 때 어떻게 외래키에 해당하는 오브젝트는 어떻게 행동해야 하는지 설정해 놓는 값입니다.
[onDelete](https://typeorm.io/#/relations/relation-options)

## CRUD

typeorm에서는 repository에서 create를 한다해서 database에 바로 저장이 되는 것은 아닙니다.
create에 해당 entity의 오브젝트를 만들고 실제로 저장은 save 메소드를 이용해서 합니다.
Promise를 리턴해주기 때문에 async/await를 이용해서 해당 save를 호출 하면 됩니다.
save 메소드는 Update에서도 이용합니다. save 메소드는 항상 주어진 조건의 entity가 존재하는지 여부를 확인하고 없다면 새로운 엔티티를 만들고, 있다면 해당 엔티티를 업데이트하기 때문입니다.
update 메소드를 이용해서도 Update 작업을 할 수 있습니다만, update 메소드는 검색 criteria가 맞는지 여부는 확인 안하기 때문에, 속도는 좀더 빠르지만, 조금더 신중하게 사용할 필요는 있습니다.
[save, update 메소드](https://typeorm.io/#/repository-api/repository-api)

참고 :
[https://typeorm.io/#/](https://typeorm.io/#/)
