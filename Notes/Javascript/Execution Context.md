# Execution Context

> *An execution context is a specification device that is used to track the runtime evaluation of code by an ECMAScript implementation.*

ECMAScript의 정의에 따르면, **코드의 수행환경에 대한 여러 정보를 가지고 있는 명세적 장치** 라고 할 수 있다. 명세적 장치이기 때문에 자바스크립트 엔진이 이를 구현하는 것은 엔진마다 다를 수 있다.

<br>

## 생성

EC(Exectuion Context)는 아래와 같은 조건 하에서 생성된다.

* 코드를 실행하기 전에 글로벌 코드의 실행 환경에 관련된 **GEC(Global Execution Context)** 가 생성된다.
* 함수를 실행할 때마다 함수의 실행 환경에 관련된 **FEC(Function Execution Context)** 가 생성된다.
* `eval()` 로 코드를 실행할 때마다 그에 관련된 EC가 생성된다. (여기서는 다루지 않는다.)

EC가 생성되면 EC 스택(Execution Context Stack)에 쌓이게 되고, 현재 실행중인 EC(running execution context)가 EC 스택의 가장 위에 있는 EC로 업데이트 된다.

```javascript
// GEC
function func1() {
  function func2() {}
  return func2(); // FEC
}
func1(); // FEC
```

위 코드를 실행하게 되면 EC 스택에는 GEC →  `func1()` 의 EC → `func2()` 의 EC 순으로 쌓이게 된다.

<br>

## 구성요소

EC가 생성되면 여러가지가 생기지만 반드시 알아두어야 할 것은 다음과 같다.

* Lexical Environment
* Variable Environment
* this

### Lexical Environment

Lexical Environment는 변수 및 함수 등의 식별자(Identifier)에 관한 정보를 가지고 있는 컴포넌트이다. 이 컴포넌트는 2개의 구성요소를 갖는다.

* Environment Record
* outer

Environment Record가 식별자에 관한 정보를 가지고 있으며 outer는 외부 Lexical Environment를 참조하는 포인터이다. 즉, 자바스크립트는 렉시컬 스코프를 사용하기 때문에 outer를 사용해서 식별자를 연쇄적으로 검색해나가는 방식이다.

```javascript
var x = 10;
 
function foo() {
  var y = 20;
  console.log(x);
}
```

위와 같은 코드가 있을 때는 아래와 같이 Lexical Environment가 형성된다.

```
globalEnvironment = {
	environmentRecord = { x: 10 },
	outer: null
}
fooEnvironment = {
	environmentRecord = { y: 20 },
	outer: globalEnvironment
}
```

따라서, `foo()` 에서 `x` 를 참조할 때는 현대 Environment Record를 찾아보고 없기 때문에 outer를 사용하여 외부의 Lexical Environment에 속해 있는 Environment Record를 찾아보는 방식이다.

### Variable Environment

Variable Environment는 Lexical Environment와 동일한 성격을 띠지만 `var` 로 선언된 변수만 저장한다는 점에서 다르다. 즉, Lexical Environment는 `var` 로 선언된 변수를 제외하고 나머지(`let` 으로 선언되었거나 함수 선언문)를 저장한다. ( 코드로 확인해 볼려면 [여기](https://stackoverflow.com/a/45788048/11789111) 를 보자 )

### this

this 객체의 바인딩이 아래와 같은 방식으로 일어난다.

* **GEC의 경우**
  * strict mode라면 `undefined` 로 바인딩된다.
  * 아니라면 global 객체로 바인딩된다. (브라우저에선 window)
* **FEC의 경우**
  * 해당 함수가 어떻게 호출되었는지에 따라 바인딩된다.

<br>

## 과정

EC는 2가지 과정을 거친다.

1. Creation Phase (생성단계)
2. Execution Phase (실행단계)

### 생성단계

생성단계는 다시 3가지 단계로 이루어진다.

1. Lexical Environment 생성
2. Variable Environment 생성
3. this 바인딩

어떤 방식으로 생성되었는지는 위에서 배웠고, **주의할 점은 값이 변수에 매핑되지 않는다는 것** 이다. `var` 의 경우는 `undefined` 로 초기화되고 `let` 이나 `const` 는 아무 값도 가지지 않는다.

### 실행단계

이제 코드를 실행하면서 **변수에 값을 매핑시킨다.** GEC의 경우만 아래코드로 살펴보자.

```javascript
var a = 3;
let b = 4;
```

생성단계에선 아래와 같이 GEC가 만들어진다.

```
GEC = {
	LexicalEnvironment = {
		EnvironmentRecord = {
			b: <uninitialized>,
			func: <function>
		},
		outer: null,
		this: global object
	},
	VariableEnvironment = {
		EnvironmentRecord = {
			a: undefined
		},
		outer: null,
		this: global object
	}
}
```

이제 코드를 실행하게 되면 실행단계가 되고 값이 매핑된다.

```
GEC = {
	LexicalEnvironment = {
		EnvironmentRecord = {
			b: 4,
			func: <function>
		},
		outer: null,
		this: global object
	},
	VariableEnvironment = {
		EnvironmentRecord = {
			a: 3
		},
		outer: null,
		this: global object
	}
}
```

<br>

## 종료

FEC는 함수 호출이 끝나게 되면 EC 스택에서 제거되고, GEC는 전체 코드를 실행해서 끝나는 시점에 EC 스택에서 제거된다. 모든 EC가 제거된 후 프로그램이 종료된다.

<br>

## 참고

* [What is the 'Execution Context' in JavaScript exactly?](https://stackoverflow.com/questions/9384758/what-is-the-execution-context-in-javascript-exactly)
* [[JS] 자바스크립트의 The Execution Context (실행 컨텍스트) 와 Hoisting (호이스팅)](https://velog.io/@imacoolgirlyo/JS-자바스크립트의-Hoisting-The-Execution-Context-호이스팅-실행-컨텍스트-6bjsmmlmgy)
* [자바스크립트 함수 (2) - 함수 호출](https://meetup.toast.com/posts/123)
* [The ECMAScript “Executable Code and Execution Contexts” chapter explained](https://medium.com/@g.smellyshovel/the-ecmascript-executable-code-and-execution-contexts-chapter-explained-fa6e098e230f#f88f)
* [ECMA-262-5 in detail. Chapter 3.2. Lexical environments: ECMAScript implementation.](http://dmitrysoshnikov.com/ecmascript/es5-chapter-3-2-lexical-environments-ecmascript-implementation/#this-binding)
* [ECMAScript 5 spec: LexicalEnvironment versus VariableEnvironment](https://2ality.com/2011/04/ecmascript-5-spec-lexicalenvironment.html)
* [Variable Environment vs lexical environment](https://stackoverflow.com/questions/23948198/variable-environment-vs-lexical-environment)
* [ECMAScript 2020 Language Specification](https://tc39.es/ecma262/)