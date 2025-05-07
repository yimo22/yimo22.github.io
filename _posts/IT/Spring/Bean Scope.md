---
aliases:
  - Spring
  - Bean
  - Scope
tags:
  - Spring
---


# Scope
```
@Scope(value = ConfigurableBeanFactory.SCOPE.PROTOTYPE)
```

Spring 에서 생성되는 Bean은 전부 Singletone 이다.
하지만,  @Scope로 특별히 설정하면 Bean을 요청할 때마다 새로운 빈을 생성한다.

## 종류

1. 싱글톤
   Spring IoC 컨테이너 당 1개의 Obj 인스턴스만 존재할 수 있다.
2. 프로토타입
   Spring IoC 컨테이너 에 여러개 Bean 이 존재할 수 있음.
3. Request
   하나의 Http 요청에만 하나의 obj
4. Session
   하나의 세션에만 하나의 Obj가 존재
5. Application
6. WebSocket

### Java Singleton 과 Spring Singleton 의 차이
Java Singleton 이란, 디자인 패턴 중의 하나이다.
Spring Singleton의 경우, Spring IoC Container당 하나의 object 인스턴스가 존재한다.

**하나의 JVM에 하나의 Spring을 돌릴경우 같은 의미지만, 하나의 JVM에 여러개 Spring을 돌릴경우 그 의미가 좀 달라진다.**


| 구분           | Prototype                                               | Singleton                                               |
| ------------ | ------------------------------------------------------- | ------------------------------------------------------- |
| Instance     | IOC 컨테이너 당 여러개 존재 가능                                    | IOC컨테이너 당 1개                                            |
| Beans        | 요청시마다 새로 생성                                             | 같은 Bean이 재사용됨                                           |
| Default      | no default                                              | default                                                 |
| Code Snippet | @Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE) | @Scope(value = ConfigurableBeanFactory.SCOPE_SINGLETON) |
| Usage        | 드물게 사용                                                  | 주로 사용                                                   |
|              | Stateful 한 경우 (사용자의 개인정보등) 에 사용                         | Stateless 한 경우에 사용                                      |


# PostConstruct vs PreDestory


##

###

# 
##
###





![[0. Index]]

