# this

### 0. 정의

this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수(self-reference variable)이다.
this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.
런타임시 결정된다.

### 1. this는 어떻게 결정되는가?

**this값은 함수 호출방식에 의해 동적으로 결정된다.**

- 함수 호출 (엄격 모드가 아닌경우)

  ```javascript
  //1. function
  function outer() {
    console.log(this); // window
  }

  //2. Arrow function
  const outer = () => console.log(this); // error
  ```

  내부함수는 어디서 선언하던 전역 객체를 가리킨다. (설계상 오류)

- 메소드 호출

  ```javascript
  const user = {
    name: "inkyu",
    sayMyName() {
      console.log(`My name is ${this.name}`);
    },
  };

  user.sayMyName(); // My name is inkyu
  ```

  하지만 화살표 함수를 사용하는 경우에는 this가 전역 객체를 가리킨다.

  ```javascript
  const user = {
    name: "inkyu",
    seyMyName: () => {
      `My name is ${this.name}`;
    },
  };

  user.sayMyName(); // My name is
  ```

- 생성자 함수 호출

  생성자 함수 `new` 키워드를 붙여 선언한다.
  일반적인 함수와는 다른 방식으로 값을 리턴한다.

  객체 리터럴과 동일하지만, 재사용가능한 객체 생성 코드를 생성할 수 있다는 점에서 의미가 있다.

  ```javascript
  function User(name) {
    //this = {}
    this.name = name;
    this.level = 1;
    //return this
  }

  const inkyu = User("inkyu");
  console.log(inkyu.name); // 'inkyu'
  console.log(inkyu.level); // 1
  ```

- apply / call / bind 호출

  this binding 이외에 this를 특정 객체에 명시적으로 바인딩하는 방법도 제공.
  매번 헷갈려서 정리해 놓는다.
  apply,call,bind는 모두 함수가 호출하는 것이다.

  **Call**

  **`func.call(객체,인수...)`**

  간단하게 설명하면, call의 첫 번째 인수인 객체가 인수들을 데리고 func 함수를 실행시키도록 하는 것.

  설명이 이상한 것 같으니 MDN의 예시를 직접 보자.

  ```javascript
  function Product(name, price) {
    this.name = name;
    this.price = price;

    if (price < 0) {
      throw RangeError(
        "Cannot create product " + this.name + " with a negative price"
      );
    }
  }

  function Food(name, price) {
    // 생성자와 같은 역할을 한다.
    Product.call(this, name, price);
    this.category = "food";
  }

  function Toy(name, price) {
    // 생성자와 같은 역할을 한다.
    Product.call(this, name, price);
    this.category = "toy";
  }

  var cheese = new Food("feta", 5);
  var fun = new Toy("robot", 40);
  ```

**apply**
Call이 사용되는 인수를 인자로 각각 넘겼다고 하면, apply는 인자들을 배열을 통해 한 번에 넘긴다.

**bind**
call과 apply와 달리 bind는 함수를 반환한다. MDN 예제를 살펴보자.

```javascript
const module = {
  x: 42,
  getX: function () {
    return this.x;
  },
};

const unboundGetX = module.getX;
console.log(unboundGetX()); // 이 실행 결과는 놀랍게도, undefined다. 메소드로 실행하는 것이 아닌, 함수로 실행하는 것이기 때문이다.

const boundGetX = unboundGetX.bind(module);
console.log(boundGetX()); //42
```
