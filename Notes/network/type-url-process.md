# URL을 입력하고 벌어지는 일

* URL을 웹 브라우저의 주소창에 입력한다.
* 웹 브라우저가 URL을 해석하고, 문법에 맞지 않으면 기본 검색엔진으로 검색한다.
* 문법에 맞으면 URL의 호스트 부분을 인코딩한다.
* HSTS(HTTP Strict Transport Security) 목록을 확인하고 있으면 HTTPS로, 없으면 HTTP로 요청한다.
* DNS(Domain Name Server) 조회
  * 브라우저/로컬 캐시 확인해서 도메인에 해당하는 IP가 있는지 확인한다.
  * 없으면 OS에게 DNS 서버에 요청하라고 지시한다.
  * DNS 서버는 해당 도메인에 해당하는 IP를 돌려준다.
* TCP 소켓을 열고 3-way handshake로 연결을 설정한다.
* HTTPS 요청이라면 TLS(Transport Layer Security) handshake 과정을 통해 세션키를 생성한다.
* 세션이 유지되는 동안 서버에게 요청하고 응답을 받는 과정을 반복한다.
  * 응답 상태코드에 따라 다르게 처리한다.
  * 응답을 디코딩(Decoding)하고 캐싱 가능하다면 캐싱한다.
* 웹브라우저는 응답받은 HTML/CSS/JS 및 이미지,폰트 등의 리소스를 사용하여 렌더링 한다.
* 서버와의 세션이 종료되면 4-way handshake로 연결을 종료한다.

<br>

## 참고

* [Github, what-happens-when-KR](https://github.com/SantonyChoi/what-happens-when-KR)
* [Stackoverflow, what happens when you type in a URL in browser](https://stackoverflow.com/questions/2092527/what-happens-when-you-type-in-a-url-in-browser)