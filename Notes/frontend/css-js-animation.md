# CSS 애니메이션 vs JS 애니메이션

웹사이트에 애니메이션 효과를 부여할 때 CSS의 `transition` / `animation` 속성을 사용할 수 있고 JS의 `setInterval()` / `requestAnimationFrame()` 을 사용할 수 있다. 하지만 각각을 사용할 때의 특징이 다르고 장단점이 있기 때문에 어떤 차이가 있는지 알아두는 것이 좋다. 기술면접에도 나온적이 있다.

<br>

## CSS 애니메이션

일반적으로, 마우스를 올렸을 때 혹은 메뉴 버튼의 전환과 같은 간단하게 처리하는 애니메이션의 경우 CSS로 처리한다. 예를 들어, 200 크기의 정사각형을 왼쪽 위에서 오른쪽 아래로 350px 움직이게 하는 애니메이션을 구현한다고 하면, `transform` 의 `translate` 를 사용해서 구현할 수 있다. 하지만 이를 JS로 구현하기 위해선 `setInterval` 을 통해서 계속해서 `style.top` 과 `style.left` 속성을 변화시켜줘야 한다. 이렇게 되면 이 속성은 브라우저의 렌더링 과정에서 reflow(layout) 단계를 발생시키기 때문에 애니메이션이 부자연스럽게 끊기는 듯한 느낌을 받게 된다. 이런 점에서 바닐라 JS로 애니메이션을 구현하는 것보다 CSS로 구현하는 것이 좋다고 할 수 있다. 이외에도 다양한 장점들이 있으며 정리하자면 다음과 같다.

* 반응형으로 애니메이션을 구현하기에 유용한데, 미디어 쿼리로 애니메이션을 적용하면 된다.
* 외부 라이브러리를 필요로 하지 않는다.
* CSS 자체가 선언형(declarative)이기 때문에 어떤 요소가 애니메이션을 가져야 한다는 직관적인 표현이 가능하다.
* 메인 쓰레드가 아닌 별도의 컴포지터 쓰레드(Compositor Thread)에서 그려지기 때문에 메인 쓰레드에서 작업하는 JS보다 효율적이다.

<br>

## JS 애니메이션

CSS로 처리하기에는 훨씬 복잡하고 무거운 애니메이션 작업들을 효율적이고, 세밀하게 다루기 위해 사용한다. 바닐라 자바스크립트로 구현할 경우 위에서 살펴본 바와 같이 계속해서 요소의 위치를 재계산하기 때문에 비효율적이며 사용자 눈에 가장 부드러운 60fps가 유지되지 않는다. 이때문에 RAF(RequestAnimationFrame) API가 등장했고 구현방식은 동일하지만 60fps를 보장할 수 있게 되었다. 이외에도 외부 라이브러리인 [Velocity.js](http://velocityjs.org/) 와 [GSAP](https://greensock.com/gsap/) 같은 라이브러리를 통해서 성능 좋은 애니메이션을 구현할 수 있다. 최근에 Web Animations API가 나오기도 했는데 현재(2020년 4월 28일) 기준으로 지원하는 브라우저가 현저히 적기 때문에 아직까진 기존의 방법들이 더 높은 생산성을 가진다고 할 수 있다. 보통 복잡한 애니메이션을 구현하려고 하면 외부 라이브러리를 사용할텐데 이것이 CSS에 비해 가지는 장점은 다음과 같다.

* 요소의 스타일이 변하는 순간마다 제어할 수 있기 때문에 애니메이션의 세밀한 구성이 가능해진다.
* GPU를 통한 하드웨어 가속을 제어할 수 있다. 이는 CSS의 특정 속성으로 인한 가속을 막아주는데, 하드웨어 가속이 모바일에서 성능저하를 발생시킬 수 있기 때문에 이런 면에선 좋다.
* 브라우저 호환성 측면에서 `transition` / `animation` 속성보다 뛰어나다.

<br>

## 참고

* [Naver D2, 최신 브라우저의 내부 살펴보기 3 - 렌더러 프로세스의 내부 동작](https://d2.naver.com/helloworld/5237120)
* [애니메이션 성능을 높이는 방법](http://sculove.github.io/blog/2013/12/05/animation-for-performance/)
* [Julian Shapiro, CSS vs. JS Animation: Which is Faster?](https://davidwalsh.name/css-js-animation)
* [손찬욱님, Web Animation API 프레젠테이션](https://sculove.github.io/slides/webAnimation/#/)