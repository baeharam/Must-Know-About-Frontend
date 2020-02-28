# CSR(Client Side Rendering)과 SSR(Server Side Rendering)

SPA(Single Page Application)란 완전히 새로운 페이지를 로드하는 웹사이트 방식에서 벗어나서 흔히 말하는 컴포넌트 기반으로 사용자 기반으로 동적일 로딩을 시키는 웹 어플리케이션을 말한다. SPA에선 기본적으로 **CSR방식** 으로 렌더링을 하며 전통적인 웹 사이트는 **SSR방식** 으로 렌더링을 한다. 각 방식의 동작방식과 장단점을 알아보고 SPA에서 SSR을 구현하는 것의 장점과 그 이유를 알아보자. (여기선 리액트로 SPA를 구현한다고 가정하자.)



## CSR

<img src="../../images/frontend/CSR.png">

CSR에선 브라우저가 서버에 HTML, CSS, JS를 전부 요청해서 리액트를 실행한 후에야 웹사이트를 사용할 수 있다. 그 전엔 보이지도 않고 사용자가 사용할 수도 없다.

### :+1: 장점

* 첫 로딩 이후의 빠른 렌더링
* 빠른 내비게이션
* 서버의 낮은 부담

### :-1: 단점

* 느린 첫 로딩
* 사용자의 인터넷 환경 및 어떤 브라우저를 사용할지 모르기 때문에 예측 불가능한 성능
* Client-side 라우팅으로 인한 크롤링 지연
* SEO(Search Engine Optimization) 문제



## SSR

<img src="../../images/frontend/SSR.png">

SSR에선 브라우저가 HTML을 요청하고 JS파일을 다운 받으면서 화면에 렌더링 시킨다. 따라서 사용자는 화면을 볼 수 있게 되지만 아직 브라우저가 리액트를 실행하지 않았기 때문에 원하는 기능이 시연되지 않을 수도 있다. 이후에 리액트가 실행되면 정상적으로 동작한다.

### :+1: 장점

* SEO 친화적이다.
* 사용자가 컨텐츠를 더 빨리 볼 수 있게 한다.
* 소셜 미디어 기반 최적화 (미리보기에서 제목, 이미지 등)
* 정적 페이지에 좋음
* 사용자 디바이스에 부담 적다.

### :-1: 단점

* 서버에 부담이 크다
* HTML 문서가 커지게 된다.
* 다른 페이지 요청시 전체 페이지 다시 렌더링



## 그럼 어떻게?

<img src="../../images/frontend/next.png">

위에서 살펴본 바로는 CSR을 하게 되면 초기 로딩 속도가 느린 대신 라우팅 측면에서 굉장히 빠르다. 하지만 역시 SEO에서 떨어진다. SSR은 초기 로딩 속도가 빠르며 SEO쪽도 굉장히 좋다. 하지만 라우팅 측면에서 다른 페이지를 전부 로드하기 때문에 사용자에게 느리게 느껴질 수 있고 서버의 부담이 커진다. 그렇다면 이런 2가지 장점을 모두 해결할 수 없을까? **정말 완벽하게 해결하진 못하겠지만 양측의 장점을 부분적으로 사용할 수는 있다**. 그러나 이를 위해선 높은 러닝커브가 존재하기 때문에 밑바닥 부터 구축하기는 쉽지 않다. 이를 위해 나온 프레임워크가 바로 Next.js이다. 기존의 리액트 라이브러리 위에 올라가는 프레임워크 개념으로 **SPA에서의 SSR을 구현하게 해준다.** Vue에서 비슷한 것으로 Nuxt.js가 있다.



## 참고

* [Client-Side Rendering versus Server-Side Rendering!](https://altalogy.com/blog/client-side-rendering-vs-server-side-rendering/)
* [What are Single Page Applications(SPA)?](https://dev.to/kendyl93/what-are-single-page-applications-spa-32bh)
* [SPA에서의 SSR과 CSR](https://velog.io/@rjs1197/SSR과-CSR의-차이를-알아보자)
* [The Benefits of Server Side Rendering Over Client Side Rendering](https://medium.com/walmartlabs/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8)