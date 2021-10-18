# **Hook이란?**
- 특별한 함수! 예를 들어 useState를 이용하여 state를 함수 컴포넌트 안에서 사용가능하게 해줌


### **without classes**


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

### **Hook 사용 타이밍**
- 함수 컴포넌트를 사용하다가 state를 추가하고 싶을 때 클래스 컴포넌트로 바꾸는 번거로움 대신 --> Hook을 이용하여 state사용


## **UseState**


```
import React, {useState} from 'react';

function Example(){
    //새로운 state변수를 선언하고, 이것을 count라고 부름
    const [count, setCount]=useState(0);
}
```


### **useState() Hook의 인자로 넘겨주는 값**
 - state의 초기 값이며, 위의 경우에서는 변수 둘다 0으로 저장

 - count변수의 값을 갱신하려면 setCount를 호출하자.
 

### **useState가 반환하는 값**
 - state변수, 해당 변수를 갱신할 수 있는 함수

 ### **state가져오기**
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


### **메모이제이션 훅 : useMemo, useCallback**


#### **useMemo**
- 계산량이 많은 함수의 반환값을 재활용하는 용도로 사용됨.

```
import React, {useMemo} from 'react';
import {runExpensiveJob} from './util';

function MyComponent({v1,v2}){
  const value = useMemo(() => runExpensiveJob(v1,v2),[v1,v2]);
  return <p>{'value is ${value}'}</p>;
}
```
- useMemo 훅의 첫번째 매개변수로 함수를 입력한다. useMemo 훅은 이 함수가 반환된 값을 기억한다.


#### **useCallback**
- 리액트의 렌더링 성능을 위해 제공되는 훅이다. 불필요한 렌더링을 막을 수 있음.

```
import React, {useState} from 'react';
import {saveToServer} from './api';
import UserEdit from'./UserEdit';

function Profile(){
  const [name, setName] = useState('');
  const [age, setAge] =useState(0);
  return(
    <div>
    <p>{'name is ${name}'}</p>
    <p>{'age is ${age}'}</p>
    <UserEdit
      onSave={()=>saveToServer(name,age)}
      setName={setName}
      setAge={setAge}
    />
    </div>
  );
}
```
- 상단의 코드에선 UserEdit 컴포넌트에서 PureComponent 혹은 React.memo를 사용해도 onSave 속성값이 항상 변경되는 불필요한 렌더링이 발생한다.

```
//...
function Profile(){
  const [name, setName] = useState('');
  const [age, setAge] =useState(0);
  const onSave = useCallback() => saveToServer(name,age),[name,age]);
  return(
    <p>{'name is ${name}'}</p>
    <p>{'age is ${age}'}</p>
    <UserEdit onSave={onSave} setName={setName} setAge={setAge}/>
    </div>
  );
}
```
- useCallback 훅을 사용하면 이전에 onSave 속성값으로 전달했던 것과 같은 함수를 useCallback 훅의 첫번째 매개변수로 입력한다. 
- 두번째 매개변수로 전달한 배열의 값이 변경되지 않으면 이전에 생성한 함수가 재사용되므로 name과 age값이 변경되지 않는 이상 UserEdit 컴포넌트의 onSave 속성값으로 항상 같은 함수가 전달된다.