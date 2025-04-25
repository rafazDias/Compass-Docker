## Exercicio 8 - PostgreSQL + pgAdmin com Docker Compose
Criando um compose file para rodar uma aplicação com banco de dados

### 1. Clonar o Repositório

```bash
git clone https://github.com/docker/awesome-compose.git
cd awesome-compose/postgresql-pgadmin
```

### 2- Criar o compose.yml
```yaml
services:
  db:
    image: postgres:15
    restart: unless-stopped
    environment:
      POSTGRES_USER: meu_usuario
      POSTGRES_PASSWORD: minha_senha_segura
      POSTGRES_DB: meu_banco
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    networks:
      - postgres-net

  pgadmin:
    image: dpage/pgadmin4:latest
    restart: unless-stopped
    environment:
      PGADMIN_DEFAULT_EMAIL: meu_email@dominio.com
      PGADMIN_DEFAULT_PASSWORD: senha_pgadmin
    ports:
      - "8080:80"
    depends_on:
      - db
    networks:
      - postgres-net

networks:
  postgres-net:
    driver: bridge

volumes:
  postgres_data:
```
### 3- Iniciando os containers
```bash
docker-compose up -d
```
