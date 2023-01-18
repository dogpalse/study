# ComponentStructure
---
### Why
- 유지보수가 쉽다
- 인터페이스 파악

### 컴포넌트 작성 순서
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

export default function Component({ props }) {
    return(
        
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

### 조건부 렌더링

### 프레젠테이션 & 컨테이너 컴포넌트
