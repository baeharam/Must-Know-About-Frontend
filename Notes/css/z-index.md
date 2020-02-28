# z-index의 동작방식

## z-index와 쌓임 맥락

z-index를 이해하기 위해선 먼저, 쌓임 맥락(Stacking Context)의 개념을 이해해야 한다. **쌓임 맥락이란, HTML 요소들에 사용자를 바라보는 기준으로 가상의 z축을 생성하여 3차원 개념으로 보는 것** 이다. 따라서, 쌓임 맥락을 형성한다는 것은 자신만의 3차원 공간을 형성하는 것이며 그 요소들의 우선순위를 z-index가 정하게 되는 원리이다.

<img src="../../images/css/stacking context.png">

[그림 출처](https://tympanus.net/codrops/css_reference/z-index/)

위 그림을 보면, 각 요소들이 사용자를 바라보는 z축 상에서 z-index에 따라 **"쌓이는"** 것을 볼 수 있다. 바로 이것이 쌓임 맥락의 개념이며 쌓임 맥락을 형성하는 조건은 [꽤 많다.](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context) 모든 걸 기억하면 좋겠지만 중요한 것들을 기억해두록 하자.

* **position이 relative/absolute이면서 z-index가 auto가 아닌 요소**
* **position이 fixed/sticky인 요소**
* **opacity가 1보다 작은 요소**
* **transform이 none이 아닌 요소**

가장 많이 쓰는 속성들을 기준으로 조금만 나열해보면 위와 같은데 이 정도는 암기하도록 하자.

쌓임 맥락은 다음 특징들을 갖는다.

* 쌓임 맥락은 **다른 쌓임 맥락을 포함할 수 있다.**
* 쌓임 맥락에서 쌓임을 고려하는 것은 **오직 자식 요소들에 대해서** 만이다.

즉, 2개의 쌓임 맥락을 형성하는 요소가 있다고 했을 때, 각각은 독립적인 쌓인 맥락을 갖으며 그 안의 자식 요소들은 부모 안에서의 쌓임만 고려된다는 것이다. 

<br>

## 우선순위

쌓임 맥락을 형성하는 요소가 아무것도 없다고 하면 다음 우선순위로 쌓이게 된다.

<img src="../../images/css/default stacking order.png">

[그림 출처](https://tympanus.net/codrops/css_reference/z-index/)

만약, 동일한 성격의 요소라면 마크업 순서로 쌓임이 결정된다. 즉, 아래와 같은 경우,

```html
<div>A</div>
<div>B</div>
<div>C</div>
```

```css
div {
  position: absolute;
}
```

여기서 쌓임 맥락을 형성하는 것으로 착각할 수도 있는데 `position: absolute` 라고 해도 `z-index: auto` 이면 쌓임 맥락을 형성하지 않는다. 어쨌든 여기선 동일한 성격의 요소들이기 때문에 마크업 순서인 A,B,C 순으로 쌓임이 형성된다. ([Codepen](https://codepen.io/BaeHaram/pen/ExjmvRY) 에서 확인할 수 있다.)

쌓임 맥락을 형성한다면, `z-index` 값을 설정할 수 있는 `position: static` 이 아닌 요소들의 경우는 동일한 마크업 레벨에서, `z-index` 값으로 우선순위를 결정한다. `z-index` 값을 설정할 수 없는 요소라면 마크업 순서로 결정한다. 여기선 `position: static` 이 아니고 `z-index: auto` 가 아닌 요소를 보자.

```html
<div>1</div>
<div>2</div>
<div>3
  <div>4</div>
  <div>5</div>
  <div>6</div>
</div>
```

마크업이 위와 같이 되어 있을 때, `z-index` 에 따라 다음과 같이 쌓인다.

<img src="../../images/css/z-index stacking order.png">

[그림출처](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)

* div1과 div2, div3는 같은 레벨에 있으므로 z-index에 따라 쌓이기 때문에 div2 > div3 > div1 순으로 쌓인다.
* div4와 div5, div6은 div3안에 있으므로 **그 안에서** z-index에 따라 쌓인다.
* 즉, div3 안의 요소들의 z-index가 div1,div2 보다 커도 영향을 주지 않는다.
* 결론적으로, div5 > div6 > div4 순으로 쌓인다.

<br>

## 참고

* [CSSReference, z-index](https://tympanus.net/codrops/css_reference/z-index/)
* [MDN, Stacking Context](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)
* [MDN, z-index](https://developer.mozilla.org/ko/docs/Web/CSS/z-index)

