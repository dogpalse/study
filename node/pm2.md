# PM2(Process Manager)
---
Node.js 어플리케이션을 쉽게 관리할 수 있게 도와주는 프로세스 매니저.  

### 프로세스
메모리 상에서 실행중인 프로그램

### 스레드
프로세스 안에서 실행되는 

### PM2의 역할
1. 무중단 서비스
2. 멀티 프로세스(Cluster Mode)
3. 로드 밸런싱
4. 프로세스 모니터링

### PM2 설치
```bash
$ npm install pm2 -g
$ pm2 -version
```

### 사용법
##### 설정 파일
```javascript
// sample.config.js
module.exports = {
    apps: [
        {
            name: 'app',
            script: './app.js',
            instance: 1,
            exec_mode: 'fork'
        },
        {
            name: 'sample',
            script: './server.js',
            instance: 2,
            exec_mode: 'cluster_mode',
            env: {
                'PORT': 8080
            }
        }
    ]
}
```

##### 실행
```bash
$ pm2 start
$ pm2 start --watch                         # 소스 변경 자동 반영
$ pm2 start --watch --ignore-watch="/dir"   # 특정 디렉토리 제외
$ pm2 start server.js -i 0                  # cluster mode로 실행
$ pm2 start server.js -i max                # cluster mode로 실행
```

##### 모니터링
```bash
$ pm2 monit
```
##### 상태 확인
```bash
$ pm2 status
# or
$ pm2 ls
```

##### 중지
```bash
$ pm2 stop
$ pm2 stop all
```