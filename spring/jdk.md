# JDK

## 1. 설치

### Ubuntu 22.04.1

```bash
sudo apt update && sudo apt upgrade
# openjdk 11
sudo apt install openjdk-11-jdk
# openjdk 8
sudo apt install openjdk-8-jdk
# JDK 경로 설정
sudo vi ~/.bashrc
************* .bashrc *************
...

export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export PATH=$PATH:$JAVA_HOME/bin
***********************************

# bashrc 설정 반영
source ~/.bashrc

# 설치 후 버전 확인
java -version
# jdk 설치 경로 확인
which java
```

### Mac

```bash

```

## 2. 버전 변경

```bash
sudo update-alternatives --config java
```

## 3. 제거

```bash
sudo apt remove openjd*
sudo apt autoremove --purge
sudo apt autoclean
```
