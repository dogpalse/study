# Yarn
---
#### Yarn
yarn은 npm과 같이 Node.js.의 패키지 관리자이다.  
자바스크립트 패키지를 설치 및 삭제, 버전 관리, 의존성 관리를 할 수 있다.

#### npm과의 차이
npm의 보안과 성능의 문제를 해결하기 위해 facebook에서 개발되었다.
npm은 패키지 설치 시 순서대로 설치하지만  
yarn은 병렬로 패키지를 설치하여 속도가 npm보다 빠르다.
yarn은 패키지 설치 시 캐싱을 이용하여 두 번재 설치 시 훨씬 빠르게 설치할 수 있다.
```bash
$ yarn cashed dir
/Library/Cashes/Yarn/v6
```

보안상으로 yarn은 yarn.lock 또는 pakcage.json 파일에 있는 패키지만 설치하므로 보안상으로 더 강화되었다.

#### Yarn 작동 원리
프로젝트의 메타 정보는 package.json에서 관리된다.
package.json에 프로젝트의 의존 패키지의 이름과 버전이 명시된다.
```bash
## package.json에 입력된 패키지 다운로드
$ yarn
# or
$ yarn install
```
yarn install을 입력하면 package.json에 입력되어 있는 모든 패키지를 yarn registry에서 다운받아 node_modules에 저장된다.
package.json에 있는 패키지뿐만 아니라 해당 패키지가 의존하는 다른 패키지들도 같이 다운로드된다.

yarn으로 패키지를 설치하면 yarn.lock이라는 패키지 잠금 파일도 생성된다.
해당 파일은 프로젝트에 패키지를 최로로 다운로드할 때 패키지의 버전이 기록된 파일이다.
yarn.lock이 있으면 yarn registry에 최신 버전이 아닌 기록되어 있는 버전으로 설치하여 동일한 버전의 패키지로 관리할 수 있다.

#### 설치 및 실행
##### - 설치
```bash
# mac
$ brew install yarn
# windows, linux
$ npm install -g yarn

$ which yarn
/usr/local/bin/yarn
```
##### - yarn 설정
package.json 파일이 생성된다.
```bash
$ yarn init
```

##### - 패키지 설치
package.json에 있는 패키지를 설치한다.
```bash
$ yarn
# or
$ yarn install
# 모든 패키지를 상제로 다시 설치
$ yarn install --force
```

##### - 패키지 추가
해당 명령어는 package.json과 yarn.lock에 추가된다
```bash
# 최신버전 추가
$ yarn add [패키지명]
# 특정 버전 추가
$ yarn add [패키지명]@[버전]
# 개발 모드에만 추가
$ yarn add [패키지명] --dev
```

##### - 패키지 제거
package.json과 yarn.lock에서 제거된다.
```bash
$ yarn remove [패키지명]
```

##### - 패키지 유효성 체크
의존 패키지들이 유효한지 체크한다.
```bash
$ yarn check
```
error나 warning이 발생하면 해당 패키지의 버전을 조정해야 한다.

