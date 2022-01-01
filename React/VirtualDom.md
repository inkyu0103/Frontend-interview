# Virtual DOM

## 설명

Virtual DOM은 UI 가상표현을 메모리 상에 두고 **재조정(Reconciliation)** 과정으로 통해 실제 DOM과 동기화 하는 것을 말한다.

(더블 버퍼링 개념)

## 왜 효율적인가?

직접 DOM을 조작하여 repaint 혹은 reflow가 발생하게 되는 경우, 비용이 많이 든다. 특히 다음과 같은 예제를 생각해보자.

```javascript
const app = document.getElementById("root");

for (let i = 0; i < 10; i++) {
  app.innerHTML += "<div>안녕하세요</div>"; // 반복문이 한 번 돌 때마다 수정
}
```

위와 같은 예시에서 발생하는 가장 큰 성능상 문제점은 반복문을 한 번 순회할 때마다 reflow 또는 repaint가 발생한다는 점이다.

리액트의 경우에는 Virtual DOM에서 모든 변화를 적용한 후, Virtual DOM의 내용을 그대로 DOM으로 전달하기 때문에(batch update) 한 번의 reflow repaint를 거치면 된다.

완벽하게 들어맞는 예시는 아니지만, 다음과 같이 수정해볼 수 있겠다.

```javascript
const app = document.getElementById("root");
let childElement = "";

for (let i = 0; i < 10; i++) {
  childElement += "<div>안녕하세요</div>";
}

app.innerHTML = childElement; // 한 번에 반영
```

위와같은 방법으로 성능을 끌어낼 수 있다면, 리액트를 사용하지 않아도 되는거 아니냐는 의문이 있을 수 있겠다.

근데 우리가 언제 이걸 다 찾고 하고 있겠니... 리액트라는 프레임워크가 다 알아서 해주니까~

## Diffing Algorithm

일반적으로 트리 구조를 비교하기 위해서는 O(N^3)

근데 휴리스틱한 방식으로 O(N) 만에 비교 끝냄

[참고]

- https://tofusand-dev.tistory.com/107

## Key?

관리하는 state가 많을수록 변경된 부분을 찾는 것보다, 처음부터 다시 구성하는 것이 훨씬 효율적이다.
