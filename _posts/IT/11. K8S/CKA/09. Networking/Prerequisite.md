---
aliases: 
tags:
---
#  Switch
##

# Routing

`route #Routing Table`


# Core DNS
[Core DNS refs](https://github.com/kubernetes/dns/blob/master/docs/specification.md)
[Core DNS k8s Plugin](https://coredns.io/plugins/kubernetes/)

# NameSpace
## About

``` bash 
ip netns # Network namespace 조회
ip link # linux 에서 Network I/F 조회,관리
ip link add ${veth1} type veth peer name ${veth1} # 두 Virtual Cable 연결
ip link set ${veth1} netns ${v1} # veth1 을 v1 namespace에 연결

ip netns exec ${network namespace name} ip link # 특정 ns 에서 명령어 실행
ip -n ${network namespace name} link # 상동

arp # ARP Table 조회

```

## Virtual Bridge

- Linux Bridge
- Open vSwitch


## Container 


# Docker Networking



# Networking Type

## 서로 결합된 컨테이너 간 통신


## Pod 와 Pod 간 통신


## Pod와 Service 간 통신


## 외부와 Service 간 통신 




![[]]

