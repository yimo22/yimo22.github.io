---
aliases: 
tags:
---
``` yml

```
# About

- Pod 안에서 데이터를 저장하거나 공유할 공간
- Pod 가 살아있는 동안은 유지되지만, Pod가 삭제되면 사라짐

일부 애플리케이션은 추가 스토리지가 필요하지만, 재시작시에도 데이터가 영구적으로 저장되는지는 중요하지 않다. 전체 성능에 거의 영향을 주지 않으면서 자주 사용되지 않는 데이터를 메모리보다 느린 스토리지로 옮길 수 있다. 

`Volume` 은 이러한 사용 사례를 위해 설계되었다. 볼륨은 Pod의 생명주기를 따르고 Pod와 함께 생성 및 삭제되므로, 영구 볼륨을 사용할 수 있는 위치에 제한받지 않고 Pod를 중지하고 다시 시작할 수 있다. 
## Type

- emptyDir
  Pod시작시 비어있음, 저장소는 kubelet 기본 디렉토리 또는 RAM에서 로컬로 제공됨
- configMap, downwardAPI, secret
  다양한 종류의 kubernetes 데이터를 Pod에 주입
- image
  컨테이너 이미지 파일이나 artifacts 를 pod에 직접 마운트할 수 있다. 
- CSI 임시 볼륨
  Volume과 유사하지만, 특정 기능을 가진 볼륨

``` yml
volumes:
  # 설정파일 마운트
  - name: config-volume
    configMap:
	  name: app-config
	  
  # 비밀번호/토큰 마운트 
  - name: secret-volume
    secret: 
      secretName: db-secret #민감정보를 base64 인코딩하여 제공
  # Pod 정보 접근
  - name: podinfo
    downwardAPI:
      items:
        - path: "podname"
          fieldRef:
            fieldPath: metadata.name
            
  # node 로컬 경로 접근
  - name: host-logs
    hostPath: # 노드의 디렉토리를 직접 마운트
      path: /var/log
      type: Directory

```








![[]]

