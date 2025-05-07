---
aliases:
  - Spring
  - Annotation
tags:
  - Spring
---

# @Component
어떤 클래스에서도 사용할 수 있는 일반적인 어노테이션 이다.
이런 어노테이션을 **스테레오 어노테이션**이라고 한다.
이런 어노테이션을 사용할때는 최대한 구체적으로 어노테이션을 명시해서 사용해야한다.
1. 유지관리의 유용성
2. Spring AOP를 통한 편의기능 사용을 위함
## 세분화
1. @Service
   Business 로직이 들어가 있음을 의미
2. @Controller
   Controller 클래스 임을 명시.
3. @Repository
   DB로부터 data를 CRUD하는 class 임을 명시

# @Lazy 
[[지연초기화]]

# @PostConstruct & @PreDestroy
@PostConstruct : 의존성 주입이 수행된 이후 초기화를 위해 실행될 메서드를 나타냄.
@PreDestroy : 컨테이너에서 인스턴스를 삭제하는 과정을 거치고 있음을 알려주는 콜백알림. 
(주로 빈의 리소스 해제하는데 사용된다.)

# @Configuration
@Bean 으로 명시한 오브젝트들을 Bean으로 등록하기 위한 어노테이션

# @ComponentScan
Components 들을 스캔하기 위한 packages들을 명시화 하는 어노테이션. 
만약 명시된 패키지가 존재하지 않을경우, 해당 class의 패키지를 default로 스캔한다.

# @Primary
Bean의 Default 를 설정할 때 사용.
일반적인 우선순위를 부여할 때 사용

# @Qualifier
Bean의 별칭을 부여하여 특정 Bean을 주입하고자 할때 사용.


# @Scope
[[Bean Scope]]

# @Named & @Inject
[[Jakarta]]



![[0. Index]]

