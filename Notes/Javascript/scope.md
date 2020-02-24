# 스코프

스코프란 자바스크립트에서 할당을 받을 변수 혹은 값으로 참조하는 변수를 사용할 때 그 변수가 어디있는지 검색해야 하는데, 그 때 검색을 하기 위한 규칙의 집합이다.

<br>

## 렉시컬 스코프

자바스크립트는 컴파일러가 토크나이징(Tokenizing)으로 토큰을 분리하고 **렉싱(Lexing) 으로 토큰에 의미를 부여할 때 스코프를 정하는** 렉시컬 스코프를 사용한다. 즉, 변수 혹은 함수가 선언되는 위치를 기반으로 스코프가 형성된다. 렉시컬 스코프로 변수를 찾을 때는 다음과 같은 과정을 거친다.

1. 현재 스코프에 원하는 변수가 있는가? → 있다면 해당 변수를 참조하고 끝난다.
2. 상위 스코프에 원하는 변수가 있는가? → 있다면 해당 변수를 참조하고 끝난다.
3. 계속 상위 스코프로 이동하다가 글로벌 스코프를 만나게 되면, 해당 변수가 있든 없든 끝이 난다.

<br>

## 스코프 체인

위와 같이 상위 스코프를 검색할 수 있는 이유는 각각의 **실행 컨텍스트(Execution Context, EC)** 에 `[[Scopes]]` 로 **스코프 체인(Scope Chain)** 이 형성되고 서로 연결되기 때문이다. 아래 코드의 스코프 체인을 보자.

```javascript
var a = 1;
function func1() {
  var b = 2;
  function func2() {
    console.log(a+b);
  }
  func2();
}
func1();
```

`func2` 에서 a와 b를 검색할 때 다음과 같이 검색한다.

1. func2의 스코프에서 a와 b를 검색하는데 없기 때문에 상위 스코프인 func1으로 간다.
2. func1에서 b를 발견했다! 하지만 a를 못 찾았으니 상위 스코프인 글로벌 스코프로 간다.
3. 글로벌 스코프에서 a를 발견했다!
4. 합인 3을 출력하고 마친다.

이걸 그림으로 보면 다음과 같다.

<img src="../../images/scope chain.png" width="400px">

(여기서 VO(Variable Object)와 AO(Activation Object) 개념을 이해하기 위해선 실행 컨텍스트 개념을 이해해야 하니 모른다면 공부하고 오자.)

<br>

## 참조

* [You don't know JS, Scope and Closures](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch1.md)