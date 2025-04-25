
## Exercicio 9 - Imagem Docker com Nginx e Material Kit

### 1- Clonar o repositório do Material Kit

```bash
git clone https://github.com/creativetimofficial/material-kit.git
cd material-kit
```

### 2- Crie o Dockerfile

```dockerfile
FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*

COPY . /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

### 3- Construa a imagem e a execute

```bash
docker build -t template:1.0v .
docker run -dp 8080:80 template:1.0v
```
![ex9](https://github.com/user-attachments/assets/1a143697-b980-42f4-8934-3ed1aa0623c0)
