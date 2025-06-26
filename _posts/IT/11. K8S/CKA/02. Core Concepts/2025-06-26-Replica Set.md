---
aliases: 
tags: 
namespaced: true
---
# About

k8s의 기본단위인 파드는 여러 개의 컨테이너를 추상화해 하나의 애플리케이션으로 동작하도록 만드는 훌륭한 컨테이너 묶음이다. 이런 파드들을 복수개 만들어 관리하는 Object가 `Replicaset` 이다. 

- 정해진 수의 동일한 파드가 항상 실행되도록 관리 
- 노드 장애 등의 이유로 파드를 사용할 수 없다면, 다른 노드에서 파드를 다시 생성

즉, **Replica Set** 의 목적은 "파드를 생성하는 것"이 아닌, "일정 개수의 파드를 유지하는 것" 이다. 
### Usage

``` yaml 
apiVersion: 
kind: ReplicaSet
metadata: 
spec:
	# ReplicaSet 정의 영역
	replicas: 
	selector: 
		matchLabels:
			key: value
	# Pod 정의 영역
	template: 
	

```


# 동작원리 

레플리카셋은 파드와 연결된 것처럼 보이지만, 사실 연결돼 있지 않다. 오히려 *느슨한 연결(loosely coupled)* 을 유지하고 있으며, 이런 느슨한 연결은 파드와 레플리카셋의 정의 중 **라벨 샐랙터**를 이용해 이뤄진다. 

# Replication Controller vs Replicaset

이전 버전의 쿠버네티스에서는 `Replication Controller` 를 활용해서 파드의 개수를 유지했었다. 하지만 이는 deprecated 되었다. 

차이점 중 하나는, 표현식 기반의 라벨 셀렉터를 사용할 수 있다는 것이다. 



![[]]

