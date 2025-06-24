---
aliases: 
tags:
---
# 필요성
Custom 한 Resource Object를 만드는데 필요한 경우

단, [[Custom Controller]] 가 없을 경우 상태변화를 감지하여 처리를 할 수 없다. 

``` yml
# Custom Resource Definition 
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: flighttickets.flights.com

spec:
  scope: Namespaced
  group: flights.com
  names:
    # kind 에 들어가는 부분
    kind: FlightTicket
    # kubectl 에서 보이는 resource Type
    singular: 
    # kubectl api-resources 에서 보이는 부분
    plural: 
    # Short cut
    shortnames: 
    - ft
      
  versions:
  - name: v1
    served: true
    storage: true
  schema:
    
    openAPIV3Schema:
      type: object
      properties:
        spec: 
          type: object
          # spec 부분에 들어갈 Custom parameter
          properties:
            from: 
              type: string
            number: 
              type: integer
              minimum: 1
              maximum: 10


-- 
# flightticket.yml
apiVersion: flights.com/v1
kind: FlightTicket
metadata:
  name: my-flight-ticket
spec:
  from: Seoul
  to: London
  number: 2

```


![[]]

