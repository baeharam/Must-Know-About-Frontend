# new의 동작방식

자바스크립트에선 `new` 연산자를 통해 함수를 생성자로 호출할 수 있고 그에따라 새로운 객체를 생성할 수 있다. 다음과 같은 과정으로 이루어진다.

* 빈 객체를 생성한다.
* `[[Prototype]]` 속성을 생성자 호출할 함수의 `prototype` 속성으로 지정한다.
  * 만약 함수의 `prototype` 속성이 원시값이라면 `Object.prototype` 으로 지정된다.
* 객체를 생성하고 이 객체를 `this` 로 지정한다.
* 함수를 호출하고 해당 함수의 `this` 로 위에서 지정한 객체를 사용한다.
* 함수의 리턴값이 원시값이라면 새로 만들어진 객체가 리턴되고 리턴값이 객체라면 해당 객체가 리턴된다.

이를 코드로 보면 다음과 같다.

```javascript
function Func() {}
const f = new Func();
```

* 빈 객체 생성 `{}`
* 해당 객체의 `[[Prototype]]` 을 `Func.prototype` 으로 지정
* 이 객체를 `this` 로 지정
* `Func()` 을 호출하고 이 함수에서 `this` 를 위 객체로 지정
* 함수의 리턴값이 `undefined` 원시값이므로 생성한 객체를 리턴

<br>

## 참고

* [Stackoverflow, What is the 'new' keyword in JavaScript?](https://stackoverflow.com/questions/1646698/what-is-the-new-keyword-in-javascript)
* [Stackoverflow, How does the new operator work in JavaScript?](https://stackoverflow.com/questions/6750880/how-does-the-new-operator-work-in-javascript)