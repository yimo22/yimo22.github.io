
# 목적 정하기 

1. 클러스터의 목적
	1. 교육목적
		1. Minikube
		2. Single node Cluster With kubeadm / GCP / AWS
	2. 개발/테스팅
		1. Multi-node cluster with a single Master
		2. Kubeadm 을 이용한 빠른 프로비저닝
		   (GCP / AWS / AKS)
	3. 프러덕션
		- Multi node / multi master nodes 환경이 필요
		  
		kubeadm / GCP / Kops / aws 의 플랫폼 이용하여 구축 가능
		즉, 비즈니스 요구사항에 맞춰 node 들의 설계가 필요함. 
	 
2. 관리주체 
3. CSP 에서 관리할지, Host가 관리할지
4. Workloads 산정
	- Host될 Applications 의 수
	- Application 의 타입(종류)
		- WEB
		- Big Data / Analytics
	- App Resouce 요구사항
		- CPU Intesive
		- Memory Intensive
	- Traffic 요구사항
		- Heavy Traffic
		- Burst Traffic
	- Storage 요구사항 
	  High Performance  = SSD
	  Multiple Concurrent Connections = Network based storage
	- Nodes 
	  Virtual Machine or Physical Machines

---
- Turnkey Solution 
	- VM 을 이용하여 직접 Provision  
		e.g.) k8s on AWS usingn Kops
		
  OpenShift
  Cloud Foundry Container Runtime
  VMware Cloud PKS
  Vagrant

- Hosted Solutions (Managed Solutions)
  k8s As A Service
  
   GKE
   OpenShift Online
   Azure Kubernetes Service
   EKS


- Stacked ETCD Topology
- External ETCD Topology
--- 
# ETCD in HA

- Key-Value 
- Distributed

Raft Algorithm
- 다수의 client에서 write가 된경우, 완료됨으로 처리
	- Quorum = N/2 + 1
	- 정족수를 채우기 위해서, 최소 3대의 N 값이 요구됨
	- 짝수일 경우, Cluster 결함이 발생할 수 있다. 