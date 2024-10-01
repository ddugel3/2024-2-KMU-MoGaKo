<h1>4주차 - 리액트 훅 3</h1>

<h4>forwardRef</h4>
부모 컴포넌트에서 자녀컴포넌트로 ref를 전달할 때 사용<br>
컴포넌트간에는 기본적으로 공유가 되지 않기 때문

```javascript
forwardRef(props, ref);
```

예시 - child 컴포넌트에 ref를 전달하는 예시

```javascript
const ChildComponent = forwardRef((props, ref) => {
    return <div ref={ref}>I am the child component!</div>;
});

```

<h4>useImperativeHandle</h4>
child component의 상태변경이나 핸들러 호출을
parent component에서 할때 사용<br>
부모 컴포넌트가 자식 컴포넌트의 요소에 접근할 수 있도록 해준다

```javascript
useImperativeHandle(ref, createHandle, [deps])
```

예시 - 부모컴포넌트에서 자식 의 input태그의 값과 focus에 관여 가능하게 하는 코드

```javascript
import React, {useImperativeHandle, useRef, forwardRef} from 'react';

// 자식 컴포넌트
const CustomInput = forwardRef((props, ref) => {
    const inputRef = useRef();

    // useImperativeHandle을 사용하여 부모가 사용할 수 있는 메서드를 정의
    useImperativeHandle(ref, () => ({
        focus: () => {
            inputRef.current.focus();
        },
        clear: () => {
            inputRef.current.value = '';
        }
    }));

    return <input ref={inputRef} type="text"/>;
});

// 부모 컴포넌트
const ParentComponent = () => {
    const inputRef = useRef();

    return (
        <div>
            <CustomInput ref={inputRef}/>
            <button onClick={() => inputRef.current.focus()}>
                Focus Input
            </button>
            <button onClick={() => inputRef.current.clear()}>
                Clear Input
            </button>
        </div>
    );
};

export default ParentComponent;

```

<h4>useContext</h4>
context를 전달할 때 사용한다<br>
context로 전달된 데이터는 부모-자식 관계 뿐만 아니라 하위 컴포넌트 전체에서 접근 가능하다
<br>

```javascript
const MyContext = React.createContext()
const value = useContext(MyContext);
```

예시 - useContext를 이용해서 context를 전달하는 예시

```javascript
const MyContext = createContext();

function ChildComponent() {
    // 3. useContext로 Context 값 접근
    const value = useContext(MyContext);
    return <p>Context Value: {value}</p>;
}

function ParentComponent() {
    const contextValue = "Hello, World!";

    return (
        // 2. Provider를 통해 Context 값 제공
        <MyContext.Provider value={contextValue}>
            <ChildComponent/>
        </MyContext.Provider>
    );
}

export default ParentComponent;
```
