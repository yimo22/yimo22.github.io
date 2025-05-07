---
aliases:
  - java
  - java8
tags:
  - java
---
# java8
## Lambda
[[Lambda|람다]]는 익명함수를 가지는 함수를 뜻한다.
이로 인해 짧아진 코드로 간결성을 높일 수 있고, 멀티쓰레드, 지연처리 등에 활용할 수 있다.

```
@FunctionalInterface // '구현해야 할 추상 메소드가 하나만 정의된 인터페이스'
public interface Test{
	public int add(int first, int two);
}
```
### java.util.function 인터페이스

1. `IntFunction<R>`
2. `BinaryOperator<T>`
---- 
## Stream

Stream 이란 다양한 데이터를 표준화된 방법으로 다루기 위한 라이브러리이다.
컬렉션의 요소를 하나씩 참조해서 람다식으로 처리할 수 있는 반복자 이다.
### 구성
1. `stream()`
   스트림생성
2. `filter()`
   중간연산 (스트림 변환, 연속수행 가능) 
3. `count`
   최종연산 (스트림 사용)
### 특징
- Stream은 데이터를 변경하지 않는다.
- Stream은 1회용 이다.
- Stream은 [[지연연산]]을 수행한다.
- Stream은 [[병렬성|병렬처리]]가 가능하다
  내부 반복자를 사용하므로 병렬 처리가 쉽다.
  Java는 ForkJoinPool 프레임워크를 이용해서 병렬처리를 한다.

----
## Interface default method

### history
``` java
interface TestInterface{
	public void sayHello();
}

class A implements TestInterface {
	@Overload
	...
}

class B implements TestInterface {
	@Overload
	...
}
```

위와 같은 상황에서, `TestInterface` 에서 method가 하나 추가된다면?
이를 구현하고 있던 모든 class 들은 추가된 method를 반드시 구현해야 한다.
이 문제는 class의 갯수가 많아질수록 심각해진다.

### 추상메서드와의 차이

- 매서드 앞에 `default` 예약어를 붙인다.
- 구현부 `{}` 가 있어야 한다.

### 장단점
장점
- 인터페이스에 `default method` 를 사용하면 추가 변경을 막을 수 있다.
  이로써 OCP(Open-Closed-Principle) 를 준수하는 코드를 설계할 수 있다.

단점
- 여러 인터페이스의 디폴트 메서드 간의 충돌 이 발생할 수 있다.
- 디폴트 메서드와 상위 클래스의 메서드 간의 충돌이 발생할 수 있다.
  
위와 같은 단점들은 default method를 오버라이딩 하면서 충돌 상황을 해결할 수 있다.

---- 
## Optional
`Optional<T>` 을 사용하면서 NPE를 방지할 수 있도록 하는 Wrapper 클래스이다. 

그 값이 NULL 일 경우에는 `Optional.empty` 의 값을 갖게 된다.

----

## new Date and Time API

### history

기존에는 `Date`, `Calendar`, `SimpleDateFormatter` 등을 주로 사용했다. 이는 여러 문제점을 갖고 있다.
- 변경이 가능
  Date와 같은 기존 클래스는 mutable 하기 때문에 Thread Safe하지 않아 멀티쓰레드 환경에서 안전하게 사용하기 어렵다.
- 클래스의 이름이 명확하지 않음
  Date인데 시간까지 설정이 가능하다는 모호함을 갖고 있다.
- 월을 표현할 때 +1을 해줘야한다.
  type safe 하지 않으며, 버그발생의 여지가 있다.

## 개선
1. 기계시간 표현
   `Instant` : 시간의 표현
   `Duration` : 날짜 사이의 간격
2. 사람시간 표현
   `LocalDateTime`, `ZonedDateTime` : 시간의 표현
   `Period` : 날짜 사이의 간격 