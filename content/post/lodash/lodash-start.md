---
title: "Lodash 란 🤔"
date: 2021-05-25T14:34:02+09:00
categories: 
- development
- lodash
tags: 
- development
- front-end
- lodash
- javascript
- map
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/lodash/img-1.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---
<!--toc-->

# [Lodash](https://lodash.com/)

Lodash는 배열, 숫자, 객체, 문자열 등으로 작업하는 번거 로움을 없애 자바 스크립트를 더 쉽게 만듭니다.
Lodash의 모듈 식 방법은 다음에 적합합니다.

- 배열, 객체 및 문자열 반복
- 값 조작 및 테스트
- 복합 함수 만들기
{{< adsense >}}
## map

### _.map(collection, [iteratee=_.identity])
- 배열 안에 객체들의 요소 중, 특정 요소만 빼서 배열로 만들고 싶은 경우 사용합니다.

Creates an array of values by running each element in collection thru iteratee. The iteratee is invoked with three arguments:
(value, index|key, collection).

Many lodash methods are guarded to work as iteratees for methods like _.every, _.filter, _.map, _.mapValues, _.reject, and _.some.

***Arguments***
collection (Array|Object): The collection to iterate over.
[iteratee=_.identity] (Function): The function invoked per iteration.

***Returns***
(Array): Returns the new mapped array.

***Example***

```
function square(n) {
  return n * n;
}
 
_.map([4, 8], square);
// => [16, 64]
 
_.map({ 'a': 4, 'b': 8 }, square);
// => [16, 64] (iteration order is not guaranteed)
 
var users = [
  { 'user': 'barney' },
  { 'user': 'fred' }
];
 
// The `_.property` iteratee shorthand.
_.map(users, 'user');
// => ['barney', 'fred']
Try in REPL
```

## sortBy
- Collection 값들을 원하는 필드를 기준으로 정렬해줍니다.


### _.sortBy(collection, [iteratees=[_.identity]])
Creates an array of elements, sorted in ascending order by the results of running each element in a collection thru each iteratee. This method performs a stable sort, that is, it preserves the original sort order of equal elements. The iteratees are invoked with one argument: (value).



***Arguments***
collection (Array|Object): The collection to iterate over.
[iteratees=[_.identity]] (...(Function|Function[])): The iteratees to sort by.

***Returns***
(Array): Returns the new sorted array.

***Example***
```
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 },
  { 'user': 'barney', 'age': 34 }
];
 
_.sortBy(users, [function(o) { return o.user; }]);
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
 
_.sortBy(users, ['user', 'age']);
// => objects for [['barney', 34], ['barney', 36], ['fred', 40], ['fred', 48]]
```

## uniqBy
- 배열 안에 객체들의 요소 중복을 제거하고 싶을 때 사용합니다. (추가로, uniq 함수는 배열의 중복을 제거합니다.)

### _.uniqBy(array, [iteratee=_.identity])
This method is like _.uniq except that it accepts iteratee which is invoked for each element in array to generate the criterion by which uniqueness is computed. The order of result values is determined by the order they occur in the array. The iteratee is invoked with one argument:
(value).

***Arguments***
array (Array): The array to inspect.
[iteratee=_.identity] (Function): The iteratee invoked per element.



***Returns***
(Array): Returns the new duplicate free array.

***Example***
```
_.uniqBy([2.1, 1.2, 2.3], Math.floor);
// => [2.1, 1.2]
 
// The `_.property` iteratee shorthand.
_.uniqBy([{ 'x': 1 }, { 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }]
```


[lodash tester](https://codepen.io/travist/full/jrBjBz/)
codepen에서 lodash를 테스트 해볼 수 있다. 

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/lodash/img-1.png)


