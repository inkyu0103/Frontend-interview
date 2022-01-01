# JWT (JSON Web Token)

고려해야할 두 가지 공격

1. xss (cross site script)
   사이트 내부에 악의적인 스크립트를 심는 것

-> localStorage에 token을 저장하는 경우, localStorage.getItem() 등으로 직접 값을 가져올 수 있음.

-> 쿠키에 들어있더라도 접근 가능 (httpOnly설정을 통해 방어 가능)

2. csrf (cross site request forgery)
   사용자 권한을 탈취하는 것 (악의적인 사이트에 들어오게 한다거나...)
   해커 서버에 요청을 보내는 스크립트를 넣어놓으면, 사용자가 접속해서 해커 서버에 요청을 넣고, 같이 가지고 있던 쿠키나 이런 것들도 넘어가게 된다.

Referer check
백엔드에서 도메인이 일치하는지 확인하는 작업

CSRF Token
임의의 난수를 생성하고 사용자 브라우저에 저장하여 확인함

same-site cookie
