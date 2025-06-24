---
aliases: 
tags:
---
# 필요성
초기, k8s는 docker 엔진을 기본엔진으로 사용하고 있었다. 
하지만, 버전업이 되면서 rkt, cri-o 등의 container runtime engine 들을 사용할 필요성이 생겼다. 

그리하여, 컨테이너 엔진과 k8s 사이에 Interface인 CRI 를 두는 아키텍처로 발전했다.

이와 같은 맥락으로, k8s 에서는 Networking 과 Storage 관련해서 의존성을 분리하기 위해 각각 CNI, CSI 를 두어 이를 해결했다.

CSI는 K8s 에 의한 표준이 아니라, Universal Standard 이다. 
이와 관련한 자세한 Spec은 [CSI Specification](https://github.com/container-storage-interface/spec) 을 참조.



![[]]

