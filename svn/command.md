# SVN Command

## mkdir

리파지토리 내부에 디렉토리 생성

```bash
###
### 실행한 리파지토리 경로 기준
### Ex) svnserve /svn/repos => svn://localhost/{프로젝트명}
###     svnserve /svn/repos/{프로젝트명} => svn://localhost/
###
svn mkdir svn://localhost/{프로젝트명}/trunk
```

## import

처음 repository에 소스코드를 업로드(최초의 한번만 수행)

```bash
svn import ~/dev/workspace/sample svn://localhost/{프로젝트명}
```

## export

버전 관리 파일을 제외한 파일만 다운로드

```bash
svn export svn://localhost/{프로젝트명}
```

## checkout

repository에서 최신 버전의 소스코드를 다운로드

```bash
svn checkout svn://localhost/{프로젝트명}

# 특정 디렉토리로 체크아웃
svn checkout svn://localhost/{프로젝트명} ~/workspace/
```

## update

로컬에 있는 파일 최신 버전으로 다운로드

```bash
svn update
```

## add

버전 관리 대상 파일을 등록

```bash
svn add {프로젝트명}/test.java
```

## commit

* add한 파일을 서버(repository)에 업로드  
* revision(버전) 수가 +1  
* 커밋 전에 update로 repository와 로컬의 버전을 일치

```bash
svn commit -m "comment"
```

## revert

로컬의 소스파일을 이전 상태로 변경

```bash
svn revert {프로젝트명}/test.java
```

## diff

소스 비교

```bash
svn diff
# 특정 파일 비교
svn diff {프로젝트명}/test.java
# revision1과 revision2 비교
svn diff -r 1:2
# 특정 revision "n"과 현재 파일 비교
svn diff -r n {프로젝트명}/test.java
# 특정 revision "n"과 현재 소스파일 전체 비교
svn diff -r n
```