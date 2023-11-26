# Docker Management

## 0. 디스크 확인

```bash
docker system df
```

## 컨테이너

### 컨테이너 확인

```bash
docker ps -q
```

### 컨테이너 제거

멈춰있는 컨테이너 제거

```bash
docker container prune -f
```

모든 컨테이너 제거

```bash
docker rm $(docker ps -a -q)
```

## 이미지

### 이미지 확인

```bash
docker images
```

### 이미지 제거

dangling 이미지 제거

```bash
docker image prune -f
```

dangling 이미지 & 사용하지 않는 이미지 제거

```bash
docker image prune -a -f
```

## 볼륨

### 볼륨 제거

```bash
docker volume prune -f
```
