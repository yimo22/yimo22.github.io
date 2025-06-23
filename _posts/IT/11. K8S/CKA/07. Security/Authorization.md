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
## ABAC

## RBAC (Role Base Access Control)
### Role 
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
```
### RoleBindings
Role 과 Account를 Binding 해주는 object

`k create rolebinding ${} --user=${} --role`


-> Cluster 단위의 Role/RoleBindings 도 가능

[Official Document - RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
## Webhook

## AlwaysAllow

## AlwaysDeny


# Check Access
`kubectl auth can-i create/delete deploy/nodes --as ${userName}

![[]]
