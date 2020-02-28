# 스코프

> [Execution Context](https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/Javascript/Execution%20Context.md) 를 모른다면 보고 오도록 하자.

스코프란 자바스크립트에서 할당을 받을 변수 혹은 값으로 참조하는 변수를 사용할 때 그 변수가 어디있는지 검색해야 하는데, 그 때 검색을 하기 위한 규칙의 집합이다.

<br>

## 렉시컬 스코프

자바스크립트는 컴파일러가 토크나이징(Tokenizing)으로 토큰을 분리하고 **렉싱(Lexing) 으로 토큰에 의미를 부여할 때 스코프를 정하는** 렉시컬 스코프를 사용한다. 즉, 변수 혹은 함수가 선언되는 위치를 기반으로 스코프가 형성된다. 렉시컬 스코프로 식별자를 찾을 때는 다음과 같은 과정을 거친다.

1. 현재 스코프에 원하는 식별자가 있는가? → 있다면 해당 식별자를 참조하고 끝난다.
2. 상위 스코프에 원하는 식별자가 있는가? → 있다면 해당 식별자를 참조하고 끝난다.
3. 계속 상위 스코프로 이동하다가 글로벌 스코프를 만나게 되면, 해당 식별자가 있든 없든 끝이 난다.

<br>

## 스코프 체인

위에서 설명한 것과 같이 상위 스코프를 찾아가기 위해선, 그에 대한 참조가 있어야 한다. 이 참조는 EC(Execution Context)에서 말했던 Lexical/Variable Environment에 있다. 각 EC는 Lexical/Variable Environment를 갖고 있고, 그 안에 각각 Environment Record와 outer 포인터를 갖는다. **여기서 outer 포인터가 바로 상위 스코프를 참조하는 요소이다.** 따라서, 스코프 체인은 다음과 같이 동작한다.

* 현재 EC의 Lexical/Variable Environment의 Environment Record에서 해당 식별자를 찾는다.
* 없으면, outer 포인터를 통해 외부의 Lexical/Variable Environment를 보고 Environment Record에서 다시 해당 식별자를 찾는다.
* outer가 `null` 일 때까지 반복해서 찾고 없으면 에러를 발생시킨다.

<br>

## 참조

* [You don't know JS, Scope and Closures](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch1.md)