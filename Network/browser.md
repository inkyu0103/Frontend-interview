# 브라우저에 google.com을 치면 발생하는 일

1. 브라우저에서 DNS 캐싱을 확인한다

   - 브라우저 캐시 확인
   - OS 캐시 확인
   - **router 캐시** 확인
   - **ISP(Internet Sevice Provider) 캐시** 확인

2. 요청한 URL이 캐시에 없는 경우, ISP의 DNS 어버가 www.google.com을 호스팅 하고 있는 서버의 IP 주소를 찾기 위해 DNS query를 날린다.
