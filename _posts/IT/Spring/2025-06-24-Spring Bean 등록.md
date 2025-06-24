---
aliases:
  - Spring
  - Configuration
  - Config
tags:
  - Spring
---

| 구분       | Annotaion                          | XML                               |
| -------- | ---------------------------------- | --------------------------------- |
| 사용편의성    | Good                               | Bad                               |
| POJO 간결성 | NO (POJO가 Spring Annotation으로 오염됨) | YES (POJO는 Spring Framework를 인지X) |
| 유지보수성    | YES                                | NO                                |
| 사용빈도     | 최근의 모든 Project                     | 드물게 사용                            |
| 권고사항     | 일관적으로 사용되어야함, 혼합사용 X               | 좌동                                |
| 디버깅난이도   | Hard                               | Medium                            |

# XML Configuration
1. resource 에서 xml파일을 만든다.
2. XML 파일 설정
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context" xsi:schemaLocation="
 http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd"> 
 
 <!-- bean definitions here -->
	<!-- Bean을 등록하는 방법 1. 수동등록 -->
	<bean id="" class="java.lang.String">
		<constructor-arg value="" />
	</bean>
	
	<!-- Bean을 등록하는 방법 2. Component-scan으로 패키지단위 등록 -->
	<context:component-scan
		base-package="여기에는 component-scan을 진행할 패키지명"
	/>
</beans>
```

3. Context를 변경
```
new ClassPathXmlApplicationContext("XML파일이름")   
```

##
###

##

###

# 
##
###





![[0. Index]]

