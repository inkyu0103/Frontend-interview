# Hook

훅 소개

### useState

### useEffect (useLayoutEffect)

### useReducer

### useCallback

### useMemo (vs React.Memo)

훅 동작 방식

- 어떻게 이전 State 혹은 Props를 기억할 수 있는가? Clouser를 이용한다.
  요점은 setState가 state를 변경시키는게 아니기 때문에, setState 호출 이후 로직에서도 state의 값은 이전과 동일하다는 점입니다. 변경된 값은 다음 컴포넌트 함수가 실행될 때 useState가 가져옵니다!

- 훅은 왜 항상 최상단에서 선언되어야 하는가?

- 여러개의 State 훅을 사용한다면?

- 동기적으로 수행되는 것처럼 코드를 작성하려면?

[참조]
https://github.com/facebook/react/blob/c09596cc6021e1f9f8a88179add93f80fc07823b/packages/react/src/ReactHooks.js#L23
https://github.com/facebook/react/blob/c09596cc6021e1f9f8a88179add93f80fc07823b/packages/react/src/ReactCurrentDispatcher.js
https://github.com/facebook/react/blob/c09596cc6021e1f9f8a88179add93f80fc07823b/packages/react-reconciler/src/ReactInternalTypes.js
https://github.com/facebook/react/blob/c09596cc6021e1f9f8a88179add93f80fc07823b/packages/react/src/ReactHooks.js
