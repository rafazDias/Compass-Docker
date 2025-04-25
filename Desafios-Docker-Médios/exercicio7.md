
## Exercicio 7 - Comunicação entre Containers com Rede Personalizada

Criando uma rede Docker personalizada para conectar containers de uma aplicação, garantindo comunicação isolada e segura entre os serviços.
### 1. Clonar o Projeto

```bash
git clone https://github.com/docker/awesome-compose.git
cd awesome-compose/react-express-mongodb
```

### 2. Configurar o docker-compose.yml

```yaml
services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    networks:
      - app-network
    depends_on:
      - backend

  backend:
    build: ./backend
    ports:
      - "3001:3001"
    environment:
      - MONGO_URI=mongodb://mongodb:27017/mydb 
    networks:
      - app-network
    depends_on:
      - mongodb

  mongodb:
    image: mongo
    ports:
      - "27017:27017"
    networks:
      - app-network

networks:
  app-network:
    driver: bridge
```

### 3- Execute os containers

```bash
docker-compose up -d --build
```

### 4- Verificando a rede

```bash
docker network inspect app-network
```
