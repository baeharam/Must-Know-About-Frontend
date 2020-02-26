# Block Formatting Context

MDN의 정의를 보면,

> *BFC는 웹페이지의 블록 레벨 요소를 렌더링하는데 사용되는 CSS의 비주얼 서식 모델 중 하나이다.*

즉, 블록 레벨 요소가 포함되는 **서식모델** 이다.

<br>

## 생성 조건

BFC가 생성되기 위해선 다음과 같은 조건 중 하나를 만족해야 한다.

* 루트 혹은 이를 포함하는 요소

* float가 none이 아니면서 clear 되지 않은 경우
* position이 absolute / fixed
* display가 inline-block / tabel-cell / tabel-caption
* overflow가 visible이 아님
* display가 flex / inline-flex

위 조건에 따른 예제를 보면, 아래 요소들은 모두 BFC를 생성한다.

```html
<div class="float"></div>
<div class="position"></div>
<div class="display"></div>
<div class="overflow"></div>
<div class="flex"></div>
```

```css
.float { float: left; }
.position { position: absolute; }
.display { display: inline-block; }
.overflow { overflow: hidden; }
.flex { display: flex; }
```

<br>

## 활용

1. **마진겹침 제거하기**

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="css,result" data-user="BaeHaram" data-slug-hash="YzXGZBd" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="BFC - Solve Margin Collapsing">
  <span>See the Pen <a href="https://codepen.io/BaeHaram/pen/YzXGZBd">
  BFC - Solve Margin Collapsing</a> by 배하람 (<a href="https://codepen.io/BaeHaram">@BaeHaram</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

`p` 태그 사이에 10px의 마진이 마진겹침으로 인해 20px이 아닌 10px이 되었다. 이 때 새로운 BFC를 생성해서 `p` 를 집어넣으면 마진겹침을 해결할 수 있다.

2. **float된 요소들 포함하기**

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="css,result" data-user="BaeHaram" data-slug-hash="oNXZBXJ" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="BFC - Solve floated element">
  <span>See the Pen <a href="https://codepen.io/BaeHaram/pen/oNXZBXJ">
  BFC - Solve floated element</a> by 배하람 (<a href="https://codepen.io/BaeHaram">@BaeHaram</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

보통 float된 요소를 포함하기 위해선 `.clearfix` 핵을 사용하지만 새로운 BFC를 생성함으로도 해결할 수 있다.

3. **float된 요소를 감싸는 텍스트를 분리하기**

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="html,result" data-user="BaeHaram" data-slug-hash="VwLpPvN" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="BFC - Solve test wrapping">
  <span>See the Pen <a href="https://codepen.io/BaeHaram/pen/VwLpPvN">
  BFC - Solve test wrapping</a> by 배하람 (<a href="https://codepen.io/BaeHaram">@BaeHaram</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

`p` 태그로 새로운 BFC를 생성하여 텍스트가 float 된 요소를 감싸지 않도록 하였다.

<br>

## 참고

* [Understanding Block Formatting Contexts in CSS](https://www.sitepoint.com/understanding-block-formatting-contexts-in-css/)
* [MDN, Block formatting context](https://developer.mozilla.org/ko/docs/Web/Guide/CSS/Block_formatting_context)

