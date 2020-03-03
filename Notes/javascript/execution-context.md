# 실행 컨텍스트 (Execution Context)

##  정의

**코드의 실행환경에 대한 여러가지 정보를 담고 있는 개념** 으로, 간단히 말하자면 자바스크립트 엔진에 의해 만들어지고 사용되는 코드 정보를 담은 객체의 집합이라고 할 수 있다.

<br>

## 종류

자바스크립트의 코드는 3가지 종류로 이루어지는데, 글로벌 스코프에서 실행하는 글로벌 코드, 함수 스코프에서 실행하는 함수 코드 그리고 여기서 다루진 않지만 `eval()` 로 실행되는 코드가 있다. 이 각각의 코드는 자신만의 실행 컨텍스트를 생성한다.

엔진이 스크립트 파일을 실행하기 전에 **글로벌 실행 컨텍스트(Global Execution Context, GEC)** 가 생성되고, 함수를 호출할 때마다 **함수 실행 컨텍스트(Function Execution Context, FEC)** 가 생성된다. 주의할 점은, 글로벌의 경우 실행 이전에 생성되지만 함수의 경우 호출할 때 생성된다는 점이다.

<br>

## 실행 컨텍스트 스택 (Execution Context Stack)

실행 컨텍스트가 생성되면 흔히 콜 스택(Call Stack)이라고도 불리는 실행 컨텍스트 스택에 쌓이게 된다. GEC는 코드를 실행하기 전에 쌓이고 모든 코드를 실행하면 제거된다. FEC는 호출할 때 쌓이고 호출이 끝나면 제거된다. 예시 코드를 통해 살펴보자.

```javascript
function func() {
  console.log('함수 실행 컨텍스트');
}
console.log('글로벌 실행 컨텍스트');
func();
```

제일 처음, 코드를 실행하기 전에 GEC가 쌓이고 코드를 실행하면서 콘솔에 "글로벌 실행 컨텍스트" 가 출력된다. 그 다음 `func()` 을 호출하고 그에 대한 FEC가 만들어져 쌓이고 FEC를 실행하며 콘솔에 "함수 실행 컨텍스트" 가 출력된다. 이후 `func()` 이 종료되고 FEC가 스택에서 제거된 후, 모든 코드의 실행이 끝나면서 GEC가 스택에서 제거된다. [GIF](https://miro.medium.com/max/1100/1*dUl6qPEaDJJTXWythQsEtQ.gif) 를 통해서 더 쉽게 이해할 수 있으니 꼭 보자.

<br>

## 구성요소

실행 컨텍스트는 다음과 같은 구성요소를 갖는다.

* Lexical Environment
* Variable Environment
* this 바인딩

### Lexical Environment

Lexical Environment는 **변수 및 함수 등의 식별자(Identifier) 및 외부 참조에 관한 정보를 가지고 있는 컴포넌트** 이다. 이 컴포넌트는 2개의 구성요소를 갖는다.

* **Environment Record**
* **outer 참조**

Environment Record가 식별자에 관한 정보를 가지고 있으며 outer 참조는 외부 Lexical Environment를 참조하는 포인터이다.

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

따라서, `foo()` 에서 `x` 를 참조할 때는 현대 Environment Record를 찾아보고 없기 때문에 outer 참조를 사용하여 외부의 Lexical Environment에 속해 있는 Environment Record를 찾아보는 방식이다.

### Variable Environment

Variable Environment는 Lexical Environment와 동일한 성격을 띠지만 **`var` 로 선언된 변수만 저장한다는 점에서 다르다.** 즉, Lexical Environment는 `var` 로 선언된 변수를 제외하고 나머지(`let` 으로 선언되었거나 함수 선언문)를 저장한다. ( 코드로 확인해 볼려면 [여기](https://stackoverflow.com/a/45788048/11789111) 를 보자 )

### this 바인딩

this의 바인딩은 실행 컨텍스트가 생성될 때마다 this 객체에 어떻게 바인딩이 되는지를 나타낸 것이다.  (ES6부터 this의 바인딩이 LexicalEnvironment 안에 있는 EnvironmentRecord 안에서 일어난다는 사실을 기억해두도록 하자. 그렇게 중요하진 않으니 알고만 있자.)

* **GEC의 경우**
  * strict mode라면 `undefined` 로 바인딩된다.
  * 아니라면 글로벌 객체로 바인딩된다. (브라우저에선 window, 노드에선 global)
* **FEC의 경우**
  * 해당 함수가 어떻게 호출되었는지에 따라 바인딩된다.

<br>

## 과정

EC는 2가지 과정을 거친다.

1. **Creation Phase (생성단계)**
2. **Execution Phase (실행단계)**

### 생성단계

생성단계는 다시 3가지 단계로 이루어진다.

1. Lexical Environment 생성
2. Variable Environment 생성
3. this 바인딩

여기서 **주의할 점은 값이 변수에 매핑되지 않는다는 것** 이다. `var` 의 경우는 `undefined` 로 초기화되고 `let` 이나 `const` 는 아무 값도 가지지 않는다.

### 실행단계

이제 코드를 실행하면서 **변수에 값을 매핑시킨다.** 예시를 통해 보자.

```javascript
var a = 3;
let b = 4;

function func(num) {
  var t = 9;
  console.log(a + b + num + t);
}

var r = func(4);
```

* **GEC의 생성 단계**

여기서 생성이 될 때 실행 컨텍스트 스택에 쌓인다.

```
GEC {
	ThisBinding: window,
	LexicalEnvironment: {
		EnvironmentRecord: {
			b: <uninitialized>,
			func: func(){...}
		},
		outer 참조: null
	},
	VariableEnvironment: {	
		EnvironmentRecord: {
			a: undefined,
			r: undefined
		},
		outer 참조: null
	}
}
```

* **GEC의 실행 단계**

```
GEC {
	ThisBinding: window,
	LexicalEnvironment: {
		EnvironmentRecord: {
			b: 4,
			func: func(){...}
		},
		outer 참조: null
	},
	VariableEnvironment: {
		EnvironmentRecord: {
			a: 3,
			r: undefined
		},
		outer 참조: null
	}
}
```

이제 `func()` 을 호출하고 FEC를 생성한다.

* **FEC의 생성 단계**

```
FEC {
	ThisBinding: window,
	LexicalEnvironment: {
		EnvironmentRecord: {
			arguments: { num: 4, length: 1 },
		},
		outer: GEC의 LexicalEnvironment
	},
	VariableEnvironment: {
		EnvironmentRecord: {
			t: undefined
		},
		outer: GEC의 LexicalEnvironment
	}
}
```

* **FEC의 실행 단계**

```
FEC {
	ThisBinding: window,
	LexicalEnvironment: {
		EnvironmentRecord: {
			arguments: { num: 4, length: 1 },
		},
		outer: GEC의 LexicalEnvironment
	},
	VariableEnvironment: {
		EnvironmentRecord: {
			t: 9
		},
		outer: GEC의 LexicalEnvironment
	}
}
```

FEC가 스택에서 제거 되고 GEC의 `r` 이 20으로 초기화된다.

```
GEC {
	ThisBinding: window,
	LexicalEnvironment: {
		EnvironmentRecord: {
			b: 4,
			func: func(){...}
		},
		outer 참조: null
	},
	VariableEnvironment: {
		EnvironmentRecord: {
			a: 3,
			r: 20
		},
		outer 참조: null
	}
}
```

모든 코드를 실행하고 GEC가 스택에서 제거된 뒤 프로그램이 종료된다. [GIF](https://miro.medium.com/max/1100/1*SBP65hdVDW5j0LuVryTiXw.gif) 를 보면 더 확실히 이해할 수 있으니 꼭 보자.

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
* [JavaScript Internals: Execution Context](https://medium.com/better-programming/javascript-internals-execution-context-bdeee6986b3b)