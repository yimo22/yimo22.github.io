---
aliases: 
tags:
---
``` bash
# default cni plugins
ls /opt/cni/bin 

# check CNI plugin
ls /etc/cni/net.d
```
## Weave

``` bash
curl -L https://github.com/weaveworks/weave/releases/download/latest_release/weave-daemonset-k8s-1.11.yaml | kubectl apply -f -
```






# References

https://kubernetes.io/docs/concepts/cluster-administration/addons/#networking-and-network-policy

![[]]

