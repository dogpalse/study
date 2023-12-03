# Mac

## 0. 세팅

 - 

## 1. Homebrew 설치

## 2. iterm2 설치

## 3. oh-my-szh 설치

## 4. iterm2 세팅

## 5. vscode 설치

## 6. openjdk 설치

## 7. node 설치

### nvm 설치

```bash
brew update
brew install nvm

mkdir ~/.nvm
vi ~/.zshrc

*************** ~/.zshrc ****************
export NVM_DIR="$HOME/.nvm"
[ -s "/usr/local/opt/nvm/nvm.sh" ] && . "/usr/local/opt/nvm/nvm.sh"
[ -s "/usr/local/opt/nvm/etc/bash_completion.d/nvm" ] && . "/usr/local/opt/nvm/etc/bash_completion.d/nvm"
*****************************************

source ~/.zshrc

# 설치 확인
nvm -v
```

### node 설치

```bash
# lts 최신 버전 설치
nvm isntall --lts
# node 확인
nvm ls
```

## 8. docker 설치

## 9. dbevear 설치

