---
aliases: []
tags:
---
# About

파드의 IP는 영속적이지 않아 항상 변할수 있다. 따라서 여러개의 **deploy** 를 하나의 애플리케이션으로 연동하려면 파드IP가 아닌, *서로의 발견(Discovery)* 를 할수있는 다른 방법이 필요하다.

서비스는 파드에 접근하기 위한 규칙을 정의한다. 
## 기능

- 여러개의 파드에 쉽게 접근할 수 있도록 고유한 도메인 이름을 부여
- 여러개의 파드에 접근할 때, 요청을 분산하는 로드밸런서 기능을 수행
- 클라우드 플랫폼의 로드 밸런서, 클러스터 노드의 포트등을 통해 파드를 외부로 노출

## Type

### ClusterIP 
쿠버네티스 내부에서만 파드들에 접근할 때 사용한다. 외부로 파드를 노출하지 않기 때문에 쿠버네티스 클러스터 내부에서만 사용되는 파드에 적합하다. 

``` yml
apiVersion: v1
kind: Service
metadata:
	name: hostname-svc-clusterip
spec:
	ports:
	- name: web-port
	  port: 8080
	  targetPort: 80
	selector:
	  app: webserver
	type: ClusterIP
```

### NodePort
파드에 접근할 수 있는 포트를 클러스터의 모든 노드에 동일하게 개방한다. 따라서 외부에서 파드에 접근할 수 있는 서비스 타입이다. 접근할 수 있는 포트는 랜덤으로 정해지지만, 특정 포트로 접근하도록 설정할 수도 있다. 

Nordport 는 ClusterIP의 기능을 포함하고 있다. 따라서 자동으로 내부 IP가 할당되어 Cluster에서도 접근이 가능하다.

``` bash
# API 서버 컴포넌트의 실행 옵션을 변경하여 원하는 포트 범위를 설정 가능 
# default는 30000~32768
--service-node-port-range=30000-35000
```
### LoadBalancer
클라우드 플랫폼에서 제공하는 로드밸런서를 동적으로 프로비저닝해 파드에 연결한다. `NodePort` 타입과 마찬가지로 외부에서 파드에 접근할 수 있는 서비스 타입이다. 그렇지만 일반적으로 AWS, GCP 등과 같은 클라우드 플랫폼 환경에서만 사용할 수 있다. 


![[]]

