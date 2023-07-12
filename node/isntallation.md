# Node

## 1. NVM 설치

### Ubuntu 22.04.2 LTS

```bash
###
### curl 설치
###
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/{nvm-version}/install.sh | bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash

###
### wget 설치
###
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/{nvm-version}/install.sh | bash

###
### 환경 설정
###
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

###
### 설치 확인
###
nvm -v
```

### macOS

```bash

```

## 2. Node 설치

```bash
###
### 설치된 node 조회
###
nvm ls

###
### 특정 버전 node 설치
###
nvm install "node-version"

###
### 최신 lts 설치
###
nvm install --lts

###
### 특정 버전 node 제거
###
nvm uninstall "node-version"

###
### 특정 버전 node 사용
###
nvm use "node-version" 

node -v
npm -v
```