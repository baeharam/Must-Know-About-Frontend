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

```html
<div class="bfc">
  <p>element</p>
  <p>element</p>
  <div class="new-bfc">
    <p>element</p>
  </div>
</div>
```

```css
div {
  background-color: blue;
}
p {
  margin: 10px 0;
  background-color: green;
}
.bfc {
  overflow: hidden;
}
.new-bfc {
  overflow: hidden;
}
```

[Codepen](https://codepen.io/BaeHaram/pen/YzXGZBd)

`p` 태그 사이에 10px의 마진이 마진겹침으로 인해 20px이 아닌 10px이 되었다. 이 때 새로운 BFC를 생성해서 `p` 를 집어넣으면 마진겹침을 해결할 수 있다.

2. **float된 요소들 포함하기**

```html
<div class="container">
  <div class="float"></div>
</div>
```

```css
.container {
  border: 3px solid red;
  overflow: hidden;
}

.float {
  float: left;
  width: 500px;
  height: 300px;
  background-color: yellow;
}
```

[Codepen](https://codepen.io/BaeHaram/pen/oNXZBXJ)

보통 float된 요소를 포함하기 위해선 `.clearfix` 핵을 사용하지만 새로운 BFC를 생성함으로도 해결할 수 있다.

3. **float된 요소를 감싸는 텍스트를 분리하기**

```html
 <div class="container">
  <div class="box"></div>
  <p>많은 양의 텍스트....</p>
</div>
```

```css
.container {
  border: 3px solid red;
  overflow: hidden;
}
.box {
  float: left;
  width: 100px;
  height: 100px;
  background-color: green;
}

p {
  overflow: hidden;
}
```

[Codepen](https://codepen.io/BaeHaram/pen/VwLpPvN)

`p` 태그로 새로운 BFC를 생성하여 텍스트가 float 된 요소를 감싸지 않도록 하였다.

<br>

## 참고

* [Understanding Block Formatting Contexts in CSS](https://www.sitepoint.com/understanding-block-formatting-contexts-in-css/)
* [MDN, Block formatting context](https://developer.mozilla.org/ko/docs/Web/Guide/CSS/Block_formatting_context)

