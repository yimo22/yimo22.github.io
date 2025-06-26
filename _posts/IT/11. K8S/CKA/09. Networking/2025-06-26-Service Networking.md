---
aliases: 
tags:
---
# About

Service 오브젝트에서는 ClusterIP 로 Cluster 간에 IP로 접근 가능
하지만, Cluster의 어떤 노드에도 Service 객체는 생성되지 않음 (Virtual Object)


# Kube proxy

## About

***kube-proxy*** 는 클러스터의 각 노드에서 실행된다. 각 노드에서 실행되어 network rules 들을 유지한다. 이 Network rules 는 Cluster 안밖의 Pods 들로 Network 통신이 가능하도록 하는 규칙들이다. 

***kubeadm*** 으로 클러스터를 구성한 경우, kube-proxy 는 daemonset으로 되어있다. 

***kube-proxy*** 는 서비스들을 모니터링하거나 각 Service 의 endpoints 를 담당하고 있다. 예를들어, Client가 Virtual IP 를 통해서 Service를 연결하려는 경우 kubeproxy는 실제 파드들에 traffic을 보내는데 역할을 한다. 

## Type

kube-proxy 는 아래의 3개 모드가 있다.
- userspace
- iptables
- ipvs

## Trouble Shooting

1. Check **kube-proxy** pod in the **kube-system** namespace is running.

2. Check **kube-proxy** logs.

3. Check **configmap** is correctly defined and the config file for running **kube-proxy** binary is correct.

4. **kube-config** is defined in the **config map**.

5. check **kube-proxy** is _running_ inside the container
   `netstat -plan | grep kube-proxy`

# how works in svc

1. `kube-api-server --service-cluster-ip-range={ipNet}` 에서 명시된 사용가능한 Cluster IP 범위를 지정할 수 있다. 
2. 사용자가 `kubectl create -f ` 을 통해서 Service 오브젝트를 생성하면, kube-api server는 이를 받아 etcd 오브젝트에 저장
3. API 서버가 IP를 할당
	1. kube-apiserver 는  `--service-cluster-ip-range={ipNet}` 내에서 사용가능한 IP를 확인
	2. 할당되지 않은 IP를 찾아 Service 오브젝트에 spec.clusterIP 필드로 지정
	3. spec.clusterIP: None 으로 설정하면, Headless Service가 되어 IP가 자동할당되지 않는다. 
4. Service 정보가 etcd에 저장
5. kube-proxy 가 IP를 사용하도록 설정
   kube-proxy는 etcd의 변경사항을 감지하여, 새 Service정보를 가져온다. 이때 `iptables` 또는 `IPVS` 규칙을 생성하여 해당 `ClusterIP` 로 들어오는 트래픽을 실제 `Pod` 로 라우팅한다. 

## 각 노드에서의 실행보장

Daemonset은 각 노드(Node) 에서 특정 pod를 실행하도록 보장하는 k8s 의 컨트롤러다. 

- 보통 CNI 플러그인, 로그수집기, 모니터링 에이전트 등의 시스템 레벨 서비스를 실행할때 사용
- 클러스터의 노드 수가 변하면, Daemonsets 는 자동으로 Pod를 추가하거나 제거한다. 





![[]]

