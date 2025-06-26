---
aliases: 
tags:
---
# About

kubeapi server로 요청이 들어오면, 우선 Authentication 을 진행한 후 process를 처리한다.

## Auth Mechanisms

### Static Password File

- CSV 파일로 User에대한 정보와 Password를 만들 수 있다. 
  구성: password / username / userid / group

이는 `Kube-apiserver` 에서 `--basic-auth-file` 을 명시하여 사용할수 있다.
또는 `-u yimo22:password` 와 같은 방법으로 유저를 명시하여 사용할 수 있다.


### Static Token File

`--token-auth-file` 을 명시하여 토큰으로도 사용할 수 있다. 이때 토큰은 무기한으로 유지되며, API서버를 다시 시작하지 않으면 토큰 목록을 변경할 수 없다. 

### Certificates

### Identity Services

# Types
## Node
## ABAC (Attribute Base Access Control)

각 유저에 대한 권한들을 각 유저들마다 정의하는 방법이다. 이런 방법을 통해서 유저들마다 고유한 권한을 수정 및 관리할 수 있다. 

하지만, 유저들이 많아질수록 관리해야하는 권한들이 많아지며 이를 수동으로 수정해야 한다는 단점이 있다. 그리고 Kube-apiserver를 재부팅 해야한다는 단점이 있다. 

## RBAC (Role Base Access Control)

공통되는 권한을 하나로 묶어, 사용자와 권한을 N:1 의 관계로 묶는 매커니즘 이다. 
### Role 

Role 은 3가지 (API그룹, 리소스, Verbs) 로 구성된다. 

`k create role ${rolename} --verb=${} --resource=${}`

``` yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
  resourceNames: ["blue", "orange"] # 특정 resource의 이름 명시 가능
```
### RoleBindings
Role 과 Account를 Binding 해주는 object이다. namespace를 명시할 수 있다. 

`k create rolebinding ${} --user=${} --role`


-> Cluster 단위의 Role/RoleBindings 도 가능

[Official Document - RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
## Webhook

외부에 권한 제어를 위임할때 사용
## AlwaysAllow

모든 요청에 대해서 허용
## AlwaysDeny

모든 요청에 대해서 차단

# Authorization Mode

Authorization 모드는 아래와 같이,  Kube-apiserver를 실행할때 설정이 가능하다. 

``` bash
/usr/local/bin/kube-apiserver \\
  --authorization-mode=Node,RBAC,WEBHOOK \\
```

이때, 실행되는 순서는 `--authorization-mode` 로 명시된 순서대로 module을 통한 인증이 진행되며 각 모듈에서 인증실패 시 다음 모듈로 인증프로세스가 넘어간다. 


# Check Access
`kubectl auth can-i create/delete deploy/nodes --as ${userName}

![[]]
