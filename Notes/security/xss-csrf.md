# XSS와 CSRF

## XSS(Cross Site Scripting, 사이트간 스크립팅)

**웹사이트 관리자가 아닌 사람이 웹사이트에 악성 스크립트를 삽입할 수 있는 취약점을 이용한 공격기법이다.** 사용자로부터 받은 입력을 제대로 검증하지 않을 때 나타나며 사용자의 정보를 탈취하거나 비정상적인 기능을 실행할 수 있다.

* **저장 XSS** : 웹사이트에 취약점이 있는 웹 서버에 스크립트를 저장시켜서 해당 웹사이트를 요청하는 사용자로 하여금 스크립트를 실행하게 하는 기법이다.
* **반사 XSS** : 검색을 사용할 때 결과가 없으면 브라우저에서 입력한 값을 문서에 포함하여 응답하는데 이를 사용하여 스크립트를 실행하는 기법으로 악성 URL을 배포하여 클릭하도록 유도하는 방법을 사용한다.
* **DOM 기반 XSS** : 공격 스크립트가 DOM 생성의 일부로 실행되면서 공격하는 기법으로 반사 XSS와 마찬가지로 악성 URL을 배포하여 클릭하도록 유도한다.

XSS 를 사용해서 사용자의 쿠키 정보 및 세션 ID를 획득할 수 있으며 시스템 관리자 권한을 획득할 수도 있다. 대응방안은 아래와 같다.

* **입/출력 값 검증 및 무효화** : 스크립트를 실행할 때는 기본적으로 `<script>` 태그를 사용하니 `<` 를 `&lt;` 로 바꾼다거나 하는 방법으로 무효화시킬 수 있다.
* **보안 라이브러리 사용** : 입/출력이 스크립트를 실행하는지에 대한 필터를 구현한 기존 라이브러리를 사용할 수 있다.

<br>

## CSRF(Cross Site Request Forgery, 사이트간 요청변조)

**사용자가 의도치 않게 공격자가 의도한 행동을 하여 취약점을 노출시키거나 수정/삭제/생성 등을 하게 만드는 공격 기법이다.** 이메일을 열어보거나 악성 사이트에 접근했을 때 특정한 요청을 하는 CSRF 스크립트를 실행하는 방식이다. 다음과 같은 시나리오가 있을 수 있다.

* `www.mybank.com` 에 접속해 있는 상태이다.
* 이 사이트에서 돈을 보낼 때 `http://www.mybank.com/transfer?to=<계좌번호>&amount=<액수>` 형식으로 보낸다고 하자.
* `www.cute-cat.org` 사이트에 접속한다. (악성 사이트이다)
* 해당 사이트의 관리자가 위에서 말한 돈을 보내는 URL과 쿼리 방식을 알고 있다면 그 요청을 실행하는 CSRF 스크립트를 사이트에 넣을 수 있다.
* 사이트에 접속하면 해당 스크립트를 실행하게 되고 `www.mybank.com` 에 요청이 가게 되서 돈을 보내게 된다.

이렇게 사용자가 의도하지 않은 요청을 실행함으로 피해를 줄 수 있는 기법이다. 대응방안은 아래와 같다.

* **`referrer` 검증** : 요청 헤더에 있는 `referrer` 속성을 검증하여 신뢰할 수 있는 도메인에서 들어오는 요청인지 검증한다.
* **CSRF 토큰** : 난수(Random Number)를 서버쪽 사용자의 세션에 저장하고 요청할 때 난수를 CSRF 토큰으로 지정하여 사용자게 전송한다. 이후 요청부터 토큰이 일치하는지 확인하여 검증한다.
* **캡챠(Captcha) 사용** : 사용자와의 상호작용을 통해서 숫자/문자를 입력하여 검증한다.

<br>

## 참고

* [KISA, 크로스 사이트 스크립팅(XSS) 공격 종류 및 대응 방법](https://www.kisa.or.kr/uploadfile/201312/201312161355109566.pdf)
* [Stackoverflow, Difference between XSS and CSRF?](https://security.stackexchange.com/questions/138987/difference-between-xss-and-csrf)
* [Stackoverflow, What is a CSRF token ? What is its importance and how does it work?](https://stackoverflow.com/questions/5207160/what-is-a-csrf-token-what-is-its-importance-and-how-does-it-work)
* [[보안] CSRF(Cross Site Request Forgery)란 무엇인가?](https://sj602.github.io/2018/07/14/what-is-CSRF/)