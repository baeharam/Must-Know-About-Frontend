# DOCTYPE

Document Type의 약자로, HTML이 어떤 버전으로 작성되었는지 미리 선언하여 웹브라우저가 내용을 올바로 표시할 수 있도록 해주는 것이다. `<!DOCTYPE>` 으로 선언하는데 이걸 해주지 않으면 **비표준 모드(quirks mode)** 로 동작한다. 비표준 모드의 경우 각 브라우저마다 문서를 나타내는 방식이 다르기 때문에 크로스 브라우징 이슈가 훨씬 심해지게 된다.

## DOCTYPE 선언의 종류

[W3C Recommended list of Doctype declarations](https://www.w3.org/QA/2002/04/valid-dtd-list.html) 에서 더욱 자세하게 확인 가능.

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

여기서 XHTML(eXtensible Hypertext Markup Language)은 XML의 규칙을 따르는 HTML이며 DTD(Document Type Definition)란 문서형을 정의해놓은 것을 말한다. 따라서, HTML 및 XHTML의 각 버전에 따른 DTD가 존재하며 이걸 DOCTYPE으로 선언해서 브라우저가 올바르게 렌더링하게 하는 것이다.

<br>

## 참고

* [What is DOCTYPE?](https://stackoverflow.com/questions/414891/what-is-doctype)

* [비표준 모드 quirks mode, 표준 모드 standards mode 차이와 DOCTYPE](https://aboooks.tistory.com/169)
* [DOCTYPE(문서형 정의) 선언](https://webdir.tistory.com/40)
* [What is difference between XHTML and HTML?](https://stackoverflow.com/questions/4153403/what-is-difference-between-xhtml-and-html)
