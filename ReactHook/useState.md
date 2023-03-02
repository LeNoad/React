## React Hook
---
## useState()
- useState는 컴포넌트에서 state값을 추가할 때 사용된다. 함수형 컴포넌트에서는 클래스형 컴포넌트처럼 state를 사용할 수 없어, Hook을 사용해서 state와 같은 기능을 할 수 있도록 만들어준다.

- 하나의 useState 함수는 하나의 상태 값만 관리를 할 수 있어 만약에 컴포넌트에서 관리해야 할 상태가 여러 개라면, useState를 여러번 사용해야 한다.

# 1. import 해오기
```javascript
import React, { useState } from 'react';
```

# 2. useState 선언하기
```javascript
const [count, setCount] = useState(0);
```

## const[count, setCount]
useState()가 호출되면 배열을 반환하는데,  그 배열의 첫번째 원소는 상태값이고, 두번째 원소는 상태를 업데이트하는 함수이다. 이 함수에 파라미터를 넣어서 호출하게 되면, 전달받은 파라미터로 값이 바뀌게 되고, 컴포넌트는 정상적으로 리렌더링 된다.

## setCount
>count값을 업데이트하는 함수, 클래스 컴포넌트에서의 this.setState는 이전 state와 새로운 state를 합치지만, 이친구는 이전값을 덮어쓴다.

## useState(0)
>숫자 0은 초기값을 의미, useState는 인자로 초기 state 설정값을 하나 받는다. 이 초기값을 첫 번째 렌더링 시에 딱 한번 사용된다.

# 3. setCount 사용해서 상태값 변경하기
여기서 setCount는 비동기로 처리가 된다. 비동기는 응답과 상관없이 다음 동작을 처리하는 방식이다.
비동기로 처리되는 이유는 이 함수가 호출 될때 마다 화면을 다시 그리기 때문에 성능이슈가 생길 수 있어서 그렇다.

```javascript
functiuon Example() {
    const[count, setCount] = useState(0);
    return (
        <div>
            <p>You Clicked {count} time </p>
            <button onClick={() => setCount(count+1)}/>
        </div>
    )
}
```