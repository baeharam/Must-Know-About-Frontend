# 브라우저의 렌더링 원리

브라우저가 화면에 나타나는 요소를 렌더링 할 때, 웹킷(Webkit)이나 게코(Gecko) 등과 같은 **렌더링 엔진** 을 사용한다. 렌더링 엔진이 HTML, CSS, Javascript로 렌더링할 때 **CRP(Critical Rendering Path)** 라는 프로세스를 사용하며 다음 단계들로 이루어진다.

1. **HTML 파싱 후, DOM(Document Object Model) 트리 구축**
2. **CSS 파싱 후, CSSOM(CSS Object Model) 트리 구축**
3. **Javascript 실행**
   * 주의! HTML 중간에 스크립트가 있다면 HTML 파싱이 중단된다.
4. **DOM과 CSSOM을 조합하여 렌더트리(Render Tree) 구축**
   * 주의! `display: none` 속성과 같이 화면에서 보이지도 않고 공간을 차지하지 않는 것은 렌더트리로 구축되지 않는다.
5. **뷰포트 기반으로 렌더트리의 각 노드가 가지는 정확한 위치와 크기 계산 (Layout/Reflow 단계)**
6. **계산한 위치/크기를 기반으로 화면에 그림 (Paint 단계)**

<br>

실제로 크롬 개발자 도구를 이용해 다음 코드를 어떻게 렌더링 하는지 살펴보았다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>테스트</title>
  </head>
  <body>
    <div></div>
    <script src="script.js"></script>
  </body>
</html>
```

```css
body {
  background-color: red;
}
div {
  width: 100px;
  height: 100px;
  background-color: blue;
}
```

```javascript
document.querySelector('div').addEventListener('click', () => {
  console.log('Click div');
});
```

<img src="../../images/frontend/rendering.png">

위 로그를 보면 알 수 있는 것처럼 위에서 언급한 CRP가 진행된다.

1. Parse HTML을 통해 HTML 파싱 후, DOM 트리 구축
2. Parse Stylesheet를 통해 CSS 파싱 후, CSSOM 트리 구축
3. Evaluate Script를 통해 Javascript 실행
4. 렌더트리 구축
5. Layout을 통해 뷰포트 기준으로 렌더트리 노드들의 각 크기/위치 계산
6. Paint를 통해 Layout에서 계산한 값들로 각 요소를 화면에 그림

<br>

## 참고

* [HTML Critical rendering path의 이해](https://blog.asamaru.net/2017/05/04/understanding-the-critical-rendering-path/)
* [Naver, 브라우저는 어떻게 동작하는가?](https://d2.naver.com/helloworld/59361)
* [MDN, Critical Rendering Path](https://developer.mozilla.org/en-US/docs/Web/Performance/Critical_rendering_path)
* [Google, 렌더링 트리 생성, 레이아웃 및 페인트](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction)
* [Stackoverflow, When does parsing HTML DOM tree happen?](https://stackoverflow.com/questions/34269416/when-does-parsing-html-dom-tree-happen)