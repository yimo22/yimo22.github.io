---
aliases: 
tags:
---
# 개요
일반 사용자가 [[Persistent Volumes]] 을 사용하기 위해 만드는 별도의 Object.

일반적으로 모든 PVC (Persistent Volume Claim) 은 PV (Persistent Volume) 과 1:1로 매칭된다. 
- 이 과정에서, k8s는 capacity, accessmodes, volume methods, storage class  등 PVC에서 명시한 것과 맞는 PV를 찾는다.
- match 된 PV가 없을경우, Pending 상태

#  
##

[ref.](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)


# 코드
``` yml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
  storageClassName: # StorageClass 명시
```

``` yml
# Pod 에서의 PVC 사용
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: mypd
  volumes:
    - name: mypd
      persistentVolumeClaim:
        claimName: myclaim



```


![[]]


