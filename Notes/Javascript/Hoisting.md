# 호이스팅(Hoisting)

> [스코프](https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/Javascript/scope.md) 의 개념을 이해하지 못했다면 이해하고 오자.

호이스팅이란 "끌어올린다" 라는 뜻으로 **변수 및 함수 선언문이 스코프 내의 최상단으로 끌어올려지는 현상** 을 말한다. 여기서 주의할 점은 **"선언문"** 이라는 것이며 "대입문"은 끌어올려지지 않는다. 아래 코드를 보자.

```javascript
console.log(a);
var a = 2;
```

컴파일러는 자바스크립트 엔진이 인터프리팅(Interpreting)을 하기 전에 컴파일을 하는데 이 때, `var a = 2;` 를 2개의 구문으로 본다.

* `var a`
* `a = 2`

`var a` 는 변수 선언문으로 컴파일을 할 때 처리하고, `a = 2` 는 실행할 때까지 내버려둔다. 따라서, 변수 a는 호이스팅 되고 콘솔에는 다음과 같은 결과가 나온다.

```javascript
undefined
```

함수 선언문의 경우도 호이스팅 된다.

```javascript
func();
function func() { console.log('함수 호이스팅'); }
```

```
함수 호이스팅
```

<br>

## 함수 호이스팅에서 주의할 점

함수 호이스팅에서 주의할 점이 더 있다.

* **함수 표현식(Function Expression)은 호이스팅 되지 않는다.**

```javascript
func();
var func = function() {}
```

여기서는 변수 func의 호이스팅이 발생해서 참조할 수는 있기 때문에 ReferenceError가 발생하지 않지만 그 값이 `undefined` 이기 때문에 TypeError가 발생한다.

* **함수와 변수 선언문 중에는 함수 선언문이 먼저다.**

```javascript
func();
var func = function(){ console.log('변수 호이스팅') }
function func() {
  console.log('함수 호이스팅');
}
```

동일한 이름으로 함수 선언문과 변수 선언문(= 함수표현식)이 있지만 함수 선언문의 호이스팅이 먼저이기 때문에 결과는 다음과 같다.

```
함수 호이스팅
```

<br>

## 참고

* [You don't know JS, Scope and Closures : Chapter 5: The (not so) Secret Lifecycle of Variables](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch5.md)