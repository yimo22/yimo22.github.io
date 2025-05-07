---
aliases:
  - Spring
  - Actuator
tags:
  - Spring
---

# Spring Boot Actuator
Application을 Monitoring 및 관리
## Endpoints
- beans
  app의 beans 리스트를 end-point로 사용할 수 있음
- health
  app의 정상작동여부
- metrics
  app의 metrics
- mappings
    Request Mapping의 자세한 정보
## 사용법
1. pom.xml 에 라이브러리 추가
```
<dependency>  
	<groupId>org.springframework.boot</groupId>  
	<artifactId>spring-boot-starter-actuator</artifactId>  
</dependency> 
```

2. `/actuator` url 을 통해서 접근 가능
## Customize

```
# Application.xml 에 작성
management.endpoints.web.exposure.include=*   # Actuator 의 모든 endpoint 개방
management.endpoints.web.exposure.include=health,metrics #health,metrics만 개방
```


![[0. Index]]

