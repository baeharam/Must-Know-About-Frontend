# block vs inline vs inline-block

| 특징                         | block              | inline             | inline-block       |
| ---------------------------- | ------------------ | ------------------ | ------------------ |
| 상하 마진/패딩               | :white_check_mark: | :x:                | :white_check_mark: |
| 좌우 마진/패딩               | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| 요소 사이 줄바꿈             | :white_check_mark: | :x:                | :x:                |
| 기본너비가 부모너비          | :white_check_mark: | :x:                | :x:                |
| 요소 사이 공백               | :x:                | :white_check_mark: | :white_check_mark: |
| 너비와 높이 명시했을 때 적용 | :white_check_mark: | :x:                | :white_check_mark: |

[Codepen](https://codepen.io/BaeHaram/pen/poJaRyK) 을 통해서 확인해보면 위의 특징들을 좀 더 명확하게 알 수 있으니 해보도록 하자.

<br>

## 참고

* [Gist, css-display.md](https://gist.github.com/Asheq/1ef5ec77b8e89c2c9da89d2b7a1cf8cb)
* [Stackoverflow, CSS display: inline vs inline-block](https://stackoverflow.com/questions/9189810/css-display-inline-vs-inline-block)