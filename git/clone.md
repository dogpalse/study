# Git Clone

## Branch

- 독립적으 기능을 개발할 때
- 기능 테스트
- 버전 관리

## Clone

1. main branch 클론 > branch 체크아웃
2. branch 클론

### main clone

```bash
# 모든 branch 클론
git clone git@{host}/{project_name}.git

# 브랜치 확인
git branch -a

# branch checkout
git checkout "branch_name"
```

### branch clone

1. 모든 branch fetch > 특정 branch checkout

```bash
git clone -b "branch_name" "remote_url" 
```

2. 특정 branch만 fetch

```bash
git clone -b "branch_name" --single-branch "remote_url"
```
