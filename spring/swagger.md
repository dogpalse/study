# Swagger

## 0. 환경
- Spring boot 2.7.11
- jdk 11.0.11
- MacOS 13.4.1(c)
- vscode 1.80.2 (Universal)

## 1. 설정

### 의존성 추가

Gradle 

```bash
implementation 'org.springdoc:springdoc-openapi-ui:1.6.6'
# or
impelementation group: 'or.springdoc', name: 'springdoc-openapi-ui', version: '1.6.6'
```

Maven

```bash
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-ui</artifactId>
    <version>1.6.6</version>
</dependency>
```

### application.properties 설정

```properties
# Swagger Setting
springdoc.packages-to-scan=com.test.demo
springdoc.default-consumes-media-type=application/json;charset=UTF-8
springdoc.default-produces-media-type=application/json;charset=UTF-8
springdoc.swagger-ui.path=/swagger-ui/index.html
springdoc.swagger-ui.tags-sorter=alpha
springdoc.swagger-ui.operations-sorter=alpha
springdoc.api-docs.groups.enabled=true
springdoc.cache.disabled=true
```

### .yaml 설정

```yaml
# Swagger Setting
springdoc:
  packages-to-scan: com.test.demo   # 적용할 패키지 정의
  default-consumes-media-type: application/json;charset=UTF-8
  default-produces-media-type: application/json;charset=UTF-8
  swagger-ui:
    path: /swagger-ui.html        # Swagger UI 경로 => localhost:8000/swagger-ui.html
    tags-sorter: alpha            # alpha: 알파벳 순 태그 정렬, method: HTTP Method 순 정렬
    operations-sorter: alpha      # alpha: 알파벳 순 태그 정렬, method: HTTP Method 순 정렬
  api-docs:
    path: /api-docs/json
    groups:
      enabled: true
  cache:
    disabled: true
```

### Config 설정

```java
@Configuration
public class OpenApiConfig {

    @Bean
    public OpenApi openApi() {
        Info info = new Info()
            .title("Swagger Demo")
            .version("v0.0.1")
            .description("Swagger 데모 테스트");

        return new OpenApi().compoentns(new Components()).info(info);
    }
}
```

## 3. 적용

### Controller

```java
@Tag(name = "Sample", description = "Sample API")
@RestController
public class Controller {

}
```