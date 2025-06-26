---
aliases: 
tags: 
namespaced: true
---
# About

Service Account는 사용자가 아닌, System의 접근을 위한 계정이다. 이는 namespaced 하며 별도로 명시하지 않으면 default의 ServiceAccount 이름으로 자동주입된다. 

그리고, 이때 주입된 token key는 secret 에 생성되며 자동으로 volume mount되어 생성된다. 
##

# 

``` yml
apiVersion: v1
kind: Pod
metadata:
  name: Test
spec:
  containers:
  - name:
    image:
  imagePullSecrets:
  - name: 

```



![[]]

