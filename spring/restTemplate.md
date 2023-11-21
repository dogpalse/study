# RestTemplate

Spring에서 제공하는 REST 방식 API호출하는 내장 클래스.  
spring 3.0 이상 지원.  
Blocking I/O 기반의 동기 방식.  

## 1. 메서드

- getForEntity() : GET 방식 요청으로 결과값을 ResponseEntity로 반환
- getForObject() : GET 방식 요청으로 결과값을 객체로 반환
- postForEntity() : POST 방식 요청으로 결과값을 ResponseEntity로 반환
- postForLocation() : POST 방식 요청으로 결과값을 헤더에 있는 URI로 반환
- postForObject() : POST 방식 요청으로 결과값을 객체로 반환
- delete() : DELETE 방식 요청
- put() : PUT 방식 요청
- exchange() : 방식을 설정하고 요청
- execute() : 요청과 응답 콜백 수정 가능


|메서드|HTTP 메서드|결과값|
|:---|:---|:---|
|getForEntity()|GET|ResponseEntity|
|getForObject()|GET|Object|
|postForEntity()|POST|ResponseEntity|
|postForObject()|POST|Object|
|postForLocation()|POST|URI|
|delete()|DELETE||
|put()|PUT||
|exchange()|Any|ResponseEntity|
|execute()|Any||

## 2. 사용법

### - 객체 생성

```java
public void restTemplate() {
    // RestTeamplte 인스턴스 생성
    RestTemplate restTemplate = new RestTemplate();

    // Header 생성
    HttpHeaders headers = new HttpHeaders();
    headers.setContentType(MediaType.APPLICATION_JSON);

    // Body 생성
    MultiValueMap<String, String> body = new LinkedMultiValueMap<>();
    body.add("username", "song");
    body.add("password", "0000");

    // HttpEntity 인스턴스 생성
    HttpEntity<?> request = new HttpEntity<>(body, headers);
}
```

### - 빈 설정

```java
@Configuration
public class RestTemplateConfig {
    @Bean
    public RestTemplate restTemplate(RestTemplateBuilder restTemplateBuilder) {
        return restTemplateBuilder
            .requestFactory(() -> new BufferClientHttpRequestFactory(new SimpleClientHttpRequestFactory()))
            .setConnectTimeout(Duction.ofMillis(5000))
            .setReadTimeout(Duration.ofMillis(5000))
            .additionalMessageConverters(new StringHttpMessageConverter(Charset.forName("UTF-8")))
            .build()
    }
}
```

### - 메서드

- getForEntity()

```java
// param이 하나일 때
ResponseEntity<String> responseEntity = restTemplate.getForEntity("http://ip:port/{id}", String.class, "id");

// param이 여러 값일 때
MultiValueMap<Stirng, String> params = new LinkedMultiValueMap<>();
params.add("name", "song");
params.add("age", "15");
ResponseEntity<String, String> response = restTemplate.getForEntity("http://localhost/{name}/{age}", String.class, params);

// 상태
responseEntity.getStatus();
// body
responseEntity.getBody();
```

- getForObject()

```java

```

- exchange()

```java

```