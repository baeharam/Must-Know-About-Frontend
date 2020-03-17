# 시맨틱 마크업

시맨틱(Semantic)이란 "의미론적인" 의 뜻을 가지며 마크업(Markup)이란 HTML 태그로 문서를 작성하는 것을 말한다. 따라서, 시맨틱 마크업이란 **의미를 잘 전달하도록 문서를 작성하는 것을 말한다.**

## 작성방법

시맨틱 마크업을 하기 위해선 각 태그를 그 용도에 맞게 사용하여야 한다. 즉, 다음과 같은 것들을 말한다.

* 헤더/푸터에 `<header>` 와 `<footer>` 사용
* 메인 컨텐츠에 `<main>` 과 `<section>` 사용
* 독립적인 컨텐츠에 `<article>` 사용
* 최상위 제목으로 `<h1>` 사용
* 순서가 없는 목록으로 `<ul>` 과 `<li>` 사용
* 내비게이션에 `<nav>` 사용

이런 식으로 태그가 가지고 있는 의미에 맞게 사용하는 것인데, 이런 점 이외에도 CSS 스타일을 명시하는 태그를 사용하지 않는 것 또한 시맨틱 마크업의 한 종류이다. **즉, 태그가 가지는 의미 자체가 스타일이라면 이는 마크업 자체가 스타일을 갖는 것이기 때문에 시맨틱 마크업에 적합하지 않다.**

예를 들어, 동일한 효과를 부여하는 `<strong>` 과 `<b>` 태그가 있다. 둘은 동일하게 글자색을 진하게 하지만 `<b>` 태그의 경우는 그 자체가 "bold" 의 약어이기 때문에 태그 자체가 스타일을 가진다고 할 수 있다. 하지만 `<strong>` 의 경우는 "그 안의 내용이 다른 내용보다 더 강조되어야 한다" 라는 의미를 가지기 때문에 시맨틱 마크업에 더 적합하다.

<br>

## 특징

* 검색엔진이 시맨틱 태그를 중요한 키워드로 간주하기 때문에 **검색엔진 최적화(SEO)에 유리하다.**
* **웹 접근성** 측면에서, 시각장애가 있는 사용자로 하여금 그 의미를 훨씬 잘 파악할 수 있다.
* 단순한 `div` , `span` 으로 둘러싸인 요소들보다 코드를 볼 때 **가독성이 더 좋다.**

실무에서 시맨틱 마크업이 완벽하게 쓰이는 것은 이상적이긴 하지만, 이러한 특징들을 고려하고 웹사이트를 구성하는 것이 많은 측면에서 바람직하다.

<br>

## 참고

* [Stackoverflow, What are the benefits of using semantic HTML?](https://stackoverflow.com/questions/1729447/what-are-the-benefits-of-using-semantic-html)
* [Stackoverflow, What's the difference between  and ,  and ?](https://stackoverflow.com/questions/271743/whats-the-difference-between-b-and-strong-i-and-em)
* [MDN, Semantics](https://developer.mozilla.org/ko/docs/Glossary/Semantics)