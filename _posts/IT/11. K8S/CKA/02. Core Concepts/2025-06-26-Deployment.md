---
aliases: 
tags: 
namespaced: true
---
# About

**Deployment** 는 ReplicaSet 의 상위 오브젝트이다. 따라서 이를 생성하면 대응하는 Replicaset도 같이 생성된다. 

즉, ***Deployment*** 여러개의 레플리카셋을 관리하기 위한 상위 오브젝트 이다. 

## 역할

- 애플리케이션의 업데이트와 배포를 더욱 편하게 하기 위해
	- ReplicaSet의 변경사항을 저장하는 리비전(Revision)을 남겨 롤백을 가능하게 해준다.
	- 무중단 서비스를 위해 파드의 롤링 업데이트의 전략을 지정할 수 있다. 


## Processing

1. 사용자가 `Deployment` yml 작성 및 create
2. YAML 파일 파싱 및 리소스 확인
3. Kubernetes API 서버에 요청 전송
4. API 서버가 요청 수신 및 검증
5. ETCD 에 리소스 저장
6. Controller Manager가 감지
   - `DeploymentController` 가 새로운 Deployment 객체가 생선된 것을 감지하여 ReplicaSet 생성 
1. Scheduler가 Pod 배치
   - `kube-scheduler` 가 이들을 감지하고, 리소스가 충분한 노드를 선택하여 배치 
8. Kubelet이 노드에서 컨테이너 실행 
   - 선택된 노드의 Kubelet은 자신에게 배정된 Pod정보를 API 서버에서 가져옴
9. Pod Ready 상태 감지 및 Update
   - Pod가 성공적으로 실행되면, Readiness Probe나 Liveness Probe를 통해 상태를 확인 
   - API 서버에 Pod 상태가 Running 및 Ready 상태로 갱신 

## 사용

``` bash
# 파드의 정보가 변경되어 업데이트가 발생했을 때, 이전의 정보를 리비전으로서 보존
kubectl apply -f deploy-nginx.yaml --record 


# 업데이트 및 롤링 배포
## 특정 revision으로 롤백
kubectl rollout undo deploy nginx --to-revision=1
## 롤링상태 확인 
kubectl rollout status deployment/app
## 업데이트 중지
kubectl rollout pause deployment/app
## 업데이트 재개
kubectl rollout resume deployment/app
## 히스토리 확인
kubectl rollout history deployment/app
## 이전배포로 롤백
kubectl rollout undo deployment/app

# 스케일링 및 리소스 제어
kubectl scale deployment/app --replicas=5
## HPA 설정
kubectl autoscale deployment/app --min=2 --max=10 --cpu-percentage=80

# 실행중인 배포의 이미지 업데이트
kubectl set image deployment/app nginx=nginx:1.21
# 환경변수 설정 또는 변경
kubectl set env deployment/app ENV_VAR=value


```

![[]]

