# local storage vs session storage vs cookie

모두 클라이언트 상에서 key/value 쌍을 저장할 수 있는 메커니즘으로 **value는 반드시 문자열** 이어야 한다. 또한 모두 [동일 출처 정책(SOP)](https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/security/sop.md) 을 따르기 때문에 다른 도메인에서 접근할 수 없다.

|               | cookie           | local storage         | session storage         |
| ------------- | ---------------- | --------------------- | ----------------------- |
| 생성자        | 클라이언트/서버  | 클라이언트            | 클라이언트              |
| 지속시간      | 설정 여부에 따름 | 명시적으로 지울때까지 | 탭 / 윈도우 닫을 때까지 |
| 용량          | 5KB              | 5MB / 10MB            | 5MB                     |
| 서버와의 통신 | O                | X                     | X                       |
| 취약점        | XSS / CSRF 공격  | XSS 공격              | XSS 공격                |

<br>

## 참고

* [What is the difference between localStorage, sessionStorage, session and cookies?](https://stackoverflow.com/questions/19867599/what-is-the-difference-between-localstorage-sessionstorage-session-and-cookies)
* [프론트엔드 인터뷰 핸드북, `cookie`, `sessionStorage`, `localStorage` 사이의 차이점을 설명하세요](https://github.com/yangshun/front-end-interview-handbook/blob/master/Translations/Korean/questions/html-questions.md#cookie-sessionstorage-localstorage-사이의-차이점을-설명하세요)
* [Local Storage vs Cookies](https://stackoverflow.com/questions/3220660/local-storage-vs-cookies)