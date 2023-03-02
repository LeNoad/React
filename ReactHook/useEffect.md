## React Hook
---
## 1. useEffect()
>useEffect 함수는 리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 실행할 수 있도록 하는 Hook 이다. useEffect는 Component가 mount 되었을 때, Component가 unmount 되었을때, component가 update 되었을때, 특정 작업을 처리 할 수 있다.

![LifeCycle](/images/ReactLifeCycle.PNG "[ Life Cycle ]")
<h3 style="font-weight:bold; text-align:center;">[ Life Cycle ]</h3>

## useEffect() 사용법
### 기본형태
```javascript
useEffect( function, deps )
```

- function : 수행하고자 하는 작업
- deps : 배열 형태이며, 배열 안에는 검사하고자 하는 특정 값 or 빈 배열 값

### useEffect() 함수 호출
```javascript
import React, { useEffect } from 'react';
```

### 1. Component가 mount 되었을 때
>컴포넌트가 화면에 가장 처음 렌더링 될 때 한번 실행하고 싶을 때는 deps 위치에 빈 배열을 놓는다.
```javascript
useEffect(() => {
    console.log('렌더링 마다 실행')
})
```

### 2. Component가 update 되었을 때
>특정 값이 업데이트 될 때 실행하고 싶을 때는 deps위치에 배열 안에 검사하고 싶은 값을 넣어준다.
```javascript
const mounted = useRef(false);

useEffect(() => {
    if(!mounted.current) {
        mounted.current = true;
    } else {
        //axios
    }
},[바뀌는 값])

// 코드 생략
```

### 3. Component가 unmount 될 때 또는 update 되기 직전
>cleanup 함수 변환 (return 뒤에 나오는 함슁며, useEffect에 대한 뒷정리 함수라고 한다.)