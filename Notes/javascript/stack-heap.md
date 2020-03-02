# 콜 스택(Call stack)과 힙(Heap)

자바스크립트 엔진이 자바스크립트를 실행할 때 원시 타입 및 참조 타입을 저장하는 메모리 구조로 콜 스택과 힙을 가진다.

* **콜 스택** : **원시타입 값** 과 함수 호출의 **실행 컨텍스트(Execution Context)** 를 저장하는 곳이다.
* **힙** : 객체, 배열, 함수와 같이 크기가 **동적으로 변할 수 있는 참조타입 값** 을 저장하는 곳이다.

<br>

## 예시를 통한 동작 원리 보기

```javascript
let a = 10;
let b = 35;
let arr = [];
function func() {
  const c = a + b;
  const obj = { d: c };
  return obj;
}
let o = func();
```

위 코드로 콜 스택과 힙의 동작을 보면 다음과 같다.

제일 처음, GEC(Global Execution Context)가 생성되고 원시 값은 콜 스택에, 참조 값은 힙에 저장된다.

<img src="../../images/javascript/memory1.png">

그 다음 함수 `func()` 을 실행하게 되고 새로운 FEC(Function Execution Context)가 생성되며 동일하게 원시 값은 스택에, 참조 값은 힙에 저장된다.

<img src="../../images/javascript/memory2.png">

이후, 함수 `func()` 이 객체 `obj` 를 리턴해서 `o` 에 저장된다. 리턴하기 때문에 FEC는 콜 스택에서 제거된다.

<img src="../../images/javascript/memory3.png">

전체 코드가 실행이 끝나고 GEC가 콜 스택에서 제거된다. GEC가 제거됨에 따라서, 힙의 객체를 참조하는 스택의 값이 없기 때문에 가비지 컬렉터(Garbage Collector, GC)에 의해 제거된다.

<br>

## 참고

* [JavaScript V8 Engine Explained](https://hackernoon.com/javascript-v8-engine-explained-3f940148d4ef)
* [<번역>자바스크립트의 메모리 모델](https://junwoo45.github.io/2019-11-04-memory_model/)
* [V8 Memory usage(Stack & Heap)](https://speakerdeck.com/deepu105/v8-memory-usage-stack-and-heap?slide=9)
* [V8 엔진(자바스크립트, NodeJS, Deno, WebAssembly) 내부의 메모리 관리 시각화하기](https://ui.toast.com/weekly-pick/ko_20200228/)