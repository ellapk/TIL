## **Components와 Props**
- 컴포넌트는 "props"라고 하는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 React [Element](Element.md)를 반환한다. 


## **함수 컴포넌트와 클래스 컴포넌트**
- 컴포넌트를 정의하는 가장 간단한 방법은 JavaScript함수를 작성하는 것.
```
function welcome(props){
    return <h1>Hello, {props.name}</h1>;
}
```
- 이 함수는 데이터를 가진 하나의 "props(속성을 나타내는 데이터)" 객체를 받은 후 리액트 element를 반환함. = 함수 컴포넌트


## **컴포넌트 렌더링**
- DOM태그가 아닌, 사용자 정의 컴포넌트로 React 엘리먼트를 나타낼 때, (하단참고)
jsx 속성과 자식을 해당 컴포넌트의 단일객체(props)로 전달
```
const element = <Welcome name="Sean" />;
```

- 객체 전달 과정을 다시 살펴보면,
```
function Welcome(props){
    return <h1>Hi, {props.name}</h1>;
}

const element= <Welcome name="Sean" />; 
ReactDOM.render(
    element,document.getElementById('root')
);

```
1. Welcome name="Sean" 엘리먼트로 ReactDOM.render()호출

2. React는 {name:'Sean'}을 props로하여 Welcome 컴포넌트 호출

3. Welcome 컴포넌트는 결과적으로 h1Hello, Sara/h1 엘리먼트를 반환

4. React DOM은 h1Hello,Sara/h1 엘리먼트와 일치하도록 DOM을 효율적으로 업데이트