# Browser Storage

1. local Storage

2. Session Storage

3. Cookie

공통점

브라우저에 데이터를 저장할 수 있음.

차이점

- 쿠키의 경우 내트워크 요청시 서버로 전송된다.
- 브라우저 스토리지의 경우 서버가 조작할 수 없다.
- 웹 스토리지 객체는 오리진에 묶여있다. ( 프로토콜 / 서브 도메인이 다르면 데이터 접근 불가)

4. 쿠키 vs 세션

- 공통점
- 차이점

  cookie는 client-side에 , session은 server-side에 저장된다.

- 세션

  세션은 웹 사이트의 여러 페이지에서 사용하기 위해서 서버쪽에 정보를 저장해놓는 것이다.
  HTTP 프로토콜은 기본적으로 stateless하기 때문에, 정보를 유지하는 역할을 하지 않는다.