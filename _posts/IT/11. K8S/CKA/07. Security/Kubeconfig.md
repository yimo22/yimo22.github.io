---
aliases:
  - kubeconfig
tags:
---
# Sections

### Cluster

## Contexts

## Users

# format
``` yml
apiVersion: v1
kind: Config

# 처음 시작할때의 default context를 설정
current-context: dev-user@google

clusters: 
- name: CLT_1
  cluster:
    certificate-authority: ca.crt # 절대경로 추천
    certificate-authority-data: ${base64인코딩된 CERT파일}
  server: https://server:8080

# Clusters 와 Users 사이를 연결
contexts: 
- name: dev-user@google
  context:
    cluster: CLT_1
    user: CLT_admin
    namespace: test # namespace 구분도 가능!

users: 
- name: CLT_admin
  user:
    client-certificate: admin.crt
    client-key: admin.key



```

- `k config use-context ${}`
  config파일에도 반영이 된다.

![[]]

