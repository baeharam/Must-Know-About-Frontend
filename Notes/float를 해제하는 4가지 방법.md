# float를 해제하는 방법들

float 속성을 자식 엘리먼트에 사용하게 되면 부모 엘리먼트가 자식의 높이를 감지할 수 없기 때문에 이를 반영하기 위한 방법이 필요하다. 다음 코드를 가정으로 한다.

```html
<div class="parent">
  부모
  <div class="child">
    자식
  </div>
</div>
```

```css
.child {
  float: left;
}
```

<br>

## 부모 엘리먼트에 `float` 적용

* 자식을 포함할 만큼만 너비로 줄어듦
* 부모가 겹겹이 있을 경우 계속해서 float 시켜야 함

```css
.parent {
  float: left;
}
```

<br>

## 부모에 `overflow` 속성 적용

* `overflow: auto` 의 경우, 자식의 너비가 더 크면 스크롤바 생김
* `overflow: hidden` 의 경우, 자식의 너비가 더 크면 잘림

```css
.parent {
  overflow: hidden;
}
```

<br>

## 부모가 끝나기 전 빈 엘리먼트로 `clear` 적용

* 의미없는 엘리먼트를 넣기 때문에 권장되지 않음

```html
<div class="parent">
  ...
  <div class="clearfix">
  </div>
</div>
```

```css
.clearfix {
  clear: both;
  height: 0;
  overflow: hidden;
}
```

<br>

## 부모에 `display: inline-block` 적용

* 약간의 여백이 생김
* 자식의 너비를 포함할 만큼으로 줄어듦

```css
.parent {
  display: inline-block;
}
```

<br>

## 가상요소로 `clear` 적용

* 제일 권장되는 방법

```css
.parent::after {
  content: '';
  display: block;
  clear: both;
}
```

<br>

## 참조

* [float를 clear하는 4가지 방법](https://naradesign.github.io/article/float-clearing.html)