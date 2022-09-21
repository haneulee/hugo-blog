---
title: "Singleton 싱글턴 패턴"
date: 2022-09-21T19:00:39+02:00
categories:
  - development
  - pattern
tags:
  - development
  - front-end
  - pattern
  - singleton
  - javascript
  - design pattern
  - 싱글턴
  - 패턴
  - 자바스크립트
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: "https://res.cloudinary.com/dtlpko2wf/image/upload/v1663783683/blog/singleton_y4xvfl.png"
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

![](https://res.cloudinary.com/dtlpko2wf/image/upload/v1663783683/blog/singleton_y4xvfl.png)

# Singleton 싱글턴 패턴

{{< alert info >}}
이 글은 [https://www.patterns.dev/posts/singleton-pattern/](https://www.patterns.dev/posts/singleton-pattern/)의 한글 번역본입니다.
{{< /alert >}}

<!--adsense-->

`singleton pattern : 애플리케이션 전체에서 단일 글로벌 인스턴스 공유`

싱글톤은 한 번 인스턴스화할 수 있고 전역적으로 액세스할 수 있는 클래스입니다.  
이 단일 인스턴스는 응용 프로그램 전체에서 공유할 수 있으므로 Singleton은 응용 프로그램의 전역 상태를 관리하는 데 적합합니다.

먼저 ES2015 클래스를 사용하여 싱글톤이 어떻게 생겼는지 살펴보겠습니다. 이 예제에서는 다음을 포함하는 Counter 클래스를 만들 것입니다.

- `getInstance` 인스턴스의 값을 반환 하는 메소드
- `getCount` counter 변수의 현재 값을 반환 하는 메소드
- `increment` counter의 값을 1씩 증가 시키는 메소드
- `decrement` counter의 값을 1씩 감소 시키는 메소드

```
let counter = 0;

class Counter {
  getInstance() {
    return this;
  }

  getCount() {
    return counter;
  }

  increment() {
    return ++counter;
  }

  decrement() {
    return --counter;
  }
}
```

그러나 이 클래스는 Singleton의 기준을 충족하지 않습니다!  
Singleton은 한 번만 인스턴스화 될 수 있어야 합니다.  
현재는 Counter 클래스의 여러 인스턴스를 만들 수 있습니다.

```
let counter = 0;

class Counter {
  getInstance() {
    return this;
  }

  getCount() {
    return counter;
  }

  increment() {
    return ++counter;
  }

  decrement() {
    return --counter;
  }
}

const counter1 = new Counter();
const counter2 = new Counter();

console.log(counter1.getInstance() === counter2.getInstance()); // false
```

new 메소드를 두 번 호출하여 다른 인스턴스와 동일하게 counter1, counter2를 설정합니다.  
counter1과 counter2의 getInstance 메서드에서 반환된 값들은 다른 인스턴스에 대한 참조를 효과적으로 반환했습니다.  
두 값은 완전히 동일하지 않습니다!

<video src="https://res.cloudinary.com/ddxwdqwkr/video/upload/v1609056519/patterns.dev/jspat-52_zkwyk1.mp4">

Counter 클래스의 인스턴스를 하나만 만들 수 있는지 확인합시다.

인스턴스를 하나만 만들 수 있도록 하는 한 가지 방법은 `instance`이라는 변수를 만드는 것입니다.  
Counter의 생성자에서 새 인스턴스가 생성될 때 인스턴스에 대한 참조와 동일하게 `instance`를 설정할 수 있습니다.  
instance 변수에 이미 값이 있는지 확인하여 새로운 인스턴스화를 방지할 수 있습니다.  
이 경우 인스턴스가 이미 존재합니다.  
이것은 발생하지 않아야 합니다.(사용자에게 알리기 위해 오류가 발생해야 합니다.)

```
let instance;
let counter = 0;

class Counter {
  constructor() {
    if (instance) {
      throw new Error("You can only create one instance!");
    }
    instance = this;
  }

  getInstance() {
    return this;
  }

  getCount() {
    return counter;
  }

  increment() {
    return ++counter;
  }

  decrement() {
    return --counter;
  }
}

const counter1 = new Counter();
const counter2 = new Counter();
// Error: You can only create one instance!
```

완벽하다! 더 이상 여러 인스턴스를 만들 수 없습니다.

Counter.js 파일에서 Counter 인스턴스를 내보내겠습니다.  
그러나 그렇게하기 전에 우리는 인스턴스 또한 동결해야 합니다.  
이 `Object.freeze` 방법은 사용하는 코드가 Singleton을 수정할 수 없도록 합니다.  
고정된 인스턴스의 속성은 추가하거나 수정할 수 없으므로 실수로 Singleton의 값을 덮어쓸 위험이 줄어듭니다.

```
let instance;
let counter = 0;

class Counter {
  constructor() {
    if (instance) {
      throw new Error("You can only create one instance!");
    }
    instance = this;
  }

  getInstance() {
    return this;
  }

  getCount() {
    return counter;
  }

  increment() {
    return ++counter;
  }

  decrement() {
    return --counter;
  }
}

const singletonCounter = Object.freeze(new Counter());
export default singletonCounter;
```

Counter 예제를 구현하는 응용 프로그램을 살펴보겠습니다.  
다음 파일이 있습니다.

- `counter.js`: Counter클래스를 포함하고 Counter 인스턴스를 기본 내보냅니다.
- `index.js`: redButton.js 및 blueButton.js모듈을 로드합니다.
- `redButton.js`: Counter를 가져오고 Counter의 increment 메서드를 빨간색 버튼에 대한 이벤트 리스너로 추가 합니다. getCount 메서드 를 호출하여 Counter의 현재 값을 기록합니다.
- `blueButton.js`: Counter를 가져오고 Counter의 increment 메서드를 파란색 버튼에 대한 이벤트 리스너로 추가 합니다. getCounte 메서드를 호출하여 Counter의 현재 값을 기록합니다.

blueButton.js, redButton.js 둘 다 counter.js에서 동일한 인스턴스를 가져옵니다.  
이 인스턴스는 두 파일 모두에서 Counter로 가져옵니다.

<video src="https://res.cloudinary.com/ddxwdqwkr/video/upload/v1609056519/patterns.dev/jspat-56_wylvcf.mp4">

redButton.js 또는 blueButton.js에서 increment메서드를 호출하면 Counter 인스턴스의 counter속성 값이 두 파일 모두에서 업데이트됩니다.  
빨간색 버튼을 클릭하든 파란색 버튼을 클릭하든 상관없습니다. : 모든 인스턴스에서 동일한 값을 공유합니다.  
이것이 다른 파일에서 메서드를 호출하더라도 카운터가 계속 1씩 증가하는 이유입니다.

---

## (단)장점

인스턴스화를 한 인스턴스로만 제한하면 잠재적으로 많은 메모리 공간을 절약할 수 있습니다.  
매번 새 인스턴스에 대한 메모리를 설정하는 대신 애플리케이션 전체에서 참조되는 해당 인스턴스에 대한 메모리만 설정하면 됩니다.  
그러나 싱글톤은 실제로 안티 패턴 으로 간주 되며 JavaScript에서 피할 수 있습니다(또는.. 해야 합니다 ).

Java 또는 C++와 같은 많은 프로그래밍 언어에서는 JavaScript에서 할 수 있는 방식으로 객체를 직접 생성할 수 없습니다.  
이러한 객체 지향 프로그래밍 언어에서는 객체를 생성하는 클래스를 생성해야 합니다.  
생성된 객체는 JavaScript 예제 instance 값과 마찬가지로 클래스의 인스턴스 값을 가집니다.

그러나 위의 예에 표시된 클래스 구현은 실제로 과도합니다.  
JavaScript에서 직접 객체를 생성할 수 있으므로 일반 객체를 사용하여 정확히 동일한 결과를 얻을 수 있습니다.  
Singleton 사용의 몇 가지 단점을 살펴보겠습니다!

### 일반 객체 사용

이전에 본 것과 동일한 예를 사용하겠습니다.  
그러나 이번에는 counter가 단순히 다음을 포함하는 객체입니다.

- count 프로퍼티
- count의 값을 1씩 증가 시키는 increment 메소드
- count의 값을 1씩 감소 시키는 decrement 메소드

```
let count = 0;

const counter = {
  increment() {
    return ++count;
  },
  decrement() {
    return --count;
  }
};

Object.freeze(counter);
export { counter };
```

객체는 참조로 전달되므로 redButton.js, blueButton.js 둘 다 동일한 counter 객체에 대한 참조를 가져옵니다.  
이 파일 중 하나에서 count의 값을 수정하면 두 파일에서 모두 볼 수 있는 counter의 값이 수정됩니다.

## 테스트

Singleton에 의존하는 테스트 코드는 까다로울 수 있습니다. 매번 새로운 인스턴스를 생성할 수 없기 때문에 모든 테스트는 이전 테스트의 전역 인스턴스 수정에 의존합니다. 이 경우 테스트 순서가 중요하며 한 번의 작은 수정으로 전체 테스트가 실패할 수 있습니다. 테스트 후에 테스트에서 수정한 사항을 재설정하려면 전체 인스턴스를 재설정해야 합니다.

```
//test.js

import Counter from "../src/counterTest";

test("incrementing 1 time should be 1", () => {
  Counter.increment();
  expect(Counter.getCount()).toBe(1);
});

test("incrementing 3 extra times should be 4", () => {
  Counter.increment();
  Counter.increment();
  Counter.increment();
  expect(Counter.getCount()).toBe(4);
});

test("decrementing 1  times should be 3", () => {
  Counter.decrement();
  expect(Counter.getCount()).toBe(3);
});

//superCounter.js
import Counter from "./counter";

export default class SuperCounter {
  constructor() {
    this.count = 0;
  }

  increment() {
    Counter.increment();
    return (this.count += 100);
  }

  decrement() {
    Counter.decrement();
    return (this.count -= 100);
  }
}
```

### 의존성 은닉

다른 모듈을 가져올 때, superCounter.js에서 모듈이 Singleton을 가져오는지 명확하지 않을 수 있습니다. 이 경우 index.js와 같은 다른 파일에서는 해당 모듈을 가져오고 해당 메서드를 호출할 수 있습니다. 이런 식으로 우리는 실수로 Singleton의 값을 수정합니다. 이는 응용 프로그램 전체에서 Singleton의 여러 인스턴스를 공유할 수 있고 모두 수정될 수 있기 때문에 예기치 않은 동작으로 이어질 수 있습니다.

```
//test.js
import Counter from "../src/counterTest";

test("incrementing 1 time should be 1", () => {
  Counter.increment();
  expect(Counter.getCount()).toBe(1);
});

test("incrementing 3 extra times should be 4", () => {
  Counter.increment();
  Counter.increment();
  Counter.increment();
  expect(Counter.getCount()).toBe(4);
});

test("decrementing 1  times should be 3", () => {
  Counter.decrement();
  expect(Counter.getCount()).toBe(3);
});

//superCounter.js
import Counter from "./counter";

export default class SuperCounter {
  constructor() {
    this.count = 0;
  }

  increment() {
    Counter.increment();
    return (this.count += 100);
  }

  decrement() {
    Counter.decrement();
    return (this.count -= 100);
  }
}
```

## 글로벌 행동

Singleton 인스턴스는 전체 앱에서 참조될 수 있어야 합니다. 전역 변수는 본질적으로 동일한 동작을 보여줍니다. 전역 변수는 전역 범위에서 사용할 수 있으므로 응용 프로그램 전체에서 해당 변수에 액세스할 수 있습니다.

전역 변수를 갖는 것은 일반적으로 잘못된 설계 결정으로 간주됩니다. 전역 범위 오염은 실수로 전역 변수 값을 덮어쓰는 결과를 초래할 수 있으며, 이로 인해 많은 예기치 않은 동작이 발생할 수 있습니다.

ES2015 에서 전역 변수를 생성하는 것은 상당히 드문 일입니다. 새로운 `let` 및 `const`는 이 두 키워드로 선언된 변수를 블록 범위로 유지하여 개발자가 실수로 전역 범위를 오염시키는 것을 방지합니다. JavaScript 의 새 `module` 시스템은 모듈의 export값과 다른 파일의 import값을 사용할 수 있으므로 전역 범위를 오염시키지 않고 전역적으로 액세스 가능한 값을 더 쉽게 생성할 수 있습니다.

그러나 Singleton의 일반적인 사용 사례는 애플리케이션 전체에 일종의 전역 상태를 갖는 것입니다. 코드베이스의 여러 부분이 동일한 변경 가능한 객체에 의존하는 경우 예기치 않은 동작을 유발할 수 있습니다.

일반적으로 코드베이스의 특정 부분은 전역 상태 내의 값을 수정하는 반면 다른 부분은 해당 데이터를 사용합니다. 여기서 실행 순서가 중요합니다. : 우리는 소비할 데이터가 없을 때 실수로 데이터를 먼저 소비하는 것을 원하지 않습니다! 전역 상태를 사용할 때 데이터 흐름을 이해하는 것은 애플리케이션이 성장하고 수십 개의 구성 요소가 서로 의존함에 따라 매우 까다로울 수 있습니다.

## React의 상태 관리

React에서는 Singleton을 사용하는 대신 `Redux` 또는 `React Context` 와 같은 상태 관리 도구를 통해 전역 상태에 의존하는 경우가 많습니다. 전역 상태 동작이 Singleton의 동작과 유사해 보일 수 있지만 이러한 도구는 Singleton의 변경 가능한 상태가 아닌 `read-only state`를 제공합니다. Redux를 사용할 때, 컴포넌트가 디스패처를 통해 액션을 보낸 후에 순수 함수 리듀서가 state를 업데이트할 수 있습니다.

이런 도구들을 사용하여 전역 상태의 단점이 사라지지는 않지만, 컴포넌트가 state를 직접 업데이트할 수 없기 때문에 최소한 의도한 대로 전역 상태가 변경되도록 할 수 있습니다.

---

참고 :
[https://www.patterns.dev/posts/singleton-pattern/](https://www.patterns.dev/posts/singleton-pattern/)
[싱글턴 패턴 위키](https://ko.wikipedia.org/wiki/%EC%8B%B1%EA%B8%80%ED%84%B4_%ED%8C%A8%ED%84%B4)
