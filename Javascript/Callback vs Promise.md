# Callback vs Promise vs async await

### Callback

1. 정의

   > A callback function is **a function passed into another function as an argument**, which is then invoked inside the outer function to complete some kind of routine or action.

2. 예시

   ```javascript
   //출처 MDN Callback function
   const sayHi = (name) => alert(`Hi, I am ${name}.`);
   const userInput = (callback) => {
     const name = prompt("Please enter your name.");
     callback(name);
   };

   userInput(sayHi);
   ```

   위와 같은 예시는 코드가 동기적으로 수행되는 경우이다.
   일반적으로는 비동기 함수가 완료 된 이후 어떤 일을 수행해야할 지를 콜백함수로 전달한다.
   대표적으로 `setTimeout` 함수가 있다.

   ```javascript
   const sayHi = () => console.log("Hi, I am Inkyu");

   setTimeout(sayHi, 1000); // 1초 뒤에 출력
   ```

3. 왜 사용할까?

### Promise

```javascript
// ES7
async function foo() {
  await bar();
}

// ES5 complied
let foo = (() => {
  var _ref = _asyncToGenerator(function* () {
    yield bar();
  });

  return function foo() {
    return _ref.apply(this, arguments);
  };
})();

function _asyncToGenerator(fn) {
  return function () {
    var gen = fn.apply(this, arguments);
    return new Promise(function (resolve, reject) {
      function step(key, arg) {
        try {
          var info = gen[key](arg);
          var value = info.value;
        } catch (error) {
          reject(error);
          return;
        }
        if (info.done) {
          resolve(value);
        } else {
          return Promise.resolve(value).then(
            function (value) {
              step("next", value);
            },
            function (err) {
              step("throw", err);
            }
          );
        }
      }
      return step("next");
    });
  };
}
```
