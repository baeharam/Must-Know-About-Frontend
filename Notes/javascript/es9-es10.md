# ES9 (ES2018) ~ ES10 (ES2019) 의 특징들

## ES9 (ES2018)

### async 반복자

기존 반복자(Iterator)의 경우 `next()` 메서드는 `value` 와 `done` 을 가진 객체를 리턴했지만 각각이 Promise로 감싸진 Promise 객체를 리턴할 수도 있게 되었다.

```javascript
const asyncIterator = function() {
  let num = 3;
  return {
    next() {
      if (num) {
        return Promise.resolve({
          value: num--,
          done: false,
        });
      } else {
        return Promise.resolve({ 
          done: true 
        });
      }
    }
  }
}

const iterator = asyncIterator();

(async function() {
  await iterator.next().then(console.log); // { value: 3, done: false }
  await iterator.next().then(console.log); // { value: 2, done: false }
  await iterator.next().then(console.log); // { value: 1, done: false }
  await iterator.next().then(console.log); // { done: true }
})();
```

### Object rest/spread 문법

배열에서 사용되던 rest/spread 문법이 객체에서도 사용가능하게 되었다.

```javascript
const obj = { one: 1, two: 2, three: 3 };
const { one, ...rest } = obj;
const newObj = { ...rest, four: 4 };
console.log(rest, newObj); // { two: 2, three: 3 } { two: 2, three: 3, four: 4 }
```

### `Promise.prototype.finally`

Promise 객체를 `then` 이나 `catch` 로 처리한 후에 try-catch 문처럼 `finally` 를 쓸 수 있게 되었다.

```javascript
const timeout = () => {
  return new Promise((res) => {
    setTimeout(() => { res("Promise 끝"); }, 1000);
  });
};

timeout()
.then(console.log)
.finally(() => console.log("무조건"));
```

<br>

## ES10 (ES2019)

### `Array.prototype.flat()/flatMap()`

배열안에 배열 혹은 비어있는 원소가 있을 때 하나의 배열로 합쳐주는 메서드가 `flat` 이고 `map` 을 한 다음에 `flat` 하는 메서드가 `flatMap` 이다.

```javascript
const arr = [[1,2,3], 4, , 5];

console.log(arr.flat()); // [ 1, 2, 3, 4, 5 ]

console.log(arr.flatMap(a => {
  if (a instanceof Array) {
    return a.length;
  } else if (Number.isInteger(a)) {
    return a*2;
  } else {
    return undefined;
  }
})); // [ 3, 8, 10 ]
```

### `Object.fromEntries()`

`Object.entries` 와는 반대로 key/value 쌍의 배열로부터 객체를 만드는 메서드이다.

```javascript
const arr = [['one', 1], ['two', 2], ['three', 3]];
console.log(Object.fromEntries(arr)); // { one: 1, two: 2, three: 3 }
```

### `String.prototype.trimStart()/trimEnd()`

앞/뒤의 공백을 지우는 메서드로, 기존에 `String.prototype.trimLeft/trimRight` 이 있지만 `String.prototype.padStart/padEnd` 와 일치시키기 위해 나왔다.

```javascript
const target = "    target    ";
console.log(target.trimStart());
console.log(target.trimEnd());
```

```
target
    target
```

### `Symbol.prototype.description`

심볼을 정의할 때 디버깅 목적으로 문자열을 인자로 전달하여 만들기도 하는데 이를 보기 위한 프로퍼티이다.

```javascript
const symbol = Symbol('description');
console.log(symbol.description);
```

### catch의 에러인자 생략 가능

try-catch 문에서 catch의 인자로 에러인자가 오는데 이를 사용하지 않는다면 생략가능하다.

```javascript
try { console.log('try'); } catch {} // try
```

<br>

## 참고

* [ECMAScript-new-feature-list, ES2018](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2018.MD)
* [ECMAScript-new-feature-list, ES2019](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2019.MD)
* [ZeroCho님, ES2019(ES10)의 변화](https://www.zerocho.com/category/ECMAScript/post/5c909bfe5a8005001ffb3f14)