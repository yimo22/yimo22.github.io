---
aliases: 
tags:
---
```
/var/lib/docker
- aufs
- containers
- image
- volumes
  +-- volume#1
  \-- vo
```

# Volumes


![[Docker_LayeredArchitecture]]

- Docker 는 [[레이어 기반 아키텍처]]기반이기에, Image Layers 에 있는 것들은 Read-only 로 파일이 생성됨
	- Container 실행환경에서 이 파일(Read-only file)에 Write를 할경우, Container-layer 에 이 파일을 복사하여 그 파일에 Write를 실행한다. 
	- 이를 COPY-ON-WRITE 매커니즘이라고 부른다. 
- Volume Mounting 에는 아래의 2가지가 있다.
	- Volume Mounting (왼쪽)
	  Docker Volume 에 마운팅
	- Bind Mounting (오른쪽)
	  Host의 디스크에 마운팅

- Volume 은 VolumeDrivers 에 의해 관리된다. 

![[]]

