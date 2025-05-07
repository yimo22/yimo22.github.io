---
aliases: 
tags:
---
# About

- 클러스터 안에 미리 만들어 놓은 스토리지 공간 (e.g. NFS, AWS EBS, GCE Disk 등)
##

[Reference](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volumes)

# 코드

``` yml
apiVersion: v1
kind: PersistentVolue
metadata: 
	name: pv-voll


spec:
	accessModes:
		- ReadWriteOnce 
	capacity:
		storage: 1Gi
	hostPath: 
		path: /tmp/data
	awsElasticBlockStore:
		volumeID: <volume-ID>
		fsType: ext4
```





![[]]

