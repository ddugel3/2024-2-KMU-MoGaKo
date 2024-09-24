<h1>3주차 - 리액트 훅 2</h1>

<h4>useCallback</h4>
useMemo 처럼 캐싱 역할을 하는 훅이다<br>
useMemo와 다른 점은 useCallback은 콜백함수를 저장한다<br>

```javascript
const 함수명 = useCallback(() => {
    // 실행될 함수 내용
}, [의존성목록]);
```

예시 - number가 변경될 때 마다 콘솔에 출력

```javascript
const someFunction = useCallback(() => {
    console.log(`someFunc: number : ${number}`);
    return;
}, [number]);
```

<h4>useLayoutEffect</h4>
useEffect와 동일한 작업을 수행하지만 useEffect와 달리 동기적으로
실행되기 때문에 useLayoutEffect의 내용이 다 실행된 이후에 화면이 업데이트 된다

```javascript
useLayoutEffect(() => [의존성]);
```

예시 - 너비가 변경될 때마다 상태 업데이트

```javascript
function MyComponent() {
    const refDiv = useRef(null);
    const [divWidth, setDivWidth] = useState(0);

    useLayoutEffect(() => {
        if (refDiv.current) {
            setDivWidth(ref.current.getBoundingClientRect().width);
        }
    }, []);

    return (
        <div ref={refDiv}>
            <p>이 요소의 너비는 {divWidth}px 입니다.</p>
        </div>
    );
}
```

<h4>useRef</h4>
컴포넌트의 참조에 관한 속성.
리액트에서 컴포넌트 선택자로 사용 가능하다 <br>
값이 변경될 때 마다 렌더링이 발생하지 않음

```javascript
const ref명 = useRef(초기값);
<input ref={ref명}/>
```

예시 - 버튼을 누르면 useRef를 설정한 요소를 focus 하는 코드

```javascript
function TextInputWithFocusButton() {
    const inputRef = useRef(null);

    useEffect(() => {
        // 컴포넌트가 마운트될 때 input에 포커스 설정
        inputRef.current.focus();
    }, []);

    return (
        <div>
            <input ref={inputRef} type="text"/>
            <button onClick={() => inputRef.current.focus()}>
                Focus the input
            </button>
        </div>
    );
}
```

예시2 - 타이머 ID를 useRef로 저장하는 코드

```javascript

function Timer() {
    const [count, setCount] = useState(0);
    const timerRef = useRef(null);

    useEffect(() => {
        timerRef.current = setInterval(() => {
            setCount((prev) => prev + 1);
        }, 1000);

        return () => {
            clearInterval(timerRef.current); // 컴포넌트 언마운트 시 타이머 제거
        };
    }, []);

    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={() => clearInterval(timerRef.current)}>Stop Timer</button>
        </div>
    );
}

```
