---
aliases: 
tags:
---
# Intro 
Ingress 는 User 가 하나의 URL 로 각기 다른 Service들에 접근이 가능하도록 역할을 한다. 

또한, URL-Rewrite 나 LoadBalance 등의 기능을 수행한다. 
## 기능

- Service 에 외부 URL을 제공
- 트래픽을 로드 밸런싱
- SSL 인증서 처리
- Virtual hosting 지정

# Detail

## Ingress Controller

### GCE 
k8s 에서 유지관리 함.
### Nginx 
k8s 에서 유지관리 함.
  
- Nginx를 Ingress Controller로 사용할 경우, 별도의 ConfigMap Object를 두어 Resource를 관리해야 한다. 
  
이를 위해서는 Service Account를 설정하고, 올바른 Rule 을 설정해야 한다. 

[Official Ref - Ingress-Nginx Controller](https://kubernetes.github.io/ingress-nginx/examples/)
#### Annotations and Rewrite target
[Official Ref - Ingress Nginx Controller (Rewrite)](https://kubernetes.github.io/ingress-nginx/examples/rewrite/)


### Contour
### HAPROXY
### Traefik
### Istio


## Ingress Resources 

Ingress Controller 에 적용된 설정과 리소스 값들이다. 
e.g.) URL 에 따라서 Service 들을 나누는 RULE들을 저장
e.g.) Domain 에 따라서 Service들을 나누도록 Rule 저장



## Usage

``` bash
kubectl create ingress <ingress-name> --rule="host/path=service:port"
```


``` yml


```

--- 
[Official Ref - Ingress Examples](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-ingress-em-)
[Official Ref - Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)
