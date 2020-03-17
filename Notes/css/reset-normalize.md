# Reset.css vs Normalize.css

크롬, 사파리, IE 등 각 브라우저마다 HTML 요소의 기본 스타일을 가지고 있다. 따라서, CSS로 스타일링을 적용할 때 이러한 특징이 동일한 스타일 적용을 방해하기 때문에 이를 해결하기 위해서 나온 스타일 초기화 기법들이다.

<br>

## Reset.css

**모든 브라우저 내장 스타일을 없애는 기법** 으로, 그 어떤 스타일도 없는 상태에서 스타일링을 시작한다. `h1` ~ `h6` , `p` , `em` 등 각 태그에 적용되는 스타일을 모두 없앤다. 가장 유명한 스타일은 Eric Mayer의 Reset CSS이며 이를 [깃헙](https://github.com/shannonmoeller/reset-css) 에서 유지하고 있다. 보통, 초기화를 한 후 각자의 방식에 맞게 변형해서 사용한다.

<br>

## Normalize.css

**모든 브라우저의 스타일을 동일하게 하는 기법** 으로, 스타일을 없애는 Reset.css와는 다르게 기존 스타일을 유지하되 브라우저들의 다른 스타일을 고치는 방식이다. 가장 유명한 스타일은 necolas의 normalize.css이며 이를 [깃헙](https://github.com/necolas/normalize.css/) 에서 유지하고 있다. 실제 코드의 주석을 보면 각 요소를 스타일링 하는 이유에 대해 설명하고 있다.

<br>

## 차이점과 선택

* Reset.css의 경우, 모든 것을 초기화하기 때문에 스타일을 처음부터 적용해 나가는 것이 힘들 수 있고 브라우저의 버그를 고치는 것이 아니기 때문에 각 브라우저마다 다른 버그를 발생시킬 수 있다. 하지만, 아예 초기화를 하는 것이기 때문에 업데이트가 필요없다.
* Normalize.css의 경우, 브라우저가 업데이트 되어서 새로운 내장 스타일이 적용될 때마다 각 브라우저의 다른 점을 파악하여 스타일을 업데이트해야 하기 때문에 끊임없는 버전 업데이트가 있어야 최신 스타일을 유지할 수 있다. 하지만, 브라우저의 버그를 고치기 때문에 버그가 발생할 걱정을 덜고 기본 스타일을 어느정도 유지하기 때문에 스타일링에 힘을 덜 들일 수 있다.

둘 다 장단점이 있기 때문에 어떤 것이 더 낫다라고는 할 수 없고, 상황에 맞게 적용해서 사용하면 된다고 생각한다.

<br>

## 참고

* [Stackoverflow, CSS reset - What exactly does it do?](https://stackoverflow.com/questions/11578819/css-reset-what-exactly-does-it-do)
* [Stackoverflow, What is the difference between Normalize.css and Reset CSS?](https://stackoverflow.com/questions/6887336/what-is-the-difference-between-normalize-css-and-reset-css)
* [reset.css 와 Normalize.css](https://sapjil.net/resetcss-normalizecss/)
* [About normalize.css](http://nicolasgallagher.com/about-normalize-css/)