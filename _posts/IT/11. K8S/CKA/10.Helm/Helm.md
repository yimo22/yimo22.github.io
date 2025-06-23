---
aliases: 
tags:
---
# About
k8s 환경에서 반복적인 리소스 배포를 효율화하고자 할 때, 단순한 `kubectl apply` 만으로는 한계가 있어 helm으로 관리한다. 

즉, Helm 은 **k8s용 패키지 매니저**로 애플리케이션을 정의하고 설치하고 업그레이드하는 작업을 코드로 템플릿화하여 수행할 수 있도록 도와준다. Helm을 이용하면 복잡한 kubernetes 리소스 정의도 하나의 패키지(Charts) 로 관리할 수 있고 배포/업데이트/롤백 까지 일관되고 쉽게 처리할 수 있다. 

- 복잡한 YML 파일을 수동으로 관리 
  -> 템플릿화하여 재사용 가능 
- 여러 리소스를 한번에 배포
  -> Helm이 묶어서 배포
- 환경별 설정을 바꿔야 함
  -> values.yaml 로 쉽게 조정 (Value Injection)
- 설치, 업그레이드, 롤벡 필요
  -> Helm 명령으로 간단하게 가능 



# Versions

## v 1.0 (Feb, 2016~)

## v 2.0 (Nov, 2016~)

- helm 은 통신하기 위해서 Tiller 를 사용했어야 했음. 
  이로인해 Tiller 는 helm과 통신하기 위한 middle ware 로서 작동했다. 
	- (-) 모든 권한을 가지고 실행하게 된다. -> 보안문제 발생
- 다음의 2가지 지원
	- Role Based Access Control
	- Custom Resource Definitions


## v 3.0 (Nov, 2019~)

- Tiller 없이 작동
- 3-Way Strategic Merge Patch 
- Multiple Components 
	- 새로운 정보 Update에 대한 metadata 들을 Secret Object에 저장하여 처리 

# Helm Charts

- Helm 버전에 따라서 `apiVersion` 명명이 다르다. 
  v 2.0 : v1 / v3.0: v2

## Structure

``` bash
hello-world-chart
  ㄴ templates 
  ㄴ value.yaml
  ㄴ Chart.yaml
  ㄴ LICENSE
  ㄴ README.md
  ㄴ charts
```


## Ways to charts

`helm search [hub/repo] [command]`

``` bash
helm search [hub/repo] [command]

helm rollback {CHART_NAME} {REVISION_NUM}
```
## Customize Parameters in Command Line 

1. `helm install --set Key=value ~`
2. `helm install --values custome-values.yaml ~`
3. `helm pull --untar bitnami/wordpress`


# LifeCycle Management



# Docs

## https://helm.sh/docs/intro/quickstart/




![[]]

