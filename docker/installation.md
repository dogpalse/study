# Docker

## Installation

### 필수 패키지 설치

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release
```

### Official GPG Key 등록

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### Stable Repository 등록

```bash
echo \
 "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
 $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### docker 설치

```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### 설치 확인

```bash
docker --version
```

### docker 사용 권한

docker는 root 계정으로 실행되기 때문에 sudo를 사용해야 한다.

```bash
# 해당 유저를 docker 그룹에 포함
sudo usermod -aG docker {유저명}
# 도커 재실행
sudo service docker restart
# 유저 재시작
```