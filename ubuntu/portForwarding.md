# PortForwarding
어느 포트로 들어온 요청을 다른 포트로 전달하는 것

#### 포트포워딩 목록 조회
```bash
$ sudo iptables -t nat -L --line-numbers
Chain PREROUTING (policy ACCEPT)
```

#### 포트포워딩 등록
```bash
$ sudo iptables -t nat -A PREROUTING -p tcp --dport [외부 접속 포트] -j REDIRECT --to-port [내부 접속 포트]
```

#### 포트포워딩 제거
```bash
$ sudo iptables -t nat -D PREROUTING [번호]
```

**해당 방식은 재부팅 후엔 설정이 리셋*

#### 재부팅 후 포트포워딩 유지
iptables-persistent 패키지 설치
```bash
$ sudo apt update && sudo apt upgrade
$ sudo apt install iptables-persistent

$ sudo systemctl enabled netfilter-persistent.service
$ sudo netfilter-persistent save
```