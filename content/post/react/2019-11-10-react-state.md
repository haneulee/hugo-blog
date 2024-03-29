---
layout: post
title: "how to handle React state array"
date: 2019-11-10 00:03:00 +0900
categories: [development, React]
tags: [javascript, react, state, array, 리액트]
---

<!--toc-->

# state 안에 있는 배열에 변화를 주는 방법

## 1. concat

- 기존 배열을 그대로 두고 새 배열을 생성한다.

<!--adsense-->

## 2. Immutability Helper

- 객체나 배열을 좀 더 쉽게 수정하게 해준다.
- 이것을 사용하기 위해서는 라이브러리를 사전 설치해줘야 한다.
- 설치 방법 : npm을 통한 설치
- $npm install --save react-addons-update
- import update from 'react-addons-update'

- 원소 추가

```
this.setState({
    list: update(
        this.state.list,
        {
            $push: [newObj, newObj2]
        }
    );
});
```

- (줄 3) 첫 번째 인수 : 처리해야할 객체나 배열
- (줄 4~6) 두 번째 인수 : 처리명령을 지니고 있는 객체
- (줄 5) push를 통하여 list 배열에 newObj, newObj2를 추가

- 원소 제거

```
this.setState({
    list: update(
        this.state.list,
        {
            $splice: [[index, 1]]
        }
    );
});
```

- (줄 5) index번째 아이템 부터 시작해서 1개의 데이터를 제거한다는 의미

- 원소 수정

```
this.setState({
    list: update(
        this.state.list,
        {
            [index]: {
                field: {$set: "value"},
                field2: {$set: "value2"}
            }
        }
    );
});
```

- (줄 5~8) index번째 아이템의 field, field2 값을 변경한다.

- 객체를 다룰 때에도 직접 접근하면 안된다.

```
let object = {
    a: '1',
    b: '2',
    c: {
        d: '3',
        e: '4',
        f: {
            change_this_value: '0',
            this_stays_same: '6'
        }
    }
}

let changed = update(object, {
    c: {
        f: {
            change_this_value: {
                $set: '5'
            }
        }
    }
}

```

- (줄 14~22) change_this_value값이 수정된다.

## 3. spread 연산자

- 사용하기 위해서는 라이브러리를 설치해줘야 한다.
- $npm install --save babel-preset-stage-0
- webpack.config.js 파일을 아래와 같이 수정해야 한다.

```
module:{
        loaders: [
            {
                test: /.js$/,
                loader: 'babel',
                exclude: /node_modules/,
                query: {
                    cacheDirectory: true,
                    presets: ['es2015', 'stage-0', 'react'],
                    plugins: ["react-hot-loader/babel"]
                }
            }
        ]
},

```

- spread 연산자를 이용하여 값을 수정

```
let object = {
    a: '1',
    b: '2',
    c: {
        d: '3',
        e: '4',
        f: {
            change_this_value: '0',
            this_stays_same: '6'
        }
    }
}

let changed = {
    ...object,
    b: "hi"
};
```

- (줄 14~17) b의 값이 수정된다.

- 값 수정의 또 다른 예시

```
let object = {
    a: '1',
    b: '2',
    c: {
        d: '3',
        e: '4',
        f: {
            change_this_value: '0',
            this_stays_same: '6'
        }
    }
}

let changed = {
    ...object,
    c: {
        ...object.c,
        f: {
            ...object.c.f,
            change_this_value: '5'
        }
    }
};
```

- (줄 14~23) change_this_value값이 수정된다

- 배열 원소 추가
- 배열에서도 마찬가지로 spread 연산자 이용이 가능하다.

```
let array = [1, 2, 3, 4, 5, 6];
let changed = [ ...array, 7];
```

- changed 배열을 출력해보면 [1, 2, 3, 4, 5, 6, 7] 로 출력된다.

- 배열 원소 제거

```
let array = [1, 2, 3, 4, 5, 6];
let changed = [ ...array.slice(0,2), ...array.slice(3,array.length)];
```

- changed 배열을 출력해보면 3이 제거되어 [1, 2, 4, 5, 6] 로 출력된다.

- 배열 원소 수정

```
let array = [1, 2, 3, 4, 5, 6];
let changed = [ ...array.slice(0,2), '수정', ...array.slice(3,array.length-1)];
```

- changed 배열을 출력해보면 [1, 2, "수정", 4, 5, 6] 로 출력된다.
