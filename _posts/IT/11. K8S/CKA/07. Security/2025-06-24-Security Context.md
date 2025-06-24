---
aliases: 
tags:
---
# Container Security
```
# MAC_ADMIN 시스템권한을 추가하여 실행
docker --cap-add MAC_ADMIN ubuntu 

# 1001 번 유저로 실행
docker run --user=1001 ubuntu sleep 3600



```
# Kubernetes Security
Container(Docker) 와 마찬가지로, k8s에서도 설정이 가능하다. 

하지만 아래의 2가지로 선택을 해야한다.
1. Container Level 
``` yml
apiVersion: v1
kind: Pod
metadata:
  name: web-prod
spec:
  # Pod Scope 
  securityContext:
    runAsUser: 1000
    capabilities:
  	  add: ["MAC_ADMIN"]
  containers: 
  - name: ubuntu
    image: ubuntu
    command: ["sleep", "3600"]
    # Container Scope 
    securityContext:
      runAsUser: 1000
      capabilities:
        add: ["MAC_ADMIN"]
```


2. Pod Level 
     - 권한을 설정시, Pod의 모든 컨테이너에 적용 

단, 둘다 설정을 할경우 Container Level 설정이 Pod Level 설정위에 Override 된다.
# 





![[]]

