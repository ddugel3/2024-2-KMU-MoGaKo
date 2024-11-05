<h1>리액트 라우팅</h1>

<h3>라우팅</h3>

애플리케이션 내에서 다른 페이지 또는 뷰로 이동하는 과정

<h3>예시</h3>

```javascript
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';
import Contact from './components/Contact';

function App() {
return (
<Router>
<Switch>
<Route exact path="/" component={Home} />
<Route path="/about" component={About} />
<Route path="/contact" component={Contact} />
</Switch>
</Router>
);
}

export default App;
```

<h3>useHistory</h3>

React Router에서 제공하는 훅으로, 프로그래밍 방식으로 네비게이션을 할 때 사용

<h3>예시</h3>

```javascript
import { useHistory } from 'react-router-dom';

function Home() {
const history = useHistory();

    const handleClick = () => {
        history.push('/about');
    };

    return (
        <div>
            <h1>Home Page</h1>
            <button onClick={handleClick}>Go to About Page</button>
        </div>
    );
}

export default Home;
```

<h3>Link 컴포넌트</h3>

기본적으로 HTML의 < a >태그와 유사하게 작동하지만, 
페이지를 리로드하지 않고 네비게이션을 수행

<h3>예시</h3>

```javascript
import { Link } from 'react-router-dom';

function Navigation() {
return (
<nav>
<ul>
<li><Link to="/">Home</Link></li>
<li><Link to="/about">About</Link></li>
<li><Link to="/contact">Contact</Link></li>
</ul>
</nav>
);
}

export default Navigation;
```

<h3>Switch 컴포넌트</h3>

한 번에 하나의 Route만 렌더링하도록 보장하는 컴포넌트

<h3>예시</h3>

```javascript
import { Switch, Route } from 'react-router-dom';

function App() {
return (
<Switch>
<Route exact path="/" component={Home} />
<Route path="/about" component={About} />
<Route path="/contact" component={Contact} />
</Switch>
);
}

export default App;
```
<h3>Route 컴포넌트</h3>

URL 경로와 일치하는 컴포넌트를 렌더링하는 데 사용

<h3>예시</h3>

```javascript
import { Route } from 'react-router-dom';

function App() {
return (
<Route path="/about" component={About} />
);
}
export default
```
