## **Hook이란?**
- 특별한 함수! 예를 들어 useState를 이용하여 state를 함수 컴포넌트 안에서 사용가능하게 해줌


#### **without classes**


```
const Example = (props) => {
    //Hook 사용 가능
    return <div />;
}
```
```
function Example(props){
    //Hook 사용 가능
    return<div />;
}
```
- React의 함수 컴포넌트는 위와 같이 생겼다.

- Hook은 클래스 안에서 동작을 하진 않으며, 클래스를 작성하지 않고 사용할 수 있다.

## **Hook 사용 타이밍**
- 함수 컴포넌트를 사용하다가 state를 추가하고 싶을 때 클래스 컴포넌트로 바꾸는 번거로움 대신 --> Hook을 이용하여 state사용


## **UseState**


```
import React, {useState} from 'react';

function Example(){
    //새로운 state변수를 선언하고, 이것을 count라고 부름
    const [count, setCount]=useState(0);
}
```


#### **useState() Hook의 인자로 넘겨주는 값**
 - state의 초기 값이며, 위의 경우에서는 변수 둘다 0으로 저장

 - count변수의 값을 갱신하려면 setCount를 호출하자.
 

#### **useState가 반환하는 값**
 - state변수, 해당 변수를 갱신할 수 있는 함수

#### **state가져오기**
 - 클래스 컴포넌트였을 때는 count갱신 시 this.setState()를 호출했음 (하단참고)
 ```
  <button onClick={() => this.setState({ count: this.state.count + 1 })}>
    Click me
  </button>
  ```
- 반면 함수 컴포넌트는 setCount와 count변수 사용으로 this 호출 불필요
```
<button onClick={() => setCount(count + 1)}>
    Click me
  </button>
```

