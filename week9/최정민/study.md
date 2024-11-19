<h1>리액트 라우팅 2</h1>

<h3>중첩 라우팅</h3>

라우트 안에 또다른 라우트를 포함시키는 형태
복잡한 구조의 UI를 구축할 때 유용하다


<h3>예시</h3>

```javascript
import React from 'react';
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import Home from './Home';
import About from './About';
import Dashboard from './Dashboard';

function App() {
    return (
        <Router>
            <Routes>
                <Route path="/" element={<Home />} />
                <Route path="about" element={<About />} />
                <Route path="dashboard/*" element={<Dashboard />} />
            </Routes>
        </Router>
    );
}

export default App;
```

```javascript
import React from 'react';
import { Routes, Route, Link } from 'react-router-dom';
import Overview from './Overview';
import Settings from './Settings';

function Dashboard() {
    return (
        <div>
            <h1>Dashboard</h1>
            <nav>
                <ul>
                    <li><Link to="overview">Overview</Link></li>
                    <li><Link to="settings">Settings</Link></li>
                </ul>
            </nav>
            <Routes>
                <Route path="overview" element={<Overview />} />
                <Route path="settings" element={<Settings />} />
            </Routes>
        </div>
    );
}

export default Dashboard;

```

<h3>비공개 라우트</h3>

특정 사용자만 해당 경로에 접근 할 수 있도록 설정하는 방법


<h3>방법 1예시</h3>

인증을 받지 않으면 다른 페이지로 연결시킴


```javascript
import React from 'react';
import { Route, Redirect } from 'react-router-dom';

const PrivateRoute = ({ component: Component, isAuthenticated, ...rest }) => (
    <Route
        {...rest}
        render={props =>
            isAuthenticated ? (
                <Component {...props} />
            ) : (
                <Redirect to="/login" />
            )
        }
    />
);

export default PrivateRoute;

```

<h3>방법 2예시</h3>

인증받지 않은 사용자에게 컴포넌트를 보이지 않게 처리함
1. 삼항연산자

```javascript
import React, { useState } from 'react';

function App() {
    const [isLoggedIn, setIsLoggedIn] = useState(false);

    return (
        <div>
            {isLoggedIn ? (
                <h1>Welcome back!</h1>
            ) : (
                <h1>Please sign in.</h1>
            )}
            <button onClick={() => setIsLoggedIn(!isLoggedIn)}>
                {isLoggedIn ? 'Sign out' : 'Sign in'}
            </button>
        </div>
    );
}

export default App;
```

2. && 사용

```javascript
import React, { useState } from 'react';

function Notification({ message }) {
    return <div className="notification">{message}</div>;
}

function App() {
    const [showNotification, setShowNotification] = useState(true);

    return (
        <div>
            {showNotification && <Notification message="You have a new message!" />}
            <button onClick={() => setShowNotification(!showNotification)}>
                {showNotification ? 'Hide Notification' : 'Show Notification'}
            </button>
        </div>
    );
}

export default App;

```

<h3>부트스트랩</h3>

스타일과 레이아웃을 제공하는 CSS프레임 워크
라이브러리를 설치한 후 import 해서 사용 가능하다<br>
classname을 통해서 라이브러리가 제공하는 스타일을 적용 가능하다.

<h4>예시</h4>
Row, Col과  버튼에 스타일을 적용하는 예제

```javascript
import React from 'react';
import { Button, Container, Row, Col } from 'react-bootstrap';
import 'bootstrap/dist/css/bootstrap.min.css';

function App() {
    return (
        <Container>
            <Row className="justify-content-md-center">
                <Col md="auto">
                    <h1>Welcome to My App</h1>
                    <Button variant="primary">Click Me</Button>
                </Col>
            </Row>
        </Container>
    );
}

export default App;
```

