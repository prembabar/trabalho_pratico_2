    # Guia de Execução Local do Frontend (React + Vite)

Olá! Este guia detalha como executar **apenas o frontend** da aplicação diretamente na sua máquina, sem o uso de Docker.

O objetivo é permitir que você veja a interface, interaja com ela e, principalmente, teste se ela consegue se comunicar com o **serviço de backend**, que deve estar rodando separadamente. O frontend roda, por padrão, na porta `5173`.

## 🛠️ Pré-requisitos

Antes de começar, você precisa ter:

1.  **Node.js**: Versão 22.
2.  **Git**: Para clonar o repositório.
3.  **Um Navegador Web**: Como Chrome, Firefox ou Edge.
4.  **Backend em Execução**: Este guia assume que você já seguiu o guia do backend e que ele está **rodando localmente** na porta `3001`. O frontend não funciona sozinho, ele precisa da API para buscar e salvar dados.
5.  **Porta do Frontend**: O frontend será servido na porta `5173` por padrão.

## 👣 Passo a Passo

### Passo 1: Clone o Repositório e Prepare o Ambiente

Se ainda não o fez, clone o projeto e navegue até a pasta correta em um **novo terminal**. É importante que o terminal do backend continue em execução.

```bash
# Clone o repositório do projeto (se ainda não o fez)
git clone <URL_DO_REPOSITORIO>

# Entre na pasta raiz do projeto
cd <NOME_DA_PARA_DO_PROJETO>

# Navegue até a pasta específica do frontend
cd frontend
```

### Passo 2: Instale as Dependências

Dentro da pasta `frontend`, execute o seguinte comando para baixar todas as bibliotecas que o React precisa para funcionar.

```bash
npm install
```

### Passo 3: Execute a Aplicação

Com a configuração verificada, inicie o servidor de desenvolvimento do frontend:

```bash
npm run dev -- --host
```

> Observação: ao rodar o frontend dentro de um container Docker, é necessário expor o servidor de desenvolvimento. Use o flag `-- --host` ao executar `npm run dev`. Sem esse flag o Vite ficará acessível apenas dentro do container e não será visível do host. Lembre-se de incluir esse comando (ou ajustar o script/Dockerfile/docker-compose) ao dockerizar a aplicação.

### Passo 4: Verifique o Funcionamento

Após executar o comando, algumas coisas acontecerão:

1.  Seu terminal mostrará uma URL local, geralmente `http://localhost:5173/`.
2.  Seu navegador web padrão deverá abrir automaticamente nesta URL.
3.  A aplicação da "Lista de Tarefas" será exibida.