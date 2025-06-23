---
aliases: 
tags:
---
# Intro 

k8s에서의 많은 노드들에서, Name 으로 접근하기 위해서는 DNS가 반드시 필요하다. 

각 `Pod` 에서 다른 `Pod` 로 접근하기 위해서, k8s는 `Service` 오브젝트를 만들면 DNS에 이를 등록한다. 그 결과, 다른 pod 에서 Name으로 pod를 호출할 수 있게 된다. 

이는 kube DNS 에서 hostname, namespace, Type, Root, IP Address 등의 정보들을 관리하고 있기 때문이다.

## DNS에서의 Pod

DNS의 Pod 는 Hostname이 다르게 적용된다. 각 Pod들의 IP 주소 중 dot (.) 이 dash 로 들어간다. 

e.g.) 10.244.2.5 의 pods는 DNS Table에 아래와 같이 들어간다. 


| Hostname   | Namespace | Type | Root          | IP Address |
| ---------- | --------- | ---- | ------------- | ---------- |
| 10-244-2-5 | default   | pod  | cluster.local | 10.244.2.5 |

# Core DNS
일반적으로 DNS를 등록하기 위해서 사용자는 다음과 같은 과정이 필요하다. 

1. `/etc/hosts` 파일에 IP 등록
2. `/etc/resolv.conf` 파일에 DNS 서버 등록
 
이런 불편한 과정들을 k8s에서는 DNS를 통해서 해결할 수 있다. **다만, IP 매핑은 자동으로 해주지 않는다. (Service Object만 지원)**


k8s에서는 v1.2 이후로 CoreDNS 를 사용한다. 
## Config 
`cat /etc/coredns/Corefile` 에서 CoreDNS 설정을 할 수 있다. 

`kubernetes` section 에서는 cluster의 TOP level 도메인을 설정할수 있다. 

`pods` 옵션을 통해서 pod들의 ip주소를 dash로 치환처리할 수 있다. (default 아님, 설정필요)
## Pods에서 hosts 파일의 처리

공통 호스트파일은 configmap 을 통해서 관리된다. 

`kubectl get configmap -n kube-system | grep coredns`
## Pods 에서 DNS으로의 처리

CoreDNS를 적용하면, Cluster의 모든 node들에서 접근이 가능하도록 하기위해 Service 를 자동생성한다. 

이는 아래의 명령어로 확인 가능하다. 
`kubectl get svc -n kube-system | grep kube-dns`

또한 각 Pods들에서의 DNS설정은 k8s에서 자동으로 처리한다. (kubelet 이 자동으로 처리한다.)

![[]]

