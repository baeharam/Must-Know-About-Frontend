# DOCTYPE

Document Type의 약자로, **HTML이 어떤 버전으로 작성되었는지 미리 선언하여 웹브라우저가 내용을 올바로 표시할 수 있도록 해주는 것** 이다. `<!DOCTYPE>` 으로 선언하는데 이걸 해주지 않으면 **호환 모드(quirks mode)** 로 동작한다. 호환 모드의 경우 각 브라우저마다 문서를 나타내는 방식이 다르기 때문에 크로스 브라우징 이슈가 훨씬 심해지게 된다.

## DTD(Document Type Definition)

DTD(Document Type Definition)란 문서 형식을 정의해놓은 것으로 DOCTYPE을 명시할 때 사용한다. 즉, HTML 문서가 어떤 문서 형식을 따르는지 DOCTYPE에서 DTD를 지정하는 것이다.

예시로 아래와 같은 것들이 있고 [W3C Recommended list of Doctype declarations](https://www.w3.org/QA/2002/04/valid-dtd-list.html) 에서 더욱 자세하게 확인 가능하다.

* XHTML 1.1
* XHTML 1.0
  * Strict DTD
  * Transitional DTD
  * Frameset DTD
* HTML 4.01
  * Strict DTD
  * Transitional DTD
  * Frameset DTD
* HTML 5

현 시점에선, HTML 5의 DTD로 DOCTYPE을 명시하는 것이 제일 바람직하다.

```html
<!DOCTYPE html>
```

<br>

## 참고

* [What is DOCTYPE?](https://stackoverflow.com/questions/414891/what-is-doctype)
* [비표준 모드 quirks mode, 표준 모드 standards mode 차이와 DOCTYPE](https://aboooks.tistory.com/169)
* [DOCTYPE(문서형 정의) 선언](https://webdir.tistory.com/40)
* [What is difference between XHTML and HTML?](https://stackoverflow.com/questions/4153403/what-is-difference-between-xhtml-and-html)
