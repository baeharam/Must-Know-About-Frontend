# 네이티브 객체 vs 호스트 객체

## 네이티브 객체 (Native Object)

ECMAScript 명세에서 의미론적인 부분을 완전히 정의해놓은 객체들로, 다음과 같은 것들이 있다.

* `Object`
* `Function`
* `Date`
* `Math`
* `parseInt`
* `eval` ...

<br>

## 호스트 객체 (Host Object)

자바스크립트를 실행하는 환경에 종속된 객체로 그 환경에서만 찾아볼 수 있는 객체이다. 만약 브라우저 환경이라면 다음과 같은 것들이 있다.

* `window`
* `document`
* `location`
* `XMLHttpRequest`
* `querySelectorAll` ...

<br>

## 참고

* [Stackoverflow, What is the difference between native objects and host objects?](https://stackoverflow.com/questions/7614317/what-is-the-difference-between-native-objects-and-host-objects)
* [MDN, Standard built-in objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)
* [Poiemaweb, 빌트인 객체](https://poiemaweb.com/js-built-in-object)