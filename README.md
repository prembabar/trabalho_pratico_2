# 📦 Projeto Docker - Lista de Tarefas

## 👥 Integrantes

| Nome         | RA    |
| ------------ | ----- |
| João Felipe Vilela Nunes     | 2310253   |
| Leonardo Valverde de Oliveira | 2310169 |
| Luiz Antônio de Paula Gomes | 2310406 |
| Prem Babar | 2310695 |
    
---

## 🎯 Objetivo

Containerizar uma aplicação completa (Frontend, Backend e Banco de Dados) utilizando Docker, garantindo comunicação entre os serviços através de rede customizada.

---

## 🧱 Arquitetura

* Frontend → Nginx (porta 8080)
* Backend → Node.js + Express (porta 3001)
* Banco → PostgreSQL (porta 5432)

---

## ⚙️ Pré-requisitos

* Docker instalado

Verificar:

```bash
docker --version
```

---

## 🚀 Passo a passo de execução

### 1. Clonar o projeto

```bash
git clone https://github.com/oLopesAlvaro/tarefas-docker.git
cd tarefas-docker
```

---

### 2. Criar rede Docker

```bash
docker network create minha-rede
```

---

### 3. Rodar banco de dados

```bash
docker run -d --name postgres --network minha-rede -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=admin -e POSTGRES_DB=tarefas -v postgres_data:/var/lib/postgresql/data -p 5432:5432 postgres:15
```

---

### 4. Build do Backend

```bash
cd backend
docker build -t backend-image .
```

---

### 5. Rodar Backend

```bash
docker run -d --name backend --network minha-rede -p 3001:3001 -e DB_HOST=postgres -e DB_USER=postgres -e DB_PASSWORD=admin -e DB_NAME=tarefas -e DB_PORT=5432 backend-image
```

---

### 6. Build do Frontend

```bash
cd ../frontend
docker build -t frontend-image .
```

---

### 7. Rodar Frontend

```bash
docker run -d --name frontend --network minha-rede -p 8080:80 frontend-image
```

---

## 🌐 Acesso

* Frontend: http://localhost:8080
* Backend: http://localhost:3001

---

## 🧪 Testes

### Verificar containers:

```bash
docker ps
```

Deve aparecer:

* postgres
* backend
* frontend

---

### Testar aplicação

1. Acessar frontend
2. Criar uma tarefa
3. Verificar se aparece na lista

---

### Testar persistência

1. Parar containers:

```bash
docker stop frontend backend postgres
```

2. Subir novamente (passos 3 a 7)

3. Verificar se tarefas continuam

---

## 📌 Observações

* Containers se comunicam pelo nome
* Não utilizar localhost entre containers
* Banco de dados possui persistência via volume Docker

---
