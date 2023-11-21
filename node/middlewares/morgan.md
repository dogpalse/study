# Morgan
Node에서 로깅하는 미들웨어

## 0. 설치
```bash
npm install morgan
# or
yarn add morgan
```

## 1. 옵션
인수 값으로 'dev', 'combined', 'common', 'short', 'tiny' 를 넣어 morgan에서 기본 제공해주는 로그 포멧을 설정.

 - combined : :remote-addr - :remote-user [:date[clf]] ":method :url HTTP/:http-version" :status :res[content-length] ":referrer" ":user-agent"
 - common : :remote-addr - :remote-user [:date[clf]] ":method :url HTTP/:http-version" :status :res[content-length]
 - dev : :method :url :status :response-time ms - :res[content-length]
 - short : :remote-addr :remote-user :method :url HTTP/:http-version :status :res[content-length] - :response-time ms
 - tiny : :method :url :status :res[content-length] - :response-time ms

## 2. 적용

### 기본 포멧 적용
```javascript
const express = require('express');
const logger = require('morgan');

const app = express();

if(process.env.profile == 'prod') {
    app.use(logger('tiny'));
} else {
    app.use(logger('dev'));
}
```

### 커스텀 포멧 지정

```javascript
const express = require('express');
const logger = require('morgan');

const app = express();

if(process.env.profile == 'prod') {
    app.use(logger('[:remote-addr - :remote-user] [:date[web]] :method :url HTTP/:http-version :status :response-time ms'));
} else {
    app.use(logger('dev'));
}
```
