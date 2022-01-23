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

위와같은 방법으로 성능을 끌어낼 수 있다면, virtual DOM을 사용하지 않아도 되는거 아니냐는 의문이 있을 수 있겠다.

맞다. 하지만, virtual DOM은 우리가 고려해야할 점들(어떤 노드가 바뀌었고, 값을 추적하고 등...) 을 자동으로 해준다는 점에서, 개발자의 생산성을 높여준다.

## Reconcilitation

일반적으로 트리 구조를 비교하기 위해서는 O(N^3)

근데 휴리스틱한 방식으로 O(N) 만에 비교 끝냄

1. 서로 다른 타입의 두 엘리먼트는 서로 다른 트리를 만들어낸다.
2. 개발자가 key prop을 통해, 여러 렌더링 사이에서 어떤 자식 엘리먼트가 변경되지 않아야 할지 표시해 줄 수 있다.

## Diffing Algorithm

엘리먼트 타입이 다른 경우 : 이전 트리를 버리고 완전히 새로운 트리를 구축한다.
엘리먼트 타입이 같은 경우 : 엘리먼트 속성을 확인하여, 동일한 내역은 유지하고, 변경된 속성들만 갱신한다.

[참고]

- https://tofusand-dev.tistory.com/107

## Key?

관리하는 state가 많을수록 변경된 부분을 찾는 것보다, 처음부터 다시 구성하는 것이 훨씬 효율적이다.

> Key는 React가 어떤 항목을 변경, 추가 또는 삭제할지 식별 하는데 도움을 준다.

인덱스를 key로 사용하는 경우 발생하는 문제는 무엇일까?
렌더링을 하는데에 문제가 발생하는 것은 아니다. 다만, 비효율적인 비교과정을 거칠 뿐.

다음 예시를 생각해보자.

```javascript
// 초기 coinList -> const coinList=["BTC","ETH"]
function showCoin(coinList) {

  ...

  return(
    coinList.map((coin,idx)=>{
      return <div key={idx}>{coin}</div>
    })
  )
}
```

예상 결과

```javascript
  <div key=0>BTC</div>
  <div key=1>ETH</div>
```

이때 coinList에 새로운 코인을 추가했다고 가정해보자.

```javascript
coinList.push("SOL");
console.log(coinList); // ["BTC","ETH","SOL"]
```

예상 결과

```javascript
  <div key=0>BTC</div>
  <div key=1>ETH</div>
  <div key=2>SOL</div>
```
