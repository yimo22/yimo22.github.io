---
aliases: 
tags:
---
# 개요
Storage 에 대해서 자동으로 Provisioning 지원.

- SC(Storage Class) 도 결국, 3-party 로부터 Storage를 만들어 이를 자동으로 PV로 만들어준다.
- [[Persistent Volume Claim]] 에서 SC를 명시하여 사용가능
##

# 코드
``` yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
reclaimPolicy: Retain
allowVolumeExpansion: true
mountOptions:
  - debug
volumeBindingMode: Immediate
```


[ref](https://kubernetes.io/ko/docs/concepts/storage/storage-classes/)




![[]]

