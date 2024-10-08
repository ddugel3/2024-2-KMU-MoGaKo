<h1>5주차 - 리덕스</h1>

<h2>리덕스</h2>
리액트 에서의 상태관리 라이브러리<br>
여러 컴포넌트가 공유하는 상태를 구현하는 플럭스 규격의 라이브러리 일종이다.<br>
리덕스를 사용하면 다른 컴포넌트로 state를 전달 할 때 props를 
이용해서 하위 컴포넌트로 하나씩 옮길 필요 없이 state를 저장해서 
따로 관리하고 필요할 때 마다 어떤 컴포넌트 에서든 꺼내서 사용 할 수 있다. 
그래서 자식이 많아져도 상태 관리가 편해진다<br>

리덕스의 상태관리는 상태값을 컴포넌트 내부가 아닌 외부의 store에서 
관리한다.

<h3>상태 관리 lifecycle</h3>
Action이라는 상태를 운반할 객체를 dispatch()메소드를 이용해서
리듀서에 전달하면 리듀서는 상태가 보관된 store에서 상태를 변경한다

<h3>예시</h3>
<h4>rootReducer</h4>
```javascript
// reducers/index.js

/** root reducer */
import { combineReducers } from "redux";
import counter from "./counter";

// 여러 reducer를 하나로 묶어주는 메소드
// store에는 하나의 reducer만 저장
const rootReducer = combineReducers({
  counter
});

export default rootReducer;
```
<h4>Reducer</h4>
```javascript
// reducers/counter.js

// reducer가 많을 때 action상수의 중복을 막기위해 
// 파일명 + 액션이름을 사용
export const INCRESE = "COUNT/INCRESE";

export const increseCount = count => ({ type: INCRESE, count });

const initalState = {
    count: 0
};

const counter = (state = initalState, action) => {
    switch (action.type) {
        case INCRESE:
            return {
                ...state,
                count: action.count
            };
            
        default:
            return state;
    }
};
```
<h4>Store</h4>
```javascript
// index.js
import React from "react";
import ReactDOM from "react-dom";
import { createStore, applyMiddleware, compose } from "redux";
import { Provider } from "react-redux";
import logger from "redux-logger";
import { composeWithDevTools } from "redux-devtools-extension";

import App from "./App";
import rootReducer from "./reducers";

// 배포 레벨에서는 리덕스 발동시 찍히는 logger를 사용하지 않습니다.
const enhancer =
  process.env.NODE_ENV === "production"
    ? compose(applyMiddleware())
    : composeWithDevTools(applyMiddleware(logger));

// 위에서 만든 reducer를 스토어 만들때 넣어줍니다
const store = createStore(rootReducer, enhancer);

ReactDOM.render(
  // 만든 store를 앱 상위에 넣어줍니다.
  <Provider store={store}>
    <App />
  </Provider>
  document.getElementById('root'),
);
```
<h4>dispatch</h4>
```javascript
import { useSelector, useDispatch } from "react-redux";
import { increseCount } from "reducers/count";

// dispatch를 사용하기 위한 준비
const dispatch = useDispatch();

// store에 접근하여 state 가져오기
const { count } = useSelector(state => state.counter);

const increse = () => {
  // store에 있는 state 바꾸는 함수 실행
  dispatch(increseCount());
};

const Counter = () => {
  return (
    <div>
      {count}
      <button onClick={increse}>증가</button>
    </div>
  );
};

export default Counter;
```
