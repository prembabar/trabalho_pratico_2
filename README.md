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

Aplicar conceitos de sistemas distribuídos através da conteinerização de uma aplicação completa, separando:

* Frontend
* Backend
* Banco de Dados

Garantindo comunicação entre os serviços via rede Docker.

---

## 🧱 Arquitetura

* Frontend → Nginx (porta 8080)
* Backend → Node.js + Express (porta 3001)
* Banco de Dados → PostgreSQL (porta 5432)

---

## ⚙️ Pré-requisitos

Antes de começar, instale:

* Docker Desktop

Verifique a instalação:

```bash
docker --version
```

---

# 🚀 PASSO A PASSO DE EXECUÇÃO

## 1. Clonar o repositório

```bash
git clone https://github.com/prembabar/trabalho_pratico_2
cd trabalho_pratico_2
```

---

## 2. Criar rede Docker

```bash
docker network create minha-rede
```

---

## 3. Subir Banco de Dados (PostgreSQL)

```bash
docker run -d --name postgres --network minha-rede -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=admin -e POSTGRES_DB=tarefas -v postgres_data:/var/lib/postgresql/data -p 5432:5432 postgres:15
```
---

## 4. Build do Backend

```bash
cd backend
docker build -t backend-image .
```

---

## 5. Subir Backend

```bash
docker run -d --name backend --network minha-rede -p 3001:3001 -e DB_HOST=postgres -e DB_USER=postgres -e DB_PASSWORD=admin -e DB_NAME=tarefas -e DB_PORT=5432 backend-image
```

### 📌 Importante:

* `DB_HOST=postgres` → nome do container do banco
* Não usar `localhost`

---

## 6. Build do Frontend

```bash
cd ../frontend
docker build -t frontend-image .
```

---

## 7. Subir Frontend

```bash
docker run -d --name frontend --network minha-rede -p 8080:80 frontend-image
```

---

# 🌐 ACESSO À APLICAÇÃO

* Frontend: http://localhost:8080
* Backend: http://localhost:3001

---

# 🧪 TESTES (PARA VALIDAÇÃO)

## ✅ 1. Verificar containers ativos

```bash
docker ps
```

Deve aparecer:

* postgres
* backend
* frontend

---

## ✅ 2. Testar aplicação

1. Acesse o frontend
2. Crie uma nova tarefa
3. Verifique se aparece na lista

---

# 🏁 CONCLUSÃO

Este projeto possui:

* Containerização completa
* Arquitetura distribuída
* Comunicação entre serviços
* Persistência de dados

---
