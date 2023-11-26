# PostgreSQL 

## 0. 환경

- docker 20.10.21
- postgreSQL 14

## 1. 설치

```bash
docker pull postgres:14.10-alpine
# or 
docker pull postgres

docker images
```

## 2. 설정

```bash
docker run -d --name postgres -e POSTGRES_PASSWORD=postgres -e TZ=Asia/Seoul -p 5432:5432 -v ~/dev/data/postgres:/var/lib/postgresql/data postgres:14.10-alpine

docker ps
```

## 3. 접속

```bash
docker exec -it postgres bash

psql -U postgres
```
