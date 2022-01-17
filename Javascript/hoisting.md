# Hoisting

- 호이스팅이란 ,인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미.

- 호이스팅이란, 코드 해석을 좀 더 수월하게 하기 위해 environmentRecord의 수집과정을 추상화한 개념. 실행 컨텍스트가 관여하는 코드집단의 최상단으로 끌어올린다.

```javascript
var global = 1;

function outer() {
  var global = 3;
  inner(); // 3이 나올까 1이 나올까?
}

function inner() {
  console.log(global);
}
```

- 변수 선언과 값 할당이 동시에 이루어진 문장은 '선언부'만을 호이스팅 한다.

- 왜 하는가? 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 장점이 있나?

- 변수 영역과 데이터 영역 부분에 메모리 공간을 할당하는 방식이 달라서가 아닐까?

- 선언과 할당이 런타임 시기에 분리되는 현상

https://blog.bitsrc.io/what-is-javascript-hoisting-f0678208eb08

> One of the benefits of hoisting is that it enables us to call functions before they appear in the code

let, const는 hoisting 되나 초기화 하기 전에는 접근 불가능 하다. (TDZ)

**Example**

```javascript
var global = 0;

function outer() {
  console.log(global); // -> undefined
  var global = 5;

  function inner() {
    var global = 10;
    console.log(global); // -> 10
  }

  inner();
  global = 3;
  console.log(global); // -> 3
}
```

## scope

정의 : 식별자에 대한 유효 범위

environmentRecord : 현재 컨텍스트 내의 식별자들에 대한 정보
outerCnvironmentRefernce : 외부 환경 정보

```javascript
function A() {
  function B() {
    function C() {}
  }
}
```
