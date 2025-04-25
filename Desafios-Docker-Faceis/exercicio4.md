## EXERCICIO 4 - Criando um Dockerfile para uma aplicação simples em Python

Utilizando o projeto Docker Flask para retornar uma mensagem ao acessar o endpoint.

### 1- Crie um DockerFile

```dockerfile
FROM python:alpine

WORKDIR /app
COPY requirements.txt /app/ 
RUN pip3 install -r requirements.txt

COPY . /app/

CMD [ "python3", "app.py" ]

EXPOSE 8000
```

### 2- Criando/rodando a imagem

```bash
docker build -t flask:1.0v .
docker run -dp 8000:8000 flask:1.0v
```

### 3-Testando

```bash
curl localhost:8000
```

Mensagem esperada:
```
Hello world!
```
