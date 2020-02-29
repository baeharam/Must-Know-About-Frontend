# IIFE (Immediately-Invoked Function Expression)

IIFE는 직역하면 즉시-실행 함수 표현식이다. 즉, 2가지 조건을 지닌다.

* **즉시 실행하여야 한다.**
* **함수 표현식이어야 한다. ( = 함수 선언문이 아니어야 한다. )**

결국, 정의하자면 함수 표현식을 즉시 실행하는 것을 말하며 해당 함수는 **익명함수와 기명함수 모두 가능** 하다. 다음과 같이 만들 수 있다.

```javascript
(function(){ 
  console.log('IIFE'); 
})();
```

실행하면 바로 "IIFE"가 출력된다. 여기서 함수는 익명함수를 사용했고 괄호로 감쌌는데, 이것은 함수 표현식으로 만들겠다는 것으로 괄호로 감싸지 않으면 함수 선언문이 되기 때문이다.

<br>

## 2가지 형태와 화살표 함수

IIFE는 2가지 형태로 사용할 수 있다.

```javascript
(function(){ console.log('IIFE'); })();
(function(){ console.log('IIFE'); }());
```

더글라스 크락포드는 아래의 방식이 에러를 덜 발생시키는 표현이라고 선호하는데, 반대하는 개발자들도 있어서 **단순히 스타일의 차이** 로 인식하면 된다.

### 화살표 함수(Arrow Function)으로 사용

ES2015(ES6)에 등장한 화살표 함수를 사용해서도 IIFE를 만들 수 있다.

```javascript
(() => console.log('IIFE'))();
```

단, 주의할 점은 이 방식의 경우 크락포드가 선호하는 방식을 사용할 수 없다.

```javascript
(() => console.log('IIFE')());
```

위 코드는 동작하지 않는데, 그 이유는 함수를 호출하기 위해선 호출대상이 명세에서 말하는 *MemberExpression*이어야 한다. 그러나 화살표 함수의 경우 *AssignmentExpression* 이기 때문에 불가능한 것이다. 이게 무슨 말인지 모르겠다면 [스택오버플로우의 답변](https://stackoverflow.com/a/34589765/11789111) 을 참고하자.

<br>

## 사용 이유

IIFE를 사용하는 이유는, 보통 전역 스코프(Global Scope)를 오염시키지 않기 위해서 사용한다. 즉, 변수를 전역 스코프에 선언하는 것을 피하기 위함이다. 이런 기법이 다음과 같은 상황에 이용된다.

### 클로저와 private 데이터

IIFE안에서 클로저를 생성하면 private 데이터를 만들 수 있고 외부에서 접근할 수 없다.

```javascript
const getCount = (function(){
  let count = 1;
  return function() {
    ++count;
    return count;
  }
})();

console.log(getCount()); // 2
console.log(getCount()); // 3
```

IIFE안의 익명함수는 클로저가 되고 변수 `count` 는 private 데이터가 되므로 밖에 보여지지 않는다. 흔히 말하는 모듈 패턴이 바로 이 방식에 의존한다.

### 변수의 별칭(alias)

예를 들어, 동일한 전역 변수를 갖는 2개의 라이브러리를 사용한다고 했을 때 충돌을 해결하기 위해 사용할 수도 있다. jQuery의 경우 `$` 라는 전역 변수를 갖는데 이를 갖는 또 다른 라이브러리가 있다고 하면 다음과 같이 해결할 수 있다.

```javascript
window.$ = funciton(){};
(function($){...})(jQuery);
```

### 최소화(Minification)를 활용한 최적화(Optimization)

[UglifyJS](https://github.com/mishoo/UglifyJS2) 와 같은 라이브러리는 최소화를 통해서 최적화를 하는데, 여기에는 변수명을 짧게 만드는 것도 포함한다.

```javascript
(function(window, document, undefined) {...})(window, document);
```

위와 같은 IIFE가 있다고 하면, 다음과 같이 줄일 수 있다.

```javascript
(function(w, d, u) {...})(window, document);
```

이를 통해 파일의 크기를 줄일 수 있게 된다.

<br>

## 참고

* [Explain the encapsulated anonymous function syntax](https://stackoverflow.com/questions/1634268/explain-the-encapsulated-anonymous-function-syntax)
* [What is the practical use of an IIFE with a name?](https://stackoverflow.com/questions/18365801/what-is-the-practical-use-of-an-iife-with-a-name)
* [Use Cases for JavaScript's IIFEs](https://mariusschulz.com/blog/use-cases-for-javascripts-iifes)
* [What is the (function() { } )() construct in JavaScript?](https://stackoverflow.com/questions/8228281/what-is-the-function-construct-in-javascript)