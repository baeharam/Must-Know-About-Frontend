# 이벤트 루프 (Event loop)

> [콜 스택(Call stack)과 힙(Heap)](https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/javascript/stack-heap.md) 을 보고 오자.

자바스크립트는 **단일 스레드(Single-threaded) 기반 언어** 로, 자바스크립트 엔진이 단일 콜 스택을 갖는다. 이 말은 요청이 동기적으로 처리된다는 것을 의미한다. 그렇다면 비동기 요청은 어떻게 처리될 수 있을까? 그것은 바로 자바스크립트를 실행하는 환경인 브라우저나 Node.js가 담당한다. **여기서 자바스크립트 엔진과 그 실행 환경을 상호 연동시켜주는 장치가 바로 이벤트 루프이다.** 따라서, 이벤트 루프는 자바스크립트 엔진에 있지 않고 그 환경에 속한다.

<br>

## 태스크 큐(Task queue)와 마이크로태스크 큐(Microtask queue)

자바스크립트의 실행 환경은 2가지 큐를 가지고 있으며 **각각 스크립트 실행, 이벤트 핸들러, 콜백함수 등의 태스크(Task) 담기는 공간이다.** 태스크가 콜백함수라면 그 종류에 따라 다른 큐에 담기며 대표적인 예로는 다음과 같은 것들이 있다.

* **태스크 큐**
  * `setTimeout()` , `setInterval()` , UI 렌더링, `requestAnimationFrame()`
* **마이크로태스크 큐**
  * Promise, MutationObserver

이벤트 루프는 2개의 큐를 감시하고 있다가 콜 스택이 비게 되면, 콜백함수를 꺼내와서 실행한다. 이 때 **마이크로태스크 큐의 콜백함수가 우선순위를 가지기 때문에** 마이크로태스크 큐의 콜백함수를 전부 실행하고 나서 태스크 큐의 콜백함수들을 실행한다. (단, UI 렌더링이 태스크 큐에 속하기 때문에 마이크로태스크 큐의 태스크가 많으면 렌더링이 지연될 수 있다.)

<br>

## 예시를 통한 동작방식의 이해

```javascript
console.log('콜 스택!');
setTimeout(() => console.log('태스크 큐!'), 0);
Promise.resolve().then(() => console.log('마이크로태스크 큐!'));
```

결과는 다음과 같다.

```
콜 스택!
마이크로태스크 큐!
태스크 큐!
```

처음 스크립트가 로드될 때 **"스크립트 실행"** 이라는 태스크가 먼저 태스크 큐에 들어간다. 그리고 나서 이벤트 루프가 태스크 큐에서 해당 태스크를 가져와 콜 스택을 실행하는 것이다. 즉, 콜 스택에는 이미 GEC(Global Execution Context)가 생성되어 있는 상태에서 "스크립트 실행" 이라는 태스크를 실행하게 되면 그제서야 GEC에 속한 코드가 실행되는 방식이다.

그럼 하나하나 어떻게 동작하는지 그림으로 살펴보자.

<img src="../../images/javascript/task0.png" width="600px">

제일 먼저, "스크립트 실행" 태스크가 태스크 큐에 들어가게 된다.

<img src="../../images/javascript/task1.png" width="600px">

이후, 이벤트 루프가 그 태스크를 가져와서 로드된 스크립트를 실행시킨다. 따라서 맨 처음에 `console.log` 가 실행된다.

<img src="../../images/javascript/task2.png" width="600px">

그 다음, `setTimeout()` 이 콜 스택으로 가고 브라우저가 이를 받아서 타이머를 동작시킨다.

<img src="../../images/javascript/task3.png" width="600px">

타이머가 끝나면 `setTimeout()` 의 콜백함수를 태스크 큐에 넣는다.

<img src="../../images/javascript/task4.png" width="600px">

`Promise` 가 콜 스택으로 가고 콜백함수를 마이크로태스크 큐에 넣는다.

<img src="../../images/javascript/task5.png" width="600px">

이벤트 루프는 마이크로태스크 큐에서 제일 오래된 태스크인 `Promise` 의 콜백함수를 가져와 콜 스택에 넣는다.

<img src="../../images/javascript/task6.png" width="600px">

`Promise` 의 콜백함수가 끝나고 태스크 큐에서 제일 오래된 태스크인 `setTimeout()` 의 콜백함수를 가져와 콜 스택에 넣는다.

<img src="../../images/javascript/task7.png" width="600px">

`setTimeout()` 의 콜백함수가 끝나면 콜 스택이 비게 되고 프로그램이 종료된다.

<br>

## 참고

* [자바스크립트와 이벤트 루프](https://meetup.toast.com/posts/89)
* [what the heck is the event loop anyway](https://www.youtube.com/watch?v=8aGhZQkoFbQ) → 굉장히 좋은 영상, 꼭 1번은 보자.
* [Event loop: microtasks and macrotasks](https://javascript.info/event-loop)