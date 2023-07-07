# 설치

## 개발 환경

OS: macOS Ventura 13.4
python: 3.8.16
airflow: 2.6.1

## 0. python 설치

### miniconda 설치

[miniconda](https://docs.conda.io/en/latest/miniconda.html)에서 `Miniconda3 macOS Apple M1 ARM 64-bit bash` 다운로드

```bash
cd ~/Downloads
sh Miniconda3-py310_23.3.1-0-MacOSX-arm64.sh

# airflow 가상환경 생성 > 가상환경 디렉토리 ~/miniconda3/envs
conda create -n 'airflow' python=3.8
# 가상환경 목록 조회
conda env list
# airflow 가상환경 활성화
conda activate airflow
# python 버전 확인
python --version

# 가상환경 비활성화
conda deactivate airflow
# 가상환경 삭제
conda env remove -n airflow

# 가상환경 내 패키지 설치
pip3 install 패키지명
# 가상환경 내 패키지 삭제
pip3 uninstall 패키지명
# 가상환경 내 설치된 패키지 목록 조회
pip3 freeze
```

## 1. airflow 설치

### 1.1 conda로 설치

```bash
# airflow 가상환경 활성화
conda activate airflow
# airflow 홈 디렉토리 설정
# default = ~/airflow
# .bashrc나 .zshrc에 AIRFLOW_HOME 설정
# 단순히 export 한번만 할 경우
export AIRFLOW_HOME=~/dev/workspace/airflow

# airflow 설치 옵션 설정
AIRFLOW_VERSION=2.6.1
PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"

pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"

# 설치 확인
airflow version

# 자동 초기화 및 DB(sqlite) 세팅, 사용자(admin) 생성 및 로그에 비밀번호
airflow standalone

##### 수동 초기화 #####
# DB 초기화
airflow db init
# 사용자 생성
airflow users create \
--username admin \
--firstname Tester \
--lastname Test \
--role Admin \
--email test@test.com \
--password test

# 사용자 삭제
airflow users delete -u "username"

# WebServer 실행
airflow webserver --port 8080
# Scheduler 실행
airflow scheduler
```

### 1.2 docker로 설치

```bash
docker run 
```

## 2. DB 세팅

### DB 생성

```bash
psql -U postgres
# or docker postgresql
docker exec -it postgres /bin/bash

create database airflow;
create user airflow with password 'airflow';
grant all privileges on database airflow to airflow;
grant all on schema public to airflow;
```

### PostgreSQL 드라이버 설치

```bash
conda activate airflow
pip install psycopg2
```

### **psycopg2 설치 에러
Error: pg_config executable not found

Solution:

```bash
pip install psycopg2-binary
```

### 설정

```bash
vi ~/dev/workspace/airflow/airflow.cfg

************** airflow.cfg **************
[core]
executor = LocalExecutor

...

[database]
sql_alchemy_conn = postgresql+psycopg2://user:password@host/db
...
*****************************************
```

### DB 세팅

```bash
# DB 초기화
airflow db init

# DB 초기화 확인
psql -U airflow -d airflow
\dt

# 사용자 생성
airflow users create \
    --username admin \
    --firstname Song \
    --lastname Byungsang \
    --role Admin \
    --email test@test.com \
    --password passwd

# airflow 실행
airflow scheduler -D
airflow webserver --port 8080 -D
```

## 3. 설정

### example dags 제거

```bash
vi ~/dev/workspace/airflow-tutorial/airflow.cfg

************** airflow.cfg **************
...
load_example = False
...
*****************************************

airflow db init
```

### dags directory 설정

```bash
vi ~/dev/workspace/airflow-tutorial/airflow.cfg

************** airflow.cfg **************
...
bags_folder = ~/dev/workspace/airflow-tutorial/dags
...
*****************************************
```