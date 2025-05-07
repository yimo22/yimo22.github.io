---
aliases: 
tags:
---
# 
0. Node Scheduling Diable처리
   `kubectl drain --ignore-daemonsets `
1. Open apt repository
   `vim /etc/apt/sources.list.d/kubernetes.list`
2. Update the version in the URL 
3. update
  ```
  kubectl drain controlplane --ignore-daemonsets
  apt update
  apt-cache madison kubeadm
  ```
4. Run the command to upgrade k8s
  ```
  apt-get install kubeadm=1.32.0-1.1
  ```
5. 
6. 



![[]]

