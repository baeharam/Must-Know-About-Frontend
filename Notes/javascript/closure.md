# 클로저(Closure)

클로저란 **함수가 속한 렉시컬 스코프를 기억하여 함수가 렉시컬 스코프 밖에서 실행될 때도 그 스코프에 접근할 수 있게 하는 기능** 을 말한다.

```javascript
function outer() {
  var a = 2;
  function inner() {
    console.log(a);
  }
  return inner;
}

var func = outer();
func(); // 2
```

여기서 GC(Garbage Collector)가 `outer()` 의 참조를 없앨 것 같지만 내부함수인 `inner()` 가 해당 스코프의 변수인 a를 참조하고 있기 때문에 없애지 않는다. 따라서 스코프 외부에서 `inner()` 가 실행되도 해당 스코프를 기억하기 때문에 2를 출력하게 된다. 즉, 여기서 클로저는 `inner()` 가 되며 `func` 에 담겨 밖에서도 실행되고 렉시컬 스코프를 기억한다.

<br>

## 예제

클로저를 사용하는 대표적인 예제는 역시 "반복문 클로저"이다.

```javascript
function func() {
  for (var i=1; i<5; i++) {
    setTimeout(function() { console.log(i); }, i*500);
  }
}
func(); // 5 5 5 5
```

코드의 의도한 바는 1부터 4까지 간격을 두고 출력하는 것이었지만 5가 4번 출력된다. 왜 이렇게 되는 것일까?  

`setTimeout()` 을 반복문 안에서 돌리면 콜백함수가 계속해서 task queue에 쌓이게 되고 반복문이 끝나고 나서 call stack으로 돌아와서 실행된다. 콜백함수는 클로저이기 때문에 상위 스코프에게 `i` 의 값을 물어보고 상위 스코프인 `func` 의 스코프에선 `i` 가 5까지 증가했기 때문에 5가 4번 출력된다.

<br>

## 해결방법

위 문제를 해결하기 위해선 2가지 방법이 있다.

* **새로운 함수 스코프로 해결하기**

```javascript
function func() {
  for (var i=1; i<5; i++) {
    (function (j) { 
      setTimeout(function() { console.log(j); }, j*500);
    })(i);
  }
}
func(); // 1 2 3 4
```

`setTimeout()` 을 IIFE(Immediately Invoked Function Expression, 즉시실행함수 표현식)로 감싸게 되면, 새로운 스코프를 형성하고 나중에 콜백함수가 `j` 를 참조할 때 그 시점의 `i` 값을 갖기 때문에 원하는 결과를 얻을 수 있게 된다.

* **블록 스코프로 해결하기**

```javascript
function func() {
  for (let i=1; i<5; i++) {
    setTimeout(function() { console.log(i); }, i*500);
  }
}
func(); // 1 2 3 4
```

함수 스코프가 아닌 블록 스코프를 갖는 `let` 을 사용하면 `for` 문 내의 새로운 스코프를 갖기 때문에 매 반복마다 새로운 `i` 가 선언되고 반복이 끝난 이후의 값으로 초기화가 된다. 따라서, `setTimeout()` 의 클로저인 콜백함수가 `i` 를 참조하기 위해 상위 스코프를 검색할 때 블록 스코프에서 매 반복마다 선언 및 초기화 된 `i` 를 참조하는 것이다.

실제 클로저를 사용하는 예를 알고 싶다면 [Stackoverflow의 답변](https://stackoverflow.com/a/39045098/11789111) 을 참고하자.

<br>

## 참고

* [TOAST, 자바스크립트의 스코프와 클로저](https://meetup.toast.com/posts/86)
* 카일 심슨, 『You don't know JS - 타입과 문법, 스코프와 클로저』, 최병현, 한빛미디어(2017)