# ComponentStructure
---
### Why
- 유지보수가 쉽다
- 인터페이스 파악

### 컴포넌트 작성 순서
```javascript
import PropTypes from 'prop-types';

Component.propTypes = {
     
};

export default function Component({ props }) {
    return(
        <div></div>
    );
}

const DATA = [
    {
        name: 'song',
    },
    {
        name: 'kang',
    }.
];
const API_URL = '/components';
function getData() {

}
```
- 최상단에 props의 타입 정의
- 컴포넌트 외부에서 상수를 정의해서 사용 --> 불필요한 렌더링 회피

### props 타입 정의
##### `prop-types` 패키지 설치
```bash
$ npm install prop-types
```

##### `prop-types` 사용법
```javascript
import PropTypes from 'prop-types';

Component.propTypes = {
    name: PropTypes.string.isRequired,
    age: PropTypes.number,
    users: PropTypes.array,
    type: PropTypes.oneOf(['write', 'read']),
    tpyes: PropTypes.oneOfType([PropTypes.object, PropTypes.array]),
    writer: PropTypes.object,
    onChange: PropTypes.func,
    enable: PropTypes.bool,    
};
```
### 조건부 렌더링
##### 조건부 렌더링 사용법
```javascript
export default function Component({ isLogin }) {
    return (
        {!isLogin && <div><h1>로그인 해야합니다!</h1></div>}
        {isLogin && <div>안녕하세요.</div>}
    );
}
```
##### 조건부 렌더링 VS 삼항 연산자

### 프레젠테이션 & 컨테이너 컴포넌트

### 성능 최적화
##### 리렌더링 과정
1. 이전 렌더링을 재사용할지 판단
2. 컴포넌트 호출
3. 변경된 부분 돔에 반영