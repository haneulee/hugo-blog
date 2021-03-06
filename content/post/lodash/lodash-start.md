---
title: "Lodash ๋ ๐ค"
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

Lodash๋ ๋ฐฐ์ด, ์ซ์, ๊ฐ์ฒด, ๋ฌธ์์ด ๋ฑ์ผ๋ก ์์ํ๋ ๋ฒ๊ฑฐ ๋ก์์ ์์  ์๋ฐ ์คํฌ๋ฆฝํธ๋ฅผ ๋ ์ฝ๊ฒ ๋ง๋ญ๋๋ค.
Lodash์ ๋ชจ๋ ์ ๋ฐฉ๋ฒ์ ๋ค์์ ์ ํฉํฉ๋๋ค.

- ๋ฐฐ์ด, ๊ฐ์ฒด ๋ฐ ๋ฌธ์์ด ๋ฐ๋ณต
- ๊ฐ ์กฐ์ ๋ฐ ํ์คํธ
- ๋ณตํฉ ํจ์ ๋ง๋ค๊ธฐ
{{< adsense >}}
## map

### _.map(collection, [iteratee=_.identity])
- ๋ฐฐ์ด ์์ ๊ฐ์ฒด๋ค์ ์์ ์ค, ํน์  ์์๋ง ๋นผ์ ๋ฐฐ์ด๋ก ๋ง๋ค๊ณ  ์ถ์ ๊ฒฝ์ฐ ์ฌ์ฉํฉ๋๋ค.

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
- Collection ๊ฐ๋ค์ ์ํ๋ ํ๋๋ฅผ ๊ธฐ์ค์ผ๋ก ์ ๋ ฌํด์ค๋๋ค.


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
- ๋ฐฐ์ด ์์ ๊ฐ์ฒด๋ค์ ์์ ์ค๋ณต์ ์ ๊ฑฐํ๊ณ  ์ถ์ ๋ ์ฌ์ฉํฉ๋๋ค. (์ถ๊ฐ๋ก, uniq ํจ์๋ ๋ฐฐ์ด์ ์ค๋ณต์ ์ ๊ฑฐํฉ๋๋ค.)

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
codepen์์ lodash๋ฅผ ํ์คํธ ํด๋ณผ ์ ์๋ค. 

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/lodash/img-1.png)


