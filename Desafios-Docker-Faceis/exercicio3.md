## EXERCICIO 3 - LISTANDO E REMOVENDO CONTAINERS

### 1- Listando

```bash
docker ps
```

### 2-Removendo um container especifico  
Ápos a listagem de container recebemos seu container ID  
com essa informação em mãos basta usar o comando:

```bash
docker container rm -f {$CONTAINER_ID}
```
