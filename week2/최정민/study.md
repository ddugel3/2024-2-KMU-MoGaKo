<h1>2주차 - 리액트 훅</h1>
<h2>리액트 훅</h2>
함수 컴포넌트에서 상태관리와 생명 주기 메서드를 사용할 수 있게 해주는 리액트 기능이다
<br>
함수형 컴포넌트에서만 사용해야한다
<h3>리액트 훅 특징</h3>
1. 같은 훅을 여러번 호출 가능하다
2. 함수 몸통이 아닌 곳에서는 사용 불가능하다
3. 비동기 함수를 콜백 함수로 사용 불가능하다
4. 여러 훅 함수를 조합해서 커스텀 훅을 만들 수 있다
<h3>리액트 훅 예시</h3>
<h4>useEffect</h4>
원하는 조건에 따라 콜백 함수를 실행시키는 리액트 훅<br>
의존성 목록을 비우면 모든 업데이트에 대해서 콜백 함수를 실행한다

```javascript
useEffect(() => {
  원하는 콜백함수 내용
}, [의존성 목록]);
```

예시 - count값이 변할 때 마다 문자열을 수정한다

```javascript
useEffect(() => {
  str = `You clicked ${count} times`;
}, [count]);
```

<h4>useState</h4>
상태를 관리하기 위해서 사용하는 훅<br>
상태관리를 통해서 동적인 웹페이지를 구현할 수 있다

```javascript
const [state변수, state변경 함수] = useState(초기값);//선언
state변경함수(변경할 값);//사용
```
예시 - 버튼을 클릭하면 count 값을 변경함

```javascript
function App() {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => {setCount(count + 1);}}><!--증가-->
      </button>
      <h1>{ count }</h1>
      <button onClick={() => {setCount(count - 1);}}><!--감소-->
      </button>
    </>
  );
}
```

<h4>useMemo</h4>
값을 저장하기 위해서 사용하는 훅<br>
복잡한 연산을 필요로 하는 변수를 미리 저장해 두면 컴포넌트가 재 렌더링 될 때 다시 연산 하지 않아도 된다<br>
첫 렌더링 이후 지정한 의존성 변수가 변할 때만 해당 값을 다시 연산한다

```javascript
const 저장할변수 = useMemo(() => {
    연산 내용
    return 저장할 결과값
},[의존성])
```

return해서 값을 저장하지 않고 연산만 새로 할 수도 있다

```javascript
useMemo(() => {
    연산 내용
},[의존성])
```

예시 - blue와 red가 변경될 때 마다 해당 값을 가져옴

```javascript
function Info({ blue, red }: any) {
  useMemo(() => getBlue(blue), [blue])
  useMemo(() => getRed(red), [red])
  return (
    <div>
      <p>blue {blue}</p>
      <p>red {red}</p>
    </div>
  )
}
```
