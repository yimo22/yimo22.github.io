---
aliases:
  - Spring
  - Jpa
tags:
  - DB
---
# JPA

JPA(Java Persistence API) 의 약자로, Java 진영의 ORM 기술 표준이다.
Hibernate, EclipseLink 등 다양한 구현체가 존재한다.
- Eclipse Link
- Toplink


JPA는 spec에 대한 정의를 내리는 interface 이다.
- 어떻게 entity를 정의하고 mapping을 하는가?
- entity를 어떻게 관리하는가?


## 등장배경
관계형 데이터베이스와 Java 라는 언어가 가지는 객체 지향성의 패러다임 불일치 

이 때문에 JDBC를 사용한 개발은 상당히 비효율적이라는 단점을 갖게 된다. 이 비효율성을 해결하고 객체지향적으로 개발에 집중할 수 있도록 해주는 것이 JPA 이다.
## 특징
- 생산성, 유지보수 등 다양한 면에서 뛰어나다.
  쿼리문을 직접 작성하지 않아도 되기 때문.
- RDB와 객체지향성의 패러다임 불일치 해소
- 복잡한 쿼리문을 작성하기에는 적합하지 않고, 높은 러닝커브를 가진다.

# Spring Data JPA
JPA의 구현체를 좀더 쉽게 사용할 수 있도록 Spring에서 제공하는 JPA 모듈이다. 
(JPA에서 사용하는 EntityManager 를 작성할 필요가 없어진다.)






![[]]

