# **Redux?**

- js를 위한 상태 관리 프레임워크

## **Redux 사용시 따라야할 원칙**

**1. 전체 상탯값을 하나의 객체에 저장한다.**
- 전체 상탯값이 하나의 자바스크립트 객체로 표현되기 때문에 활용도가 높아짐.


**2. 상탯값은 불변 객체다.**

- 상탯값은 오직 액션 객체에 의해서만 변경되어야 한다.


```
const incrementAction = {
    type : 'INCREMENT',
//action 객체는 type 속성값이 존재한다.
//type 속성 값으로 액션 객체를 구분함
    amount: 123,
//type 속성값 제외 나머지는 상탯값 수정을 위해 사용되는 정보
};

const conditionalIncrementAction = {
    type : 'CONDITIONAL_INCREMENT',
    amout : 2,
    gt : 10,
    lt : 100,
};
store.dispatch(incrementAction);
//액션 객체 + dispatch 메서드 호출시 상탯값 변경가능

store.dispatch(conditionalIncrementAction);

```


**3. 상탯값은 순수 함수에 의해서만 변경되어야 한다.**


- reducer : 리덕스에서 상탯값을 변경하는 함수

>(state,action)=>nextState


