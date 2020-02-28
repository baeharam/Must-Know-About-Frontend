# this의 바인딩

EC(Execution Context)가 생성될 때마다 this의 바인딩이 일어나며 우선순위 순으로 나열해보면 다음과 같다.

1. `new` 를 사용했을 때 해당 객체로 바인딩된다.

```javascript
var name = "global";
function Func() {
  this.name = "Func";
  this.print = function f() { console.log(this.name); };
}
var a = new Func();
a.print(); // Func
```

2. `call`, `apply`, `bind` 와 같은 명시적 바인딩을 사용했을 때 인자로 전달된 객체에 바인딩된다.

```javascript
function func() {
  console.log(this.name);
}

var obj = { name: 'obj name' };
func.call(obj); // obj name
func.apply(obj); // obj name
(func.bind(obj))(); // obj name
```

3. 객체의 메소드로 호출할 경우 해당 객체에 바인딩된다.

```javascript
var obj = {
  name: 'obj name',
  print: function p() { console.log(this.name); }
};
obj.print(); // obj name
```

4. 그 외의 경우

* strict mode: `undefined` 로 초기화된다.
* 일반: 브라우저라면 `window` 객체에 바인딩 된다.

<br>

## 참고

* [김정환 블로그, 자바스크립트 this 바인딩 우선순위](http://jeonghwan-kim.github.io/2017/10/22/js-context-binding.html#암시적-바인딩과-new-바인딩의-우선순위)
* [How does the “this” keyword work?](https://stackoverflow.com/questions/3127429/how-does-the-this-keyword-work)