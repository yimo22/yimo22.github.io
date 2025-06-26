---
layout: post
title: "API Gateway"
description: "An example post which shows code rendering."
date: 2025-06-26 00:00:00 +0900
categories: Uncategorized
aliases: []
tags: []
---

Ingress 는 다음의 한계를 갖고 있다. 
 - 다양한 프로토콜 지원X
 - 멀티 테넌트 환경에서 Role을 정확히 나누기 어렵다. 

이를 위해 k8s에서 진행하고 있는 새로운 Project가 api gateway 다. 

# Intro 

## About
Gateway API 는 k8s에서 네트워크 트래픽을 관리하는 차세대 API 표준으로, 기존 Ingress API의 한계를 보완하며 더 유연하고 확장 가능한 트래픽 라우팅을 제공하는 API 이다. 

- API Gateway는 클라이언트 요청을 받아 적절한 서비스로 전달하는 역할을 하는 프록시이다. 
- 인증, 인가, 로깅, 속도제한(rate limiting), TLS 종료, 요청/응답 변환등의 기능을 수행 
- [[Ingress]] 와 비슷해 보이지만, API Gateway는 좀 더 복잡한 기능과 정책 제어에 초점이 맞춰져 있다. 

## Compare to Ingress

| 비교 항목     | Ingress       | Gateway API                                        |
| --------- | ------------- | -------------------------------------------------- |
| 트래픽타입     | HTTP/HTTPS 전용 | HTTP, TCP, UDP, gRPC 지원                            |
| 로드밸런싱 제어  | 제한적 (L7 기반)   | L4, L7 모두 지원                                       |
| 서비스 메시 통합 | 어렵다           | Istio, Linkerd 등과 쉽게 통합                            |
| 구조적 분리    | 단일 리소스        | 여러 개의 리소스로 분리                                      |
| 확장성       | Annotation 기반 | CRD (Custom Resource Definition) 기반 <br>(확장성 good) |
- Ingress API 는 Http/Https 기반의 간단한 L7 트래픽 라우팅만 가능하다 
- Gateway API 는 L4, L7 모두 지원하며 TCP, UDP, HTTP, gRPC 등 다양한 프로토콜을 처리 가능하다
- 멀티 리스너 (Multiple Listeners) 를 지원하여, 하나의 Gateway에서 여러 개의 프로토콜/포트를 동시에 운영 가능하다 

## Pros 

- L4 + L7 지원
  HTTP 뿐만 아니라 TCP, UDP, gRPC 까지 지원
- 멀티 리스너 지원
  하나의 G/W에서 여러 포트/프로토콜 운영 가능
- 서비스 매시 연동
  Istio, Linkerd 등과 네이티브 통합 가능
- 멀티 네임스페이스 지원
  ReferenceGrant를 통해 다중 네임스페이스 리소스 접근 가능
- 뛰어난 확장성
  CRD 기반이라 벤더별 커스텀 확장 가능

# 구성

다음의 3가지로 구성된다. 

## GatewayClass

클러스터에서 사용할 Gateway유형을 정의하는 리소스이다.
즉, GatewayClass는 실제 Gateway 를 생성하는 템플릿 역할을 한다. 

``` yml
apiVersion: gateway.networking.k8s.io/v1beta1
kind: GatewayClass
metadata:
  name: my-gateway-class
spec:
  # 사용하려는 Gateway 컨트롤러 (Nginx, Istio, Contour 등) 지정
  controllerName: example.com/gateway-controller 

```

## Gateway 

실제 트래픽을 수신하는 API 리소스

``` yml
apiVersion: gateway.networking.k8s.io/v1beta1
kind: Gateway
metadata:
  name: my-gateway
spec:
  # 사용할 GatewayClass 지정
  gatewayClassName: my-gateway-class
  # Gateway가 수신할 포트와 프로토콜 설정
  listeners:
  - protocol: HTTP
    port: 80
    name: http

```

## HttpRoute

트래픽을 트정 서비스로 라우팅한다. 

이외에도 다음과 같은 Route들을 설정할 수 있다. 
- `TCPRoute`
- `UDPRoute`

``` yml
apiVersion: gateway.networking.k8s.io/v1beta1
kind: HTTPRoute
metadata:
  name: my-route
spec:
  parentRefs: # 이 Route가 어느 Gateway에 연결되는지 명시
  - name: my-gateway
  rules:
  - matches:
    - path: # /app 으로 들어오는 요청을 my-service:8080 으로 전달
        type: Prefix
        value: /app
    backendRefs:
    - name: my-service
      port: 8080

```
