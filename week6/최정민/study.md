<h1>6주차 - 리덕스2</h1>

<h3>configureStore</h3>

리듀서에서 반환한 상태를 store 객체로 정리하는 역할을 한다<br>
root reducer :여러 리듀서를 하나로 합쳐서 저장, 관리한다 

<h3>예시</h3>

```javascript
const store = configureStore({ 
    reducer: { 
        counter: counterReducer, 
        user: userReducer, 
    }, 
});
```
<h3>useSelector</h3>

redux store에 저장된 상태를 읽어오는데 사용한다<br>

<h3>예시</h3>

```javascript
function Counter() {
    const count = useSelector((state) => state.counter.value); 
    return ( 
        <div> 
            <span>{count}</span> 
        </div> ); 
}
```

<h3>Action</h3>

상태변화를 위해서 사용하는 객체<br>
함께 전달하는 데이터인 payload 필드가 있다.<br>


<h3>예시</h3>

```javascript
// 액션 타입 정의 
const INCREMENT = 'INCREMENT'; 
const DECREMENT = 'DECREMENT'; 
// 액션 크리에이터 정의 
const increment = () => ({ type: INCREMENT }); 
const decrement = () => ({ type: DECREMENT });
```

<h3>reducer </h3>
상태를 변경하는데 사용하는 함수<br>
초기상태와 action을 전달하면 변화된 상태를 반환해 준다

<h4>예시</h4>

```javascript
const initialState = { value: 0 };

function counterReducer(state = initialState, action) {
    switch (action.type) {
        case 'INCREMENT':
            return { value: state.value + 1 };
        case 'DECREMENT':
            return { value: state.value - 1 };
        default:
            return state;
    }
}
```

<h3> 미들웨어 </h3>
액션이 발생하면 리듀서가 작동하기 전에 먼저 동작한다
비동기 작업처리, 로깅, 오류 보고등에 사용된다.

<h4> 예시 </h4>

```javascript
import { applyMiddleware, createStore } from 'redux';
import thunk from 'redux-thunk';
import logger from 'redux-logger';
import rootReducer from './reducers';

const store = createStore(
  rootReducer,
  applyMiddleware(thunk, logger)
);

export default store;


```

