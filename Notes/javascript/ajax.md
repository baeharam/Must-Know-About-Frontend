# AJAX

## AJAX란 무엇인가?

Asynchronous Javascript And XML의 약자로, 비동기적으로 JS를 사용해서 데이터를 받아와 동적으로 DOM을 갱신 및 조작하는 웹 개발 기법을 의미한다. 여기서 XML이 있는 이유는 예전엔 데이터 포맷으로 XML을 많이 사용했기 때문이다.

<br>

## 어떻게 동작하는가?

<img src="../../images/javascript/AJAX.png">

사용자가 AJAX가 적용된 UI와 상호작용하면, 서버에 AJAX 요청을 보내게 된다. 서버는 DB에서 데이터를 가져와서 JS 파일에 정의되어 있는 대로 HTML/CSS와 데이터를 융합하여 만든 DOM 객체를 UI에 업데이트 시킨다. 비동기로 이루어지며, 기존의 페이지를 전부 로딩하는 방식이 아닌 일부만 업데이트 하는 방식이다.

<br>

## 어떻게 사용하는가?

일반적으로 `XMLHttpRequest` 객체를 사용하여 인스턴스를 만들어 인스턴스의 `open()` , `send()` 등의 메소드를 이용한다. 

```javascript
var ourRequest = new XMLHttpRequest();
ourRequest.open(
  "GET",
  "https://learnwebcode.github.io/json-example/animals-1.json"
);
ourRequest.onload = () => {
  var ourData = JSON.parse(ourRequest.responseText);
  console.log(ourData[0]);
};
ourRequest.send();
```

`open()` 으로 요청할 메소드와 URL을 설정한 뒤, 모두 로드되었을 경우의 콜백함수를 초기화한다. 그 다음 `send()` 로 요청을 보낸다. 아래 CodeSandbox를 통해서 직접 수행해보자.

[![Edit JSON and AJAX](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/thirsty-glade-mmbub?fontsize=14&hidenavigation=1&theme=dark)

<br>

## 장단점

### 장점

* 페이지를 전환하지 않고 빠르게 화면 일부분 업데이트 할 수 있다.
* 수신하는 데이터 양을 줄일 수 있고 클라이언트에게 처리를 맡길 수 있다.
* 서버 처리를 기다리지 않고 비동기 요청이 가능하다.

### 단점

* 지원하지 않는 브라우저가 있다.
* 페이지 전환없이 서버와 통신을 하기 때문에 보안상에 문제가 있을 수 있다.
* 무분별하게 사용하면 역으로 서버의 부하가 늘어날 수 있다.
* CORS 문제가 발생할 수 있다.

<br>

## 참고

* [JSON and AJAX Tutorial: With Real Examples(유튜브)](https://www.youtube.com/watch?v=rJesac0_Ftw)
* [How is Ajax independent from a server?](https://www.quora.com/How-is-Ajax-independent-from-a-server)
* [MDN, Ajax 시작하기](https://developer.mozilla.org/ko/docs/Web/Guide/AJAX/Getting_Started)
* [위키백과, Ajax](https://ko.wikipedia.org/wiki/Ajax)