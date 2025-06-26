---
aliases: 
tags:
---
# 
##

# 


``` yml
apiVersion:
metadata:
kind:

spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
  - Ingress # egress

  ingress: 
  - from: 
    # Rule 1
    - podSelector:
        matchLabels:
          name: api-pod
          
      namespaceSelector:
        matchLabels:
          name: api-pod
          
    # Ruel 2
    - ipBlock:
        cidr:
      
    ports:
	- protocol: TCP
	  port: 3306
  egress:
  - to: # ingress 와 동일

```


![[]]

