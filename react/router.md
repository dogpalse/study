# Router
---
6버전으로 업데이트되면서 사용 방법이 많이 바꼈다.  
`<Switch>` -> `<Routes>`  
`<Route path='' component={ Component } />` -> `<Route path='' element={<Component />} />`
> Reference
> [공식문서](reactrouter.com)

### 1. 개념
라우팅: 사용자가 요청한 URL에 맞는 페이지를 보여주는 것

### 2. 사용
####  Intallation
```bash
$ npm install react-router-dom
# or
$ yarn add react-router-dom
```

#### BrowserRouter
라우터를 적용하고자 하는 컴포넌트의 최상위에 `<BrowserRouter>` 적용
```javascript
import { render } from 'react-dom';
import { BrowserRouter } from 'react-router-dom';
import App from './App';

const rootElement = document.getElementById('root');
render(
    <BrowserRouter>
        <App />
    </BrowserRouter>,
    rootElement
)
```

#### Route
`<Route>`를 적용하기 위해 `<Routes>`로 감싼다.
```javascript
import { Routes, Route } from 'react-router-dom';
import Home from './routes/Home';
import Invoices from './routes/Invoices';
import Expenses from './routes/Expenses';

export default function App() {
    return (
        <Routes>
            <Route path='/' element={<Home />} />
            <Route path='/invoices' element={<Invoices />} />
            <Route path='/Expenses' element={<Expenses />} />
        </Routes>
    );
}
```

#### useRoutes
배열로 라우팅 설정

```javascript
import { useRoutes } from 'react-router-dom';
import Layout from './layouts/Layout';
import Home from './routes/Home';
import Invoices from './routes/Invoices';
import Expenses from './routes/Expenses';

export default function App() {
    const element = useRoutes([
        {
            path: '/',
            element: <Layout />,
            children: [
                {
                    index: true, element: <Home />
                },
                {
                    path: 'invoices', element: <Invoices />
                },
                {
                    path: 'expenses', element: <Expenses />
                }
            ]
        }
    ]);

    return element;
}
```

#### Link
리액트에서는 페이지 이동 시 `<a>` 대신 `<Link>` 사용
```javascript
import { Link } from 'react-router-dom';

export default function Nav() {
    return (
        <nav>
            <Link to='/'>Home</Link>
            <Link to='/invoices'>Invoices</Link>
            <Link to='/expenses'>Expenses</Link>
        </nav>
    );
}
```

#### Nested Routes
1. Nested Routes
```javascript
import { Routes, Route } from 'react-router-dom';
import Home from './routes/Home';
import Invoices from './routes/Invoices';
import Expenses from './routes/Expenses';

export default function App() {
    return (
        <Routes>
            <Route path='/' element={<Home />}>
                <Route path='invoices' element={<Invoices />} />
                <Route path='expenses' element={<Expenses />} />
            </Route>
        </Routes>
    );
}
```
2. Outlet
```javascript
import { Outlet, Link } from 'react-router-dom';

export default function Home() {
    return (
        <div>
            <h1>Home</h1>
            <nav>
                <Link to='/invoices'>Invoices</Link>
                <Link to='/expenses'>Expenses</Link>
            </nav>
            <Outlet />
        </div>
    );
}
```
부모 컴포넌트(Home)에서 `<Outlet />`에 라우팅된 자식 컴포넌트를 렌더링.

#### No Match Route
path에 '*'을 값으로 넘겨준다
```javascript
import { Routes, Route } from 'react-router-dom';
import Home from './routes/Home';
import Invoices from './routes/Invoices';
import Expenses from './routes/Expenses';

export default function App() {
    return (
        <Routes>
            <Route path='/' element={<Home />}>
                <Route path='invoices' element={<Invoices />} />
                <Route path='expenses' element={<Expenses />} />
                <Route path='*' element={
                    <main>
                        <p>해당 페이지는 존재하지 않습니다.</p>
                    </main>
                }>
            </Route>
        </Routes>
    )
}
```

#### URL Params
적용할 URL 라우터에 Nested Route 적용
해당 컴포넌트에서 useParams 사용
```javascript
import { Routes, Route } from 'react-router-dom';
import Home from './routes/Home';
import Invoices from './routes/Invoices';
import Expenses from './routes/Expenses';

export default function App() {
    return (
        <Routes>
            <Route path='/' element={<Home />}>
                <Route path='invoices' element={<Invoices />}>
                    <Route path=':invoiceId' element={<Invoices />} />
                </Route>
                <Route path='expenses' element={<Expenses />} />
                <Route path='*' element={
                    <main>
                        <p>해당 페이지는 존재하지 않습니다.</p>
                    </main>
                }>
            </Route>
        </Routes>
    )
}
``` 
```javascript
import { useParams } from 'react-router-dom';

export default function Invoices() {
    let { invoiceId } = useParams();        // 비구조 할당

    return (
        <h1>Invoices</h1>
        {invoiceId ? <p>{invoiceId}</p> : null}
    );
}
```
`<Route>`의 path에 적용한 ":invoiceId"를 useParams().invoiceId에 매핑
useParams의 값은 항상 문자열.

#### Index Route
 - `<Route>`의 path 대신해 index 사용
 - 부모와 같은 경로면서 다른 자식들과 경로가 같으면 안된다.
 - 부모 라우트의 디폴트 자식 라우트.
```javascript
import { Routes, Route } from 'react-router-dom';
import Home from './routes/Home';
import Invoices from './routes/Invoices';
import Expenses from './routes/Expenses';

export default function App() {
    return (
        <Routes>
            <Route path='/' element={<Home />}>
                <Route path='invoices'>
                    <Route index element={
                        <main>
                            <p>Invoice 선택...!</p>
                        </main>
                    }/>
                    <Route path=':invoiceId' element={<Invoices />} />
                </Route>
                <Route path='expenses' element={<Expenses />} />
                <Route path='*' element={
                    <main>
                        <p>해당 페이지는 존재하지 않습니다.</p>
                    </main>
                }>
            </Route>
        </Routes>
    )
}
``` 
```javascript
import { useParams } from 'react-router-dom';

export default function Invoices() {
    let { invoiceId } = useParams();        // 비구조 할당

    return (
        <h1>Invoices</h1>
        {invoiceId ? <p>{invoiceId}</p> : null}
    );
}
```

#### Query String
해당 컴포넌트에서 useSearchParams 사용
```javascript
import { Routes, Route } from 'react-router-dom';
import Home from './routes/Home';
import Invoices from './routes/Invoices';
import Expenses from './routes/Expenses';

export default function App() {
    return (
        <Routes>
            <Route path='/' element={<Home />}>
                <Route path='invoices' element={<Invoices />}>
                    <Route path=':invoiceId' element={<Invoices />} />
                </Route>
                <Route path='expenses' element={<Expenses />} />
                <Route path='*' element={
                    <main>
                        <p>해당 페이지는 존재하지 않습니다.</p>
                    </main>
                }>
            </Route>
        </Routes>
    )
}
``` 
```javascript
import { useSearchParams } from 'react-router-dom';

export default function Invoices() {
    const [ searchParams, setSearchParams ] = useSearchParams();
    const id = searchParams.get('id');
    const mode = searchParams.get('mode');

    return (
        <h1>Invoices</h1>
        <p>{id}</p>
        <p>{mode}</p>
    );
}
```

