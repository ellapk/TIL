# **State and Lifecycle**

## **State**

- 사용자가 알 필요 없는 데이터를 내부에서 은닉한다.

- **props** 는(함수 매개변수처럼) 컴포넌트에 전달되는 반면, **state** 는 (함수 내에 선언된 변수처럼)컴포넌트 안에서 관리된다.

**사용법**
- **render()** 함수보다 먼저 **constructor()** 함수를 적어준다. 컴포넌트 생성자에서 **super** 를 호출하기 전에는 **this** 를 사용할 수 없기 때문이다.


***직접 State를 수정하지 말고 !*** 
사용하기
```
//Wrong
this.state.comment='Hello';
```
->
대신 **setState()** 를 사용하기 
```
//Correct
this.setState({comment:'Hello'});
```


## **State 업데이트의 병합**
- **setState()** 를 호출할 때 React는 제공한 객체를 현재 state로 병합한다.
- state는 다양한 독립적인 변수 포함 가능
```
constructor(props){
    super(props);
    this.state={
        posts:[],
        comments:[]
    };
}
```
별도의 **setState()** 호출로 해당 변수들을 독립적으로 업데이트도 가능
```
componentDidMount(){
    fetchPosts().then(response=>{
        this.setState({
            post:response.posts
        });
    });

 fetchCommnets().then(response => {
     this.setState({
         comments:response.comments
     });
 });   
}
```








**함수에서 클래스로 변환**
1. **React.Component** 를 확장하는 동일한 이름의 class 생성.
2. **render()** 라고 불리는 빈 메서드를 추가
3. 함수의 내용을 **render()** 메서드 안으로 옮김.
4. **render()** 내용 안에 있는 **props** 를 **this.props**로 변경
5. 남아있는 빈 함수 선언 삭제


