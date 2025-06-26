---
aliases: 
tags:
---
kubeadm 은 온프레미스 환경, 클라우드 인프라 환경에 상관없이 일반적인 리눅스 서버라면 모두 사용할 수 있다. 
# Config

``` bash
--apiserver-advertise-address // 다른 노드가 마스터에게 접근할 수 있는 IP주소
--pod-network-cidr // 쿠버네티스에서 사용할 컨테이너의 네트워크 대역
--kubernetes-version // 특정 버전의 쿠버네티스 설치
--cri-socket // 쿠버네티스가 containerd의 컨테이너 런타임 인터페이스를 통해 컨테이너를 사용하도록 설정
```




![[]]

