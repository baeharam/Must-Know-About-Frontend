# ES7 (ES2016) ~ ES8 (ES2017) 의 특징들

## ES7 (ES2016)

### `Array.prototype.includes`

* `arr.includes(찾는원소, [, 인덱스시작점])`

특정 원소를 포함했는지의 여부를 반환하는 메서드이다. 첫번째 인자로는 타겟 원소를, 두번째 인자로는 어느 인덱스부터 검사할 것인지를 줄 수 있다.

```javascript
[1, 2, 3].includes(2); // true
[1, 2, NaN].includes(NaN); // true
[1, 2, 3].includes(2,2); // 인덱스 2부터 시작하는데 3밖에 없으므로 false
[1, 2, 3].includes(3,4); // 인덱스 범위 넘어가면 자동 false
```

### 멱법(Exponentiation)

* `피연산자 ** 피연산자`

숫자를 제곱하는 방법을 말하며 이를 짧게 나타냈다.

```javascript
2 ** 2; // 4
Math.pow(2, 2); // 4
```

<br>

## ES8 (ES2017)

### `async - await`

* `async function 함수이름 (매개변수들...) {}`

비동기 함수를 보다 직관적으로 사용하는 문법으로 함수 앞에 `async` 키워드를 달면 내부에서 `await` 을 사용하여 Promise 객체의 완료를 기다릴 수 있다.

```javascript
const promiseFunc1 = function() {
  return new Promise((res, rej) => {
    setTimeout(() => {
      res("첫번째 Promise 끝");
    }, 1000);
  });
};

const promiseFunc2 = function() {
  return new Promise((res, rej) => {
    setTimeout(() => {
      res("두번째 Promise 끝");
    }, 1000);
  });
};

const handleAsyncFunc = async function() {
  const promiseMessage1 = await promiseFunc1();
  const promiseMessage2 = await promiseFunc2();
  console.log(promiseMessage1, promiseMessage2);
};

handleAsyncFunc(); // 첫번째 Promise 끝 두번째 Promise 끝
```

### `Object.entries()`

* `Object.entries(객체)`

key/value 쌍을 배열로 가져오는 메서드이다.

```javascript
const obj = { one: 1, two: 2, three: 3 };
console.log(Object.entries(obj));
// [['one', 1], ['two', 2], ['three', 3]]
```

### `Object.values()`

* `Object.values(객체)`

value 만 배열로 가져오는 메서드이다.

```javascript
const obj = { one: 1, two: 2, three: 3 };
console.log(Object.values(obj));
// [1, 2, 3]
```

### `Object.getOwnPropertyDescriptors()`

* `Object.getOwnPropertyDescriptors(객체)`

모든 프로퍼티의 디스크립터인 `value`, `writable`, `enumerable`, `configurable`, `set`, `get` 을 가져오는 메서드이다.

```javascript
const obj = { one: 1, two: 2, three: 3 };
console.log(Object.getOwnPropertyDescriptors(obj));
```

```
{
  one: { value: 1, writable: true, enumerable: true, configurable: true },
  two: { value: 2, writable: true, enumerable: true, configurable: true },
  three: { value: 3, writable: true, enumerable: true, configurable: true }
}
```

### Trailing 콤마

함수 선언문, 함수 호출에서 마지막에도 콤마를 쓸 수 있다.

```javascript
function test(a,b,){
  console.log(a,b,);
}
```

<br>

## 참고

* [ECMAScript-new-feature-list, ES2016](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2016.MD)
* [ECMAScript-new-feature-list, ES2017](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2017.MD)