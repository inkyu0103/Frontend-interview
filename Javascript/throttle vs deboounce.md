# throttle vs debounce

### **공통점**

자주 사용되는 이벤트나 함수들의 실행되는 빈도를 줄여서, 성능 상의 유리함을 가져오기 위한 개념

### Throttle

입력 주기를 방해하지 않고, 일정 시간의 입력을 모아 한 번씩 출력을 제한

[Throttle 구현]

```javascript
const throttle = (callback, delay) => {
  let wating = true;

  return () => {
    if (wating) {
      callback();
      wating = false;
      setTimeout(() => {
        wating = true;
      }, delay);
    }
  };
};
```

### Debounce

입력 주기가 끝나면 출력

[Debounce 구현]

```javascript
const debounce = (callback, delay) => {
  let wating;

  return () => {
    clearTimeout();
  };
};
```

![그림](https://images.velog.io/images/inkyu0103/post/1cc9ebbe-51d0-4cd8-8dcd-faaa37f5034f/image.png)

```javascript
const throttleAndDebounce = () => {
  // 쓰로틀링과 디바운스를 체크하기 위한 변수를 만들어줍니다.
  let throttleCheck, debounceCheck;

  return {
    // throttle과 debounce 모두 실행할 콜백 함수와 실행할 주기를 인자로 받습니다.
    throttle(callback, milliseconds) {
      return function () {
        if (!throttleCheck) {
          // setTimeout을 이용하여 설정한 주기마다 콜백이 실행될 수 있도록 하였고,
          // 실행이 끝난 후에는 다시 throttleCheck를 false로 만들어 주어, 설정한 주기마다 이벤트가 한 번씩만 호출되도록 하였습니다.
          throttleCheck = setTimeout(() => {
            callback(...arguments);
            throttleCheck = false;
          }, milliseconds);
        }
      };
    },

    debounce(callback, milliseconds) {
      return function () {
        // clearTimeout을 이용하여 이벤트 발생을 무시해주고,
        // 마지막 호출 이후, 일정 시간이 지난 후에 단 한 번만, 이벤트가 호출되도록 하였습니다.
        clearTimeout(debounceCheck);
        debounceCheck = setTimeout(() => {
          callback(...arguments);
        }, milliseconds);
      };
    },
  };
};
```
