# Gradle

## 0. 환경

- OS: Mac
- Jdk: openjdk 11.0.11
- Editor: VSCode

## 1. gradle 설치

```bash
# homebrew로 설치할 수 있는 gradle 버전을 조회
brew search gradle
# 조회한 버전 중에 설치하고 싶은 gradle 설치
brew install gradle@7
# gradle 경로 설정
echo export PATH="/opt/homebrew/opt/gradle@7/bin:$PATH"

gradle --version
```

## 2. gradle 프로젝트

### 프로젝트 구조
- .gradle: 작업 파일 디렉토리
- gradle: gradle-wrapper 관련 디렉토리
- gradlew/gradle.bat: gradle-wrapper 실행 명령
- build.gradle: 의존성과 빌드처리 등 기본 설정 파일
- settings.gradle: 프로젝트 설정 정보 파일

#### build.gradle 작성

gradle 기본 설정 파일

```groovy
plugins {
    id 'java'
    id 'org.springframework.boot' version '2.7.10'
    id 'io.spring.dependency-management' version '1.0.15.RELEASE'
}

group = 'com.hashlab'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '11'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

taks.named('test') {
    useJUnitPlatform()
}
```

- plugins: 플러그인 설정
- sourceCompatibility: java 컴파일 버전 정의
- repositories: 필요한 라이브러리를 다운로드할 저장소 정의.
ex) mavenCentral(): 공개 저장소, maven {}: maven 저장소 

### 프로젝트 Task

task는 프로텍트 작업 단위.  

#### gradle

로컬에 설치된 gradle로 task 수행
`gradle [task]`

##### 빌드

- 프로젝트 빌드
- build.gradle에 `apply plugin: 'java'`를 추가하면 .jar로 패키징까지 수행
- build 디렉토리 생성

```bash
gradle build
```

##### 수행

- 컴파일 후 main 클래서 실행

```bash
gradle run
# 스프링부트 실행
gradle bootRun
```

##### 패키징

- .jar로 패키징
- build/lib 디렉토리에 .jar 생성

```bash
gradle jar
```

##### 클린

- build 디렉토리 제거

```bash
gradle clean
```

#### gradle-wrapper

다른 환경에서 gradle을 설치 없이 task 수행

```bash
# 리눅스 & 맥
./graldew [task]

# 윈도우
gradlew [task]
```