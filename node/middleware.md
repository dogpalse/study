# Middleware
요청과 응답 사이에서 동작하며 요청과 응답을 조작한다.

## 사용법
`app.use`와 `app.get`, `app.post`와 같은 http 메서드에 적용한다.
`app.use`는 `app.use((req, res, next) => {})`  
`app.get`는 `app.get('/', (req,res, next) => {})`  

에러 처리 미들웨어는 인수 4개 적용.  
`app.use((err, req, res, next) => {})`
```javascript
app.use((req, res, next) => {
    next();
});
app.get('/', (req, res, next) => {
    next();
}, (req, res, next) => {

});
app.use((err, req, res, next) => {
    res.status(500).send(err.message);
})
```

`next`는 다음 미들웨어로 넘어가는 함수이다.  
위 `app.get()`처럼 미들웨어를 여러 개 연결할 수 있다. 해당 미들웨어에서도 next()를 해야 다음 미들웨어가 실행된다.


## 미들웨어 패키지
### 1. morgan
요청과 응답의 정보를 로깅하는 미들웨어다.
#### 설치
```bash
$ npm i morgan
```
#### 적용
```javascript
const logger = require('morgan');

app.use(logger('dev'));
```
인수 값으로 'dev', 'combined', 'common', 'short', 'tiny' 등이 올 수 있다.

### 2. static
express 모듈에서 제공해주는 미들웨어이며 정적인 파일을 제공해주는 라우터 역할을 한다.
#### 적용
```javascript
app.use('요청 경로', express.static('정적 파일 경로'));
app.use('/', express.static(path.join(__dirname, 'pulic')));
```


### 3. body-parser
요청의 body에 있는 데이터를 처리해 req.body에 저장.  
#### 적용
```javascript
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
```
`express.json()`은 JSON 형식의 데이터를 req.body에 저장.  
`express.urlencoded()`은 URL-encoded(Ex, 폼 데이터) 형식의 데이터를 req.body에 저장.  
`extended` 값이 `true`이면 `qs` 모듈 사용, `false`이면 node의 `querystring` 사용.  
`qs` 모듈은 `npm install qs`로 설치 필요.


### 4. cookie-parser
요청에 포함된 쿠키를 req.cookies 객체 또는 쿠키에 서명이 있을 경우 req.signedCookies 객체에 저장하는 미들웨어.
#### 설치
```bash
$ npm i cookie-parser
```
#### 적용
```javascript
app.use(cookeiparser('cookie_secret key'));
```
`cookie_secret key`를 통해 만들어진 서명을 쿠키 뒤에 붙인다.

#### 쿠키 생성 및 제거
```javascript
// 쿠키 생성
// res.cookie(key, value, option)
res.cookie('name', 'song', {
    expires: new Date(Date.now() + 100000),
    httpOnly: true,         // js애서 접근 불가능하게 설정
    secure: true,           // https 적용
    signed: true            // 서명 포함
});

// 쿠키 제거
// res.clearCookie(key, value, option)
res.clearCookie('name', 'song', {
    httpOnly: true,
    secure: true,
    signed: true
});
```
**쿠키 제거 시 expires나 maxAge을 제외한 옵션 값이 일치해야 한다.*

### 5. express-session
세션 관리 미들웨어로 세션관리 사용 시 클라이언트에 쿠키를 보낸다.
#### 설치
```bash
$ npm i express-session
```
#### 적용
```javascript
const session =require('express-session');

app.use(session({
    resave: false,
    saveUninitialized: false,
    secret: process.env.COOKIE_SECRET,
    cookie: {
        httpOnly: true,
        secure: false,
    },
    name: 'songbs'
}))
```