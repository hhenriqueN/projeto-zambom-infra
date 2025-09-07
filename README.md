
# Projeto Zambom - Infraestrutura

Este repositório contém a configuração de **infraestrutura** do Projeto de Software, utilizando **Docker Compose** para orquestrar os serviços e o banco de dados.

## 🚀 Serviços incluídos

O `docker-compose.yml` sobe os seguintes containers:

- `atividades-service` → imagem do DockerHub `iquenavarro/atividades-service:latest`
- `progresso-service` → imagem do DockerHub `iquenavarro/progresso-service:latest`
- `agendamento-service` → imagem do DockerHub `iquenavarro/agendamento-service:latest`
- `mongo` → banco de dados MongoDB oficial (`mongo:6`)

Cada serviço utiliza uma base separada dentro do mesmo MongoDB:

- `atividades_db`
- `progresso_db`
- `agendamento_db`

---

## 📦 Pré-requisitos

- [Docker](https://docs.docker.com/get-docker/) instalado
- [Docker Compose](https://docs.docker.com/compose/) instalado (já vem junto com o Docker Desktop)

---

## ▶️ Como rodar o ambiente

1. Clone este repositório:

   ```bash
   git clone https://github.com/<seu-usuario>/projeto-zambom-infra.git
   cd projeto-zambom-infra
   ```

2. Suba os containers:

   ```bash
   docker compose up
   ```

   > Para rodar em segundo plano:
   > ```bash
   > docker compose up -d
   > ```

3. Serviços disponíveis:

   - **Atividades Service:** [http://localhost:8001](http://localhost:8001)
   - **Progresso Service:** [http://localhost:8002](http://localhost:8002)
   - **Agendamento Service:** [http://localhost:8003](http://localhost:8003)
   - **MongoDB:** `localhost:27017`

---

## 🛠️ Acessando o MongoDB

O Mongo roda dentro de um container, mas está exposto na porta `27017`.

Você pode acessar de diferentes formas:

### 1. Linha de comando (CLI do Mongo)

Instale o cliente Mongo (`mongosh`) e conecte:

```bash
mongosh "mongodb://localhost:27017"
```

Listar bancos de dados:

```bash
show dbs
```

Trocar para um banco (exemplo atividades):

```bash
use atividades_db
```

### 2. MongoDB Compass (GUI)

Baixe [MongoDB Compass](https://www.mongodb.com/products/compass) e conecte usando a URI:

```
mongodb://localhost:27017
```

### 3. Extensão no VSCode

- Instale **MongoDB for VS Code**
- Configure a conexão com `mongodb://localhost:27017`

---

## 📌 Observações importantes

- As imagens dos serviços são puxadas automaticamente do DockerHub:
  - `iquenavarro/atividades-service:latest`
  - `iquenavarro/progresso-service:latest`
  - `iquenavarro/agendamento-service:latest`
- Sempre que houver push no GitHub (branch `main`) dos serviços, novas imagens serão publicadas no DockerHub via **GitHub Actions**.
- Para aplicar atualizações no ambiente, basta rodar novamente:
  ```bash
  docker compose pull
  docker compose up -d
  ```

