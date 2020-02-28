# var vs let vs const

모두 변수를 선언하는 키워드라는 것은 동일하다. 하지만, let과 const는 ES2015(ES6)에서 등장했고 여러가지 다른 특성을 갖는다.

## 스코프 규칙

> 스코프의 개념을 모른다면 [스코프](https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/Javascript/scope.md) 를 보고 오자.

* var는 함수 스코프를 갖는다.
* let과 const는 블록 스코프를 갖는다.

```javascript
function run() {
  var foo = "Foo";
  let bar = "Bar";

  console.log(foo, bar);

  {
    let baz = "Bazz";
    console.log(baz);
  }

  console.log(baz); // ReferenceError
}

run();
```

따라서, 위 코드를 실행했을 때 블록 안에 있는 `baz` 를 출력하게 되면 ReferenceError가 발생하는 것이다.

<br>

## 호이스팅

> 호이스팅의 개념을 모른다면 [호이스팅](https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/Javascript/Hoisting.md) 을 보고 오자.

* var는 **함수 스코프의 최상단으로 호이스팅** 되고 선언과 동시에 `undefined` 로 초기화 된다.
* let과 const는 **블록 스코프의 최상단으로 호이스팅** 되고 선언만 되고 값이 할당되기 전까지 어떤 값으로도 초기화되지 않는다.

```javascript
function run() {
  console.log(foo); // undefined
  var foo = "Foo";
  console.log(foo); // Foo
}

run();
```

따라서, var의 경우 위와 같이 선언 전에 출력하면 `undefined` 가 출력된다.

```javascript
function checkHoisting() {
  console.log(foo); // ReferenceError
  let foo = "Foo";
  console.log(foo); // Foo
}

checkHoisting();
```

반면에, let의 경우는 선언 전에 호이스팅 되긴 하지만 어떤 값도 가지지 않기 때문에 ReferenceError가 발생한다. 이런 현상을 **TDZ(Temporal Dead Zone)** 라고 한다. 즉, 선언은 되었지만 참조는 할 수 없는 사각지대를 갖는 것이다.

<br>

## 글로벌 객체로의 바인딩

**strict mode가 아니라는 가정 하에,**

* var는 글로벌 스코프에서 선언되었을 경우 글로벌 객체에 바인딩된다.
* let과 const는 글로벌 스코프에서 선언되었을 경우 글로벌 객체에 바인딩되지 않는다.

```javascript
var foo = "Foo";  // globally scoped
let bar = "Bar"; // globally scoped

console.log(window.foo); // Foo
console.log(window.bar); // undefined
```

브라우저 환경에서 글로벌 객체는 `window` 인데, var의 경우 바인딩이 되었고 let의 경우는 되지 않았다는 걸 볼 수 있다.

<br>

## 재선언 (Redeclaration)

* var는 재선언이 가능하다.
* let과 const는 재선언이 불가능하다.

```javascript
var foo = "foo1";
var foo = "foo2"; // 문제없음

let bar = "bar1";
let bar = "bar2"; // SyntaxError: Identifier 'bar' has already been declared
```

<br>

## let vs const

* var와 let은 재할당이 가능하다.
* const는 선언과 초기화가 반드시 동시에 일어나야 하며 재할당이 불가능하다. 즉, 상수와 같은 고정값을 선언할 때 사용하는 키워드이다.

<br>

## 참고

* [Stackoverflow, What's the difference between using “let” and “var”?](https://stackoverflow.com/questions/762011/whats-the-difference-between-using-let-and-var)
* [Stackoverflow, Are variables declared with let or const not hoisted in ES6?](https://stackoverflow.com/questions/31219420/are-variables-declared-with-let-or-const-not-hoisted-in-es6)
* [PoiemaWeb, let, const](https://poiemaweb.com/es6-block-scope)

