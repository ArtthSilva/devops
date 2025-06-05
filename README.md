# Atividade final de DevOps

Este projeto demonstra a containerização de uma aplicação full stack usando Docker, incluindo frontend, backend e banco de dados MongoDB.

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
└── README.md
```

## Como Executar

### 1. Criar a rede Docker

```bash
docker network create devops
```

### 2. Executar o MongoDB

```bash
docker run -d --name mongo --network devops -p 27017:27017 mongo:latest
```

### 3. Construir e executar o Backend

```bash
# Na pasta backend
docker build -t backend-image .
docker run --name backend --network devops -p 3000:3000 backend-image
```

### 4. Executar o Frontend

```bash
docker run --name frontend --network devops -p 8080:80 -v "/home/arthur/Documentos/faculdade/devops/frontend:/usr/share/nginx/html" nginx:alpine
```

## 📋 Comandos Úteis

### Verificar redes Docker
```bash
docker network ls
```

### Verificar containers em execução
```bash
docker ps
```

### Parar e remover containers
```bash
docker stop frontend backend mongo
docker rm frontend backend mongo
```

### Remover rede
```bash
docker network rm devops
```

## 🌐 Acesso à Aplicação Frontend

- http://localhost:8080




## 🐳 Dockerfile (Backend)

O backend utiliza um Dockerfile para criar a imagem personalizada com as dependências Node.js necessárias.

## Observações

- Todos os containers estão na mesma rede Docker (`devops`) para comunicação interna
- O frontend é servido através de um volume montado no Nginx
- O MongoDB roda em modo daemon (`-d`) em background
- As portas são mapeadas para acesso externo aos serviços

## Tecnologias Utilizadas

- Docker & Docker Network
- Nginx (Alpine)
- Node.js & Express
- MongoDB
- HTML/CSS/JavaScript

 