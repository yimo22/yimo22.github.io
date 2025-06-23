---
aliases:
  - Spring
  - JDBC
tags:
  - DB
---
# JDBC 
JDBC(Java Database Connectivity) 는 자바에서 관계형 데이터베이스에 접속할 수 있는 API (인터페이스)를 뜻한다. 

## 배경 및 장단점

JDBC 이전에는 DB 종류에 따라 다른 SQL문을 사용해야 했다. 그러나 JDBC의 등장으로 DB마다 다른 SQL문을 통일하는 문법을 만들어 사용할 수 있도록 되었다. 


그러나 JDBC의 등장으로, 다음과 같은 번거로움을 겪게 된다.
1. 코드가 길어진다.
2. 쿼리문을 직접 작성해야 한다.
3. 예외 처리를 위한 복잡한 Try-Catch 문을 사용해야 한다.


# Spring JDBC 
스프링에서 JDBC 프로그래밍을 위해 제공하는 Spring API 이다.
자원을 내부적으로 생성하고 해제해주어 기존 JDBC보다 빠르고 편리하게 사용할 수 있다. 

## 특징
- 설정이 기존 JDBC와 동일
- JDBC API 상에서 반복되는 코드를 줄여줌
- 여전히 쿼리문을 직접 작성해야 한다.


## JDBC 와의 차이점
Spring JDBC는 Spring Framework에서 제공하는 JDBC 모듈이다. 

Spring JDBC는 JDBC 코드를 좀더 간결하게 작성하고 더 쉽게 DB에 연결, 사용하도록 돕는다.

## 특징

### DataSource 
Spring JDBC는 DB 연결 풀을 관리하기 위한 DataSource 인터페이스를 제공한다.

DataSource를 사용하여 DB 연결 및 트랜잭션 관리를 편리하게 처리할 수 있다.

### 예외처리 및 자원관리
Spring JDBC는 JDBC 작업에서 발생하는 예외를 일관되게 처리하고, 연결 및 리소스 관리를 자동으로 처리하여 개발자가 명시적으로 관리해야 하는 부분을 간소화

### SQL문 실행 및 매핑
간단하고 직관적인 방식으로 SQL문을 실행하고 결과를 자바 객체로 매핑하는 기능을 제공.

- ResultSet을 자동으로 객체로 변환하고, PreparedStatement 및 CallableStatement를 사용하여 SQL 파라미터를 설정할 수 있다.

### 트랜잭션 관리
Spring JDBC는 스프링의 트랜잭션 관리기능과 통합된다.

기존에는 Service에서 커밋과 롤백을 설정했었다면 Spring에서는 자동으로 이를 관리해준다. 이로인해 트랜잭션 경계 설정, 롤백, 커밋 등의 작업을 편리하게 처리할 수 있다.

### 다양한 Callback 및 템플릿
Spring JDBC는 다양한 템플릿과 콜백 기능을 제공한다.

1. Jdbc Template
2. NamedParameterJdbcTemplate
   JdbcTemplate 의 경우, 파라미터의 '?' 의 위치가 강제된다. 이런 방식은 가독성을 떨어뜨리게 된다.
   
   그래서 나온것이 NamedParameterJdbcTemplate 이다. 이는 '?' 대신 ':변수명' 을 이용하여 순서 문제를 해결했다.
   
   또한 객체와 매핑되어 SQL문 작성에 편리하다는 장점을 갖고 있다.
3. ~~SimpleJdbcTemplate~~
   `JdbcTemplate` 과 `NamedParameterJdbcTemplate` 를 합쳐놓은 템플릿 클래스 이다.
   하지만, 이는 deprecated 되었다.
   [SimpleJdbcTemplate 공식 문서](https://docs.spring.io/spring-framework/docs/4.1.5.RELEASE/javadoc-api/index.html?org/springframework/jdbc/core/simple/SimpleJdbcTemplate.html)


이를 통해 반복적인 JDBC 코드 작성을 간소화하고, 일관성있는 방식으로 DB 엑세스 작업을 수행할 수 있다.

## 사용법
1. pom.xml 에 라이브러리 추가

``` xml
    <dependency>  
        <groupId>org.springframework.boot</groupId>  
        <artifactId>spring-boot-starter-data-jdbc</artifactId>  
    </dependency>
```
2. `org.springframework.jdbc.core.JdbcTemplate.JdbcTemplate` 을 주입
3. CRUD 작성 및 사용


![[]]

