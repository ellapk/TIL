## **Element**
- 엘리먼트는 리액트 앱의 가장 작은 단위

- 화면에 표시할 내용을 기술한다.
```
const element = <h1>Hi Hi Hi</h1>;
```

- 불변객체로서, 생성한 이후 해당 엘리먼트의 자식이나 속성 변경 못함


## **엘리먼트 vs 컴포넌트**
- 엘리먼트는 [컴포넌트](Component&Props.md)의 "구성요소" 일뿐 혼동금지


## **엘리먼트 rendering**
- 리액트 엘리먼트를 루트 DOM 노드에 렌더링 하려면**ReactDOM.render()** 로 전달
```
const element=<h1>Hi Hi Hi</h1>;
ReactDOM.render(element,document.getElementById('root'));
```
