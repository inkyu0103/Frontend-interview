# Closure

### 1. 정의

> 클로저는 함수와 함수가 선언된 어휘적 환경의 조합이다
>
> A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment).

### 2. Lexical Environment

- environmentRecord : 현재 context에서 사용되는 변수에 대한 정보들
- outerEnvironmentRecord : outer scope에서 사용되는 변수에 대한 정보들 (outer lexicalEnvironment에 chaning 되어있음)
- 런타임에 콜스택 상에서 동적으로 결정되는 것이 아니라, 이미 컴파일 타임?에 정해져있음.

```javascript
var global = 5;

function outer() {
  var global = 3;

  function inner() {
    console.log(global); // 3
  }

  inner();
}
```

```javascript
var global = 5;

function outer() {
  var global = 3;
  inner(); // 5
}

function inner() {
  console.log(global);
}
```

### 3. 가비지 컬렉션?

### 4. 클로저 사용이유?

- 정보 은닉

- 콜 스택과 별개의 상태 유지 가능
