# Generator

하나의 값만을 리턴할 수 있는 일반함수와 달리, 제너레이터 함수는 여러개의 값을 하나씩 반환할 수 있다.
제너레이터 함수와 이터러블은 무슨 관련이 있을까?

1. 동작방식

   제너레이터 함수를 호출하면 코드가 실행되는 것이 아니라, `제너레이터 객체`가 반환된다.

   제너레이터 객체의 `next()`메소드를 실행하면 제너레이터 함수 내부의 yield문을 만날 때 까지 실행된다.

2. 선언 방식

   ```javascript
   function* generator() {}
   ```

   Arrow function으로도 제너레이터 함수를 만들 수 있을까?

3. generator === iterable object?

   이터러블 객체란 배열을 일반화 한 객체이다. `for..of` 문법을 이용하면 쉽게 어떤 객체의 내부를 순회할 수 있다.

   - for...of 문법은 객체에 `Symbol.iterator` 속성이 존재해야 사용가능하다.

   제너레이터는 이터레이터를 어떻게 하면 쉽게 구현할지를 염두에 두며 자바스크립트에 추가되었습니다.

4. 비동기 이터레이터 Symbol.asyncIterator

   symbol.iterator 대신 symbol.asynciterator 사용 & next는 Promise 반환.

참고
https://meetup.toast.com/posts/73

single thread , non-blocking IO이면 cps 방식을 사용해야하나?
