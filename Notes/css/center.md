# 가로/세로 가운데 정렬하기

## div의 가운데 정렬

```html
<div class="position-margin"></div>
<div class="position-transform"></div>
<div class="flex">
  <div></div>
</div>
```

위와 같이 마크업이 되어있다고 했을때 다음 방법들을 사용할 수 있다.

### position과 margin

```css
.position-margin {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
 	bottom: 0;
  margin: auto;
}
```

원래 `div` 는 부모의 너비만큼 너비를 갖기 때문에 자신의 너비가 있다 하더라도 보이지 않는 공간이 있다. 이런 특성 때문에 `margin: 0 auto` 와 같이 가로 가운데 정렬을 할 수 있는데, `position: absolute` 를 쓰면 이 공간이 사라지게 된다. 따라서, 해당 공간을 전체로 확장하기 위해서 `left` , `right` , `top` , `bottom` 을 각각 0으로 설정해주었다. 이렇게 되면 보이지 않는 공간이 가로/세로를 전부 차지하게 되고 여기서 `margin: auto` 를 주면 알아서 바깥여백이 만들어지기 때문에 전체적으로 가운데 정렬된다.

### position과 transform

```css
.position-transform {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
```

`div` 의 너비와 높이를 모를 때 유용한 기법으로 부모 기준으로 50% 위/왼쪽에서 떨어진다음 자신의 너비/높이의 50%를 다시 역방향으로 오게 하는 방법이다.

### flex

```css
.flex {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

부모에게 `display: flex` 를 줘야 해결할 수 있는 제약이 있고 지원하지 않는 브라우저가 있긴 하지만 그래도 상당히 유용하게 쓰인다.

**[Codepen](https://codepen.io/BaeHaram/pen/LYVdRmL) 을 통해서 연습해보자.**

<br>

## 텍스트 요소의 가운데 정렬

### 텍스트 -  padding

```html
<div>
  <span>텍스트</span>
</div>
```

```css
div { 
  text-align: center; 
	padding: 3em 0;
}
```

부모에 `text-align: center` 를 줘서 자식 요소들의 텍스트를 가로 가운데 정렬 했고 높이를 주지 않고 패딩을 상/하로 줘서 세로 가운데 정렬을 했다. 이 때 패딩의 단위로 `em` 을 사용했는데 이는 현재 엘리먼트의 폰트 크기의 3배를 의미한다. 즉, 폰트 크기가 바뀔 때마다 패딩도 변하기 때문에 유동적으로 세로 가운데 정렬이 이루어지는 방법이다.

### 텍스트 - line-height

```css
div { height: 100px; }
span { line-height: 100px; }
```

만약 높이를 명시적으로 준다면, 텍스트 요소에게 동일한 크기의 `line-height` 를 주어서 해결할 수 있다.

### 이미지

```html
<div>
  <img src="이미지주소">
  <span>텍스트</span>
</div>
```

```css
img {
  vertical-align: middle;
}
```

이미지의 정렬도 위와 같이 할 수 있는데 한가지 다른 점은, 폰트의 baseline 기준으로 배치가 되기 때문에 이를 middle로 맞춰야 제대로된 정렬이 이루어진다.

**[Codepen](https://codepen.io/BaeHaram/pen/oNXqzJo) 을 통해서 연습해보자.**

<br>

## 참고

* [빔캠프, div 가로세로 모두 가운데 정렬 css position (유튜브)](https://www.youtube.com/watch?v=vdvLfkn9wp4)
* [빔캠프, 너비높이를 알 수 없는 div 가로세로 모두 가운데 정렬 (유튜브)](https://www.youtube.com/watch?v=78-X1JGvCZU)
* [빔캠프, CSS 텍스트 요소 가로, 세로 가운데 정렬 (유튜브)](https://www.youtube.com/watch?v=PEYt17TlTQk)
* [Stackoverflow, Best way to center a  on a page vertically and horizontally?](https://stackoverflow.com/questions/356809/best-way-to-center-a-div-on-a-page-vertically-and-horizontally)