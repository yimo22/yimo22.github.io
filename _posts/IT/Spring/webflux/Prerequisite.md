---
aliases: 
tags:
---
# About 


## 필요성

Webflux는 논블로킹으로 동작하는 웹 스택의 필요성 때문에 등장하게 되었다. 기존 Spring MVC의 Servlet API 는 v3.1 부터 논블로킹을위한 API를 제공했었다. 

하지만, 이외의 동기적으로 처리하는 모듈 (Filter, Servlet) 과 블로킹 방식의 API (getParameter, getPart) 들이 있기에 환벽한 논블로킹 환경의 개발을 할 수 없었으며, Netty와의 연동을 위한 새로운 API가 필요하게 되었다. 

> 2017년 8월에 릴리즈되어 Spring 5 (Spring boot 2.x) 에 새롭게 추가된 Webflux가 생긴이유.
> 
> 1. 적은양의 스레드와 최소한의 HW 자원으로 동시성을 핸들링하기 위해. 
> 2. 함수형 프로그래밍 (Non-blocking 애플리케이션 API의 토대)

### 도입 고려사항 

> 1. MSA  환경에서, 하나의 요청을 처리하기 위해 수십여개의 외부 시스템에 대한 요청이 필요한 시스템에서 어떻게 가장 빠른 응답을 줄 수 있을까?
> 
> 2. 수많은 요청을 처리해야할 때, 어떻게 쓰레드 지옥을 벗어날 수 있을까?
>
> 3. 내부 Hard한 연들이 로직의 주를 이루는 가? 
>    (Spring Guide에 따르면, 내부 hard한 연산들이 로직의 주를 이루는 경우 MVC보다 성능적인 향상을 내지 못한다고 한다.)
> 4. 리액티브 라이브러리 유무 
>    사용하는 라이브러리 들이 블로킹이라면, 전환하기 어려울 수 있다. 




## 추천 사용자 
- 비동기, non-blocking reactive 개발에 사용하는 경우
- 효율적으로 동작하는 고성능 웹어플리케이션 개발에 사용
- 서비스간 호출이 많은 MSA 아키텍처에 적합


Non-blocking 방식은 오류가 발생하기 쉽고 디버깅이 어렵기 때문에 학습이 필요하다. 그리고 non-blocking 과 blocking 코드를 같이 사용하게 되면 비동기 코드가 무의미해지고 성능적인 이점도 볼수 없기 때문에 잘 고려해서 사용해야한다.

# Spring MVC vs Webflux


![[Pasted image 20250303155807.png]]

## 공통점

- `@Controller` , Reactive 클라이언트 이다. 
	- 둘 모두Tomcat, Jetty, Undertow 와 같은 서버에서 실행할 수 있다. 

## 차이점

### Spring MVC
- 명령형 논리, JDBC, JPA를 가질수 있음

Spring MVC는 하나의 요청에 대해 하나의 스레드가 사용된다. (Thread-per-Request)
그래서 다량의 요청을 대비해 미리 스레드풀을 생성해놓으며, 각요청마다 스레드를 할당하여 처리한다.  


### Spring Webflux
- 기능적 엔드포인트, 이벤트루프, 동시성 모델을 가질수 있음.
	- Event Driven
	- Asynchronous Non-blocking I/O

Reactive Programming 은 논블로킹과 고정된 스레드 수 만으로 모든 요청을 처리함으로 Spring MVC의 문제들을 해결한다. 

서버는 한 개의 스레드로 운영하며, Default로 CPU 코어 수 개수의 스레드를 가진 워커풀을 생성하여 해당 워커 풀 내의 스레드로 모든 요청을 처리. 

논블로킹으로 동작해야하며, **Blocking Library 가 사용되어야한다면, 워커 스레드가 아닌 외부 별도의 스레드로 요청을 처리**해야한다. 이는 요청을 처리하는 Event Loop 가 절대 블로킹되지 않아야 하기 때문이다. 



[배달의민족 최전방 시스템! ‘가게노출 시스템’을 소개합니다. | 우아한형제들 기술블로그](https://techblog.woowahan.com/2667/)
![[]]

