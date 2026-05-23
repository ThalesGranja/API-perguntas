# 🚀 API de Perguntas e Respostas (Prisma ORM + Docker)

Uma API RESTful construída com Node.js e TypeScript para o gerenciamento de Usuários e Perguntas. Este projeto foi desenvolvido com o propósito de estudar e aplicar na prática a conteinerização de ambientes com Docker, bem como a modelagem e manipulação de banco de dados PostgreSQL utilizando a ferramenta Prisma ORM.

## 🛠️ Tecnologias Utilizadas

- **Node.js** com **TypeScript**
- **Express** (Roteamento da API)
- **Prisma ORM** (Modelagem e manipulação do Banco de Dados)
- **PostgreSQL** (Banco de Dados Relacional)
- **Docker** (Conteinerização do ambiente)

## 📋 Pré-requisitos

Antes de começar, certifique-se de ter as seguintes ferramentas instaladas em sua máquina:
- [Git](https://git-scm.com/)
- [Node.js](https://nodejs.org/en/)
- [Docker](https://www.docker.com/)

## ⚙️ Como executar o projeto na sua máquina

### 1. Clone o repositório e instale as dependências

Primeiro, faça o clone do projeto e acesse a pasta raiz:

```bash
git clone [https://github.com/thalesgranja/nome-do-seu-repositorio.git](https://github.com/thalesgranja/nome-do-seu-repositorio.git)
cd nome-do-seu-repositorio
```

Em seguida, instale as dependências do projeto:

```bash
npm install
```

### 2. Configure o Banco de Dados com Docker

Para rodar o banco de dados localmente sem precisar instalar o PostgreSQL na sua máquina, utilize o Docker. Execute o comando abaixo no seu terminal para criar e iniciar o container:

```bash
docker run --name postgres-orm -e POSTGRESQL_USERNAME=postgres -e POSTGRESQL_PASSWORD=postgres -e POSTGRES_DATABASE=api -p 5432:5432 -d bitnami/postgresql:latest
```

### 3. Configuração das Variáveis de Ambiente

Para que a aplicação consiga se conectar ao banco de dados que acabou de ser criado no Docker, é obrigatório criar um arquivo `.env` na **raiz do projeto**.

Crie o arquivo `.env` e adicione a variável `DATABASE_URL` com as credenciais corretas (baseadas no comando Docker acima):

```env
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/api?schema=public"
```

### 4. Execute as Migrations e o Seed do Prisma

Com o banco de dados rodando e o arquivo `.env` configurado, sincronize a estrutura do banco de dados e insira os dados iniciais (seed):

```bash
npx prisma migrate dev
npx prisma db seed
```

### 5. Inicie a aplicação

Tudo pronto! Agora é só iniciar o servidor de desenvolvimento:

```bash
npm run dev
```

O servidor estará rodando na porta **3333**. Você pode acessar e testar a API através da URL base: `http://localhost:3333`.

## 📌 Rotas Disponíveis (Endpoints)

**Usuários (`/users`)**

* `GET /users` - Lista todos os usuários
* `POST /users` - Cria um novo usuário
* `GET /users/:id` - Busca os detalhes de um usuário específico

**Perguntas (`/questions`)**

* `GET /questions` - Lista todas as perguntas (permite filtragem por título na query `?title=`)
* `POST /questions` - Cria uma nova pergunta vinculada a um usuário
* `PUT /questions/:id` - Atualiza o título e/ou conteúdo de uma pergunta
* `DELETE /questions/:id` - Exclui uma pergunta

---

Desenvolvido por [Thales Granja](https://github.com/thalesgranja).
