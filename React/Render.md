## **Render 함수**
- 리액트에서 UI를 사용할 때 필연적으로 눈에 보이는 화면을 구성해줌.

- 컴포넌트의 정보를 이용해 화면을 구성(렌더링)한다.

## **Rendering 순서**
1. 컴포넌트 정의

2. 컴포넌트의 정보를 이용해 렌더링

3. 문자열 형식의 html 코드 반환

4. DOM 요소에 주입



## **배열 Rendring 예시**


**UserList.js**
```
import React from 'react';

function UserList() {
  const users = [
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com'
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com'
    }
    ];
     return (
    <div>
      <div>
        <b>{users[0].username}</b> <span>({users[0].email})</span>
      </div>
      <div>
        <b>{users[1].username}</b> <span>({users[1].email})</span>
      </div>
       </div>
  );
}

export default UserList;
```


- 이제 컴포넌트를 사용하고, map()을 사용하여 동적 배열까지 렌더링해보자
- **map()** 함수는 배열안에 있는 각 원소를 변환하여 새로운 배열을 만들어준다. 일반 데이터 배열을 리액트 엘리먼트로 이루어진 배열로 변환할 수 있음

```
import React from 'react';

function User({ user }) {
  return (
    <div>
      <b>{user.username}</b> <span>({user.email})</span>
    </div>
  );
}

function UserList() {
  const users = [
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com'
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com'
    },
   
  ];

  return (
    <div>
      {users.map(user => (
        <User user={user} />
      ))}
    </div>
  );
}

export default UserList;
```

- 하지만 상단의 코드처럼 렌더링시 **key** 설정을 따로 하지 않으면 기본적으로 배열의 **index** 값을 **key** 로 사용하게되는데, 이는 배열이 업데이트될 때 효율적이지도 못하다.

- 따라서 **key**  props를 설정해야 한다. 이때 이 값은 각 원소들마다 가지고 있는 고유값으로 설정을 해야 한다. 현재로써는 id가 고유 값.

```
import React from 'react';

function User({ user }) {
  return (
    <div>
      <b>{user.username}</b> <span>({user.email})</span>
    </div>
  );
}

function UserList() {
  const users = [
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com'
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com'
    },
  ];

  return (
    <div>
      {users.map(user => (
        <User user={user} key={user.id} />
      ))}
    </div>
  );
}

export default UserList;
```



