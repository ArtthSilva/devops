# Atividade final de DevOps

Este projeto demonstra a containerização de uma aplicação full stack usando Docker e Docker Compose, incluindo frontend, backend e banco de dados MongoDB.

## Arquitetura

- **Frontend**: Interface web servida pelo Nginx
- **Backend**: API Node.js/Express
- **Banco de Dados**: MongoDB
- **Network**: Rede Docker customizada para comunicação entre containers

## Estrutura do Projeto

```
devops/
├── frontend/           # Arquivo com HTML/CSS/JS
├── backend/           # API Node.js
│   ├── package.json
│   ├── index.js
│   └── Dockerfile
├── docker-compose.yml
└── README.md
```

## 🚀 Como Executar com Docker Compose (Recomendado)

### Executar toda a aplicação
```bash
docker-compose up -d
```
![executando docker compose](/evidencias/executando_compose.png)

### Parar a aplicação
```bash
docker-compose down
```

### Ver logs dos serviços
```bash
docker-compose logs
```

### Reconstruir e executar
```bash
docker-compose up --build -d
```

---

## Como Executar com Docker (Método Manual)

### 1. Criar a rede Docker

```bash
docker network create devops
```
![criando network](/evidencias/criando_network.png)
---

### 2. Executar o MongoDB

```bash
docker run -d --name mongo --network devops -p 27017:27017 mongo:latest
```
![executando mongodb](/evidencias/executando_mongodb.png)
---

### 3. Construir e executar o Backend

```bash
# Na pasta backend
docker build -t backend-image .
docker run --name backend --network devops -p 3000:3000 backend-image
```
![criando backend](/evidencias/criando_backend.png)
---

### 4. Executar o Frontend

```bash
docker run --name frontend --network devops -p 8080:80 -v "/home/arthur/Documentos/faculdade/devops/frontend:/usr/share/nginx/html" nginx:alpine
```
![executando frontend](/evidencias/executando_frontend.png)

### Testando frontend
![testando frontend](/evidencias/frontend_testando.png)
---

## 📋 Comandos Úteis

### Docker Compose
```bash
# Visualizar status dos serviços
docker-compose ps

# Parar um serviço específico
docker-compose stop frontend

# Reiniciar um serviço específico
docker-compose restart backend

# Remover containers e volumes
docker-compose down -v
```

### Docker Tradicional
```bash
# Verificar redes Docker
docker network ls

# Verificar containers em execução
docker ps

# Parar e remover containers
docker stop frontend backend mongo
docker rm frontend backend mongo

# Remover rede
docker network rm devops
```

## Acesso à aplicação frontend

- http://localhost:8080


## Observações

- Todos os containers estão na mesma rede Docker (`devops`) para comunicação interna
- O frontend é servido através de um volume montado no Nginx
- O MongoDB roda com persistência de dados através de volumes
- As portas são mapeadas para acesso externo aos serviços
- Docker Compose gerencia automaticamente as dependências entre serviços

## 🔧 Tecnologias Utilizadas

- Docker & Docker Compose
- Nginx (Alpine)
- Node.js & Express
- MongoDB
- HTML/CSS/JavaScript
