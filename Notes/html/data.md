# data- 속성

**DOM에 데이터를 저장할 수 있는 사용자 정의 데이터 속성** 으로 `data-` 다음 오는 값이 데이터가 된다. 이 속성은 사용하고자 하는 용도에 적합한 속성이나 요소가 없을 때 사용하며 해당 웹페이지가 **독자적으로 사용하는 값** 이다. 즉, 웹페이지와 독립적인 소프트웨어가 이 속성을 사용해서는 안된다.

예를 들어, 음악 사이트에서 앨범 트랙의 음악을 리스트 형식으로 나타내는데 그걸 시간 순으로 정렬하기 위해서 `data-` 속성으로 음악 시간을 삽입한다고 하자.

```html
<ol>
  <li data-length="2m11s">빨간맛</li>
  ...
</ol>
```

만약 이 음악 사이트와 전혀 상관이 없는 외부에서 음악 시간을 알아내기 위해 사용한다면 목적에 부합하지 않는 것이다. 따라서, `data-` 속성은 해당 사이트만의 자체 스크립트를 위한 속성이라고 할 수 있다.

<br>

## 참고

* [W3, Custom Data Attribute](https://www.w3.org/TR/2011/WD-html5-20110525/elements.html#custom-data-attribute)
* [프론트엔드 인터뷰 핸드북, `data-` 속성은 무엇에 좋은가요?](https://github.com/yangshun/front-end-interview-handbook/blob/master/contents/kr/html-questions.md#data-속성은-무엇에-좋은가요)

