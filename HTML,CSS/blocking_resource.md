# Blocking Resources

보통 HTML이 파싱될 때, script를 만나면 DOM을 그리는 것을 중단하고 script를 download 한다.

그래서 일반적으로 body태그 맨 마지막에 script를 달게 된다.
그러면 페이지 콘텐츠 출력도 막지 않게 된다.

script는 여러 속성을 가지는데 대표적인 것은 defer , async

SPA 같은 경우 초기에 모든 js를 다운받고 추가적인 데이터는 요청하는 방식이라 js가 매우 크다.

- defer

  - 지연 스크립트를 '백 그라운드'에서 다운로드 한다.
  - 만약 백 그라운드에서 하는게 하나의 프로세스로 돌아간다면,
  - 그렇다면 parallel vs concurrent (병렬성은 하나의 작업을 병렬적으로 수행하여 빠르게 마치는 것, 동시성은 같은 여러개의 작업에 대하여 동시에 처리하는 방법)
  - concurrent 하게 처리하는 것일까?

  - DOMContentLoaded 이벤트 발생 전에 지연스크립트가 실행된다.
  - (DOMContentLoaded -> 초기 HTML이 다운로드가 완료된 후 발생하는 이벤트)

- asnyc
  - 이 속성이 붙으면 페이지와 완전히 독립적으로 동작한다.
  - html 페이지는 async 스크립트 다운이 완료되길 기다리지 않고, 페이지 내 콘텐츠 처리 / 출력
  - 근데 async 스크립트 실행 중에는 HTML파싱이 멈춘다.
  - 정확한 순서 예측 불가능 (먼저 다운로드 된 스크립트가 먼저 실행)

@import vs link tag

성능상 차이가 있다는데.. 자료가 없나?
아래 자료 있음

https://csswizardry.com/2018/11/css-and-network-performance/
https://www.miscw.com/page-load-performance-import-vs-link-css-better-13968.html
