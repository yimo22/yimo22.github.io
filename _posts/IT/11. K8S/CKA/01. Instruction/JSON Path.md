---
aliases: 
tags:
---
# About

# Usage

1. Identify the kubectl command
2. Familiarize with JSON output
3. Form the JSON PATH query
4. Use the JSON PATH query with kubectl command
   `kubectl get pods -o=jsonpath={.items[*].metadata.name  }`
   `kubectl get pods -o jsonpath-file={TEXT파일}`
   
## detail

| 문법  | 설명                               |     |     |
| --- | -------------------------------- | --- | --- |
| $   | 루트노드, JSON Path의 모든 표현식은 이것으로 시작 |     |     |
| @   | 현재노드                             |     |     |
| .   | 하위노드                             |     |     |
| ..  | 중첩된 전체 하위 요소들                    |     |     |
| []  | 배열 인덱스                           |     |     |
| *   | 모든 요소와 매칭되는 와일드카드                |     |     |
| ?   | 조건부 필터 표현식                       |     |     |

## example

### Loops

```
'
{range .itesm[*]}
{.metadata.name}{"\t"}
{.status.capacity.cpu}{"\n"}
{end}
'
```

### Custom colum

```
kubectl get nodes -o=custom-colums=<COLUMN NAME>:<JSONPATH>, <COLUMN NAME>:<JSONPATH>
```

### Sort

```
kubectl get nodes --sort-by= <JSONPATH>
```

![[]]

