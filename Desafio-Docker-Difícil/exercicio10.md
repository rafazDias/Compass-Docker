
## Exercício 10 - Aplicação Python Executando como Usuário Não-Root

### 1- Conteúdo do app.py

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return "Olá! Este aplicativo está rodando como um usuário não-root!\n"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

### 2- Crie o requirements.txt com o Flask dentro

```
flask
```

### 3- Conteúdo do Dockerfile

```dockerfile
FROM python:slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN groupadd -r dev && useradd -r -g dev leonardo

RUN chown -R leonardo:dev /app

USER leonardo

EXPOSE 5000

CMD ["python", "app.py"]
```

### 4- Construindo/rodando a imagem 

```bash
docker build -t nome_app:1.0v .
docker run -dp 5000:5000 nome_app:1.0v
```

### 5- Verificando usuario

```bash
docker exec nome_app:1.0v whoami
```
![ex10|1](https://github.com/user-attachments/assets/b7dc11e8-f3f7-41c6-b525-80efb6f9e728)

![ex10](https://github.com/user-attachments/assets/69ac48ff-534a-49e9-b38c-b4d468c091aa)
