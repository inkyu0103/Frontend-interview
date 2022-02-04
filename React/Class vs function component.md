# Class component vs Function component

1. 기본적인 차이
   클래스 컴포넌트와 달리,함수 컴포넌트는 원래 state를 가질 수 없었다.
   그러나 Hook을 통해 함수 컴포넌트도 state를 가질 수 있게 되었다.

   Q. 왜 함수 컴포넌트는 state를 가질 수 없었는가?

   리렌더링 되면, 모두 초기화 되고 다시 할당하기 때문.
   Hook은 클로저를 이용하여, 다른 공간에 값을 보관하기 때문에, 유지 가능

   cf) 클래스 컴포넌트를 작성하기 위해서 보통 다음과 같이 작성한다.

   ```javascript
       import {Component} from 'react'

       class App extends Component{
           ...
       }
   ```

   근데 놀랍게도, Component는 클래스 문법으로 작성된 것이 아니라, (생성자) 함수로 작성되어있다.

   ```javascript
   function Component(props, context, updater) {
     this.props = props;
     this.context = context;
     // If a component has string refs, we will assign a different object later.
     this.refs = emptyObject;
     // We initialize the default updater but the real one gets injected by the
     // renderer.
     this.updater = updater || ReactNoopUpdateQueue;
   }
   ```

2. 생명주기를 사용하는 방식이 다르다

동작에서의 차이

- 함수 컴포넌트는 렌더링된 값을 고정시킨다.
- 함수 컴포넌트의 props는 immutable하다.

- class에서의 this는 mutable 하기 때문에, 예상치 못한 동작을 야기할 수 있다.

[참조]
https://overreacted.io/ko/how-are-function-components-different-from-classes/
