# 절전
---
### 1. 노트북 화면 닫아도 절전 막기
```bash
$ sudo vi /etc/systemd/logind.conf

************** logind.conf **************
[Login]
#NAutoVTs=6
...
HandleLidSwitch=ignore
...
*****************************************

$ sudo systemctl restart systemd-logind
```