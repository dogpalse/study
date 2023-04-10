# User

## 1. 생성

### adduser

- home 디렉토리 자동 생성
- 계정 생성 중 비밀번호 설정
- bash 설정

```bash
sudo adduser "유저명"
# 계정 확인
cat /etc/passwd
```

## 2. 접속

```bash
su "유저명"
```

## 3. sudo 권한 부여

sudo 그룹에 해당 유저를 추가

```bash
sudo usermod -aG sudo "유저명"
```

***리부팅 후 적용***

## 4. 삭제

```bash
sudo deluser "유저명"
```
