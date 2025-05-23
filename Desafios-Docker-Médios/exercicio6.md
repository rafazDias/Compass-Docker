
## EXERCÍCIO 6 – Criando um Dockerfile Multi-Stage para aplicação Go (docker-gs-ping)

Otimizar a imagem Docker da aplicação Go docker-gs-ping usando multi-stage build para reduzir drasticamente o tamanho da imagem final.

### 1-CLONANDO O REPOSITÓRIO

```bash
git clone https://github.com/docker/docker-gs-ping.git
cd docker-gs-ping
```

### 2-CRIANDO O DOCKERFILE MULTI-STAGE

```dockerfile
FROM golang:1.19-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY *.go ./

RUN CGO_ENABLED=0 GOOS=linux go build -o /docker-gs-ping

FROM gcr.io/distroless/base-debian11

WORKDIR /

COPY --from=builder /docker-gs-ping /docker-gs-ping

EXPOSE 8080

USER nonroot:nonroot

ENTRYPOINT ["/docker-gs-ping"]
```

### 3- Construindo/rodando a imagem

```bash
docker build -t go:1.0v .
docker run -dp 8080:8080 go:1.0v
```

### 4- Testando a aplicação:

```bash
docker run -dp 8080:8080 go:1.0v
```

Mensagem esperada:
```
Hello, Docker!
```
![ex6](https://github.com/user-attachments/assets/9a67e5c7-3244-49b8-93dd-de466d1ef309)
