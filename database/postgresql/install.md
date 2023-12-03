# PostgreSQL 

## 0. 환경

- docker 20.10.21
- postgreSQL 14

## 1. 설치

```bash
# 특정 버전 이미지
docker pull postgres:14.10-alpine
# 최신 버전 이미지
docker pull postgres

docker images
```

## 2. 설정

```bash
docker run -d --name postgres -e POSTGRES_PASSWORD=postgres -e TZ=Asia/Seoul -p 5432:5432 -v ~/dev/docker/data/postgres:/var/lib/postgresql/data postgres:14.10-alpine

docker ps
```

## 3. 접속

```bash
docker exec -it postgres bash

psql -U postgres
```
