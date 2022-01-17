# Life Cycle

![](https://kyun2da.dev/static/69e54fe57da139eabae168b5e8304af4/01645/lifecycle.png)

## 관련 메소드 or Hook

**Mount**

- constructor

- componentDidMount

**Update**

- componentDidUpdate

**Unmount**

- componentWillUmmount

**나머지**

- getDerivedStateFromProps

- sholudComponentUpdate

  ```javascript
  shouldComponentUpdate(nextProps, nextState); // retrun type : boolean (default value :true)
  ```

  기본적으로는 state나 props가 바뀔 때 마다 렌더링 되는 것이 원칙
  이 메소드를 사용해서 기대할 수 있는 것 -> 렌더링을 건너뛸 수 있음?

  > 이 메소드는 **성능최적화**만을 위한 것입니다. 렌더링을 방지하기 위한 목적으로 사용할 경우 버그로 이어질 수 있다.

  Q. 성능최적화 !== 렌더링 방지? , 필요없는 렌더링을 방지하는 것 외에도 , 렌더링을 막아야 하는 경우가 존재할까?

  대안 : React.PureComponent를 사용할 수 있음.

- render

- getSnapshotBeforeUpdate

[참고]
https://ko.reactjs.org/docs/react-component.html#shouldcomponentupdate
