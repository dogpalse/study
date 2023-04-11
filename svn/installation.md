# SVN

## 0. 정리

### repository

Repository는 코드 원본이 저장되는 공간.

### trunk

메인 개발 소스

### branch

trunk에서 분기된 개발 소스

### 프로토콜

* file:/// : 로컬디스크 접근
* http:// : http 접근
* https:// : SSL을 통한 https 접근
* svn:// : svn 서버 프로토콜을 통한 접근
* svn+ssh://ssh : 

## 1. 설치

### Ubuntu 22.04.1 LTS

```bash
$ sudo apt-get install -y subvision
# 설치 확인
$ svn
# svn 계정 수동 생성
$ sudo adduser svn
```

## 2. repository 생성

```bash
# svn 계정 사용
$ su svn
$ mkdir /home/svn/repo
$ svnadmin create /home/svn/repo/{프로젝트명}
$ cd ~/repo/{프로젝트명}
$ ls -al
drwxrwxr-x 6 svn svn 4096  4월 10 14:25 ./
drwxr-x--- 4 svn svn 4096  4월 10 14:54 ../
drwxrwxr-x 2 svn svn 4096  4월 10 14:29 conf/
drwxrwsr-x 6 svn svn 4096  4월 10 14:25 db/
-r--r--r-- 1 svn svn    2  4월 10 14:25 format
drwxrwxr-x 2 svn svn 4096  4월 10 14:25 hooks/
drwxrwxr-x 2 svn svn 4096  4월 10 14:25 locks/
-rw-rw-r-- 1 svn svn  246  4월 10 14:25 README.txt
```

## 3. 설정

### 유저 및 권한

```bash
# repository 디렉토리로 이동
$ cd ~/repo/{프로젝트명}/conf

# 유저 설정
$ vi ./passwd
**************** passwd ******************
[users]
# harry = harryssecret
# sally = sallyssecret
#############
# 작성 형식
# 유저명 = 비번
admin = admin
admin1 = admin
tari = nmnmnm
user = user
******************************************

# 권한 설정
$ vi ./authz
**************** authz ******************
# 그룹명 설정
[groups]
adm = admin,admin1

[/]         # 디렉토리 경로
@adm = rw   # adm group read/write 권한 부여
tari = rw   # tari 유저 read/write 권한 부여
* = r       # 모든 사용자 read 권한 부여

[/test]     # test 디렉토리 경로
@adm = rw
tari = rw
* = r
******************************************
```

### 서버

```bash
cd ~/repo/{프로젝트명}/conf
vi ./svnserve.conf
##### 아래 항목 주석 제거 #####
# anon-access = read
# auth-access = write
# password-db = passwd
# authz-db = authz
```

* anon-access = read 누구나 읽기만 가능
* auth-access = write 인증된 경우 쓰기 가능
* password-db = passwd 사용자 계정 정보 db로 passwd 사용
* authz-db = authz 사용자 권한 정보 db로 authz 사용

## 4. service 등록

```bash
# svn 실행
svnserve -d -r /home/svn/repo
# svn 확인
sudo svn checkout svn://localhost/test
```

```bash
$ sudo vi /etc/init.d/svnserve
**************** svnserve ******************
#! /bin/sh
### BEGIN INIT INFO
# Provides: svnserve
# Required-Start: $local_fs $syslog $remote_fs
# Required-Stop: $local_fs $syslog $remote_fs
# Default-Start: 2 3 4 5
# Default-Stop: 0 1 6
# Short-Description: Start svnserve
### END INIT INFO

PATH=/sbin:/usr/sbin:/bin:/usr/bin
DESC="svnserve"
NAME=svnserve
DAEMON=/usr/bin/$NAME
DAEMON_ARGS="-d -r /home/svn/repo/{프로젝트명}"
PIDFILE=/var/run/$NAME.pid
SCRIPTNAME=/etc/init.d/$NAME

[ -x "$DAEMON" ] || exit 0

[ -r /etc/default/$NAME ] && . /etc/default/$NAME

. /lib/init/vars.sh
. /lib/lsb/init-functions

do_start()
{
    start-stop-daemon --start --quiet --pidfile $PIDFILE --exec $DAEMON --test > /dev/null \
        || return 1

    start-stop-daemon --start --quiet --pidfile $PIDFILE --exec $DAEMON -- $DAEMON_ARGS \
        || return 2
}

do_stop()
{
    start-stop-daemon --stop --quiet --retry=TERM/30/KILL/5 --pidfile $PIDFILE --name $NAME
    RETVAL="$?"
    [ "$RETVAL" = 2 ] && return 2
    start-stop-daemon --stop --quiet --oknodo --retry=0/30/KILL/5 --exec $DAEMON
    [ "$?" = 2 ] && return 2
    rm -f $PIDFILE
    return "$RETVAL"
}


case "$1" in
    start)
        [ "$VERBOSE" != no ] && log_daemon_msg "Starting $DESC" "$NAME"
        do_start
        case "$?" in
            0|1) [ "$VERBOSE" != no ] && log_end_msg 0 ;;
            2) [ "$VERBOSE" != no ] && log_end_msg 1 ;;
        esac
        ;;

    stop)
        [ "$VERBOSE" != no ] && log_daemon_msg "Stopping $DESC" "$NAME"
        do_stop
        case "$?" in
            0|1) [ "$VERBOSE" != no ] && log_end_msg 0 ;;
            2) [ "$VERBOSE" != no ] && log_end_msg 1 ;;
            esac
            ;;

    restart|force-reload)
        log_daemon_msg "Restarting $DESC" "$NAME"
        do_stop
        case "$?" in
        0|1)
            do_start
            case "$?" in
                0) log_end_msg 0 ;;
                1) log_end_msg 1 ;; # Old process is still running
                *) log_end_msg 1 ;; # Failed to start
            esac
            ;;
        *)
            # Failed to stop
            log_end_msg 1
            ;;
        esac
        ;;
*)
    echo "Usage: $SCRIPTNAME {start|stop|restart|force-reload}" >&2
    exit 3
    ;;
esac

exit 0
********************************************

# 실행 권한 수정
$ sudo chmod +x svnserve
```

***DAEMON_ARGS 경로를 자신의 repository 경로로 지정해 줍니다.***

## 5. 명령어

### import

처음 repository에 소스코드를 업로드(최초의 한번만 수행)

```bash
svn import ~/workspace/test svn://localhost/test
```

### export

버전 관리 파일을 제외한 파일만 다운로드

```bash
svn export svn://localhost/test
```

### checkout

repository에서 최신 버전의 소스코드를 다운로드

```bash
svn checkout svn://localhost/test

# 특정 디렉토리로 체크아웃
svn checkout svn://localhost/test ~/workspace/
```

### update

로컬에 있는 파일 최신 버전으로 다운로드

```bash
svn update
```

### add

버전 관리 대상 파일을 등록

```bash
svn add test/test.java
```

### commit

* add한 파일을 서버(repository)에 업로드  
* revision(버전) 수가 +1  
* 커밋 전에 update로 repository와 로컬의 버전을 일치

```bash
svn commit -m "comment"
```

### revert

로컬의 소스파일을 이전 상태로 변경

```bash
svn revert test/test.java
```

### diff

소스 비교

```bash
svn diff
# 특정 파일 비교
svn diff test/test.java
# revision1과 revision2 비교
svn diff -r 1:2
# 특정 revision "n"과 현재 파일 비교
svn diff -r n test/test.java
# 특정 revision "n"과 현재 소스파일 전체 비교
svn diff -r n
```