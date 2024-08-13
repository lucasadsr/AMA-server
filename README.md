# AMA API

Esta API foi desenvolvida em Go e serve como backend para um aplicativo de AMA (Ask Me Anything). Ela utiliza WebSockets para comunicação em tempo real, PostgreSQL como banco de dados, e está containerizada usando Docker. Além disso, o Tern é usado para análise de dependências de segurança.

## Índice

- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Configuração](#configuração)
- [Uso](#uso)
- [Documentação da API](#documentação-da-api)

## Pré-requisitos

Antes de começar, certifique-se de ter as seguintes ferramentas instaladas:

- [Go](https://golang.org/dl/)
- [Docker](https://www.docker.com/get-started)
- [Tern](https://github.com/tern-tools/tern)

## Instalação

Clone o repositório e navegue até o diretório do projeto:

```bash
git clone https://github.com/lucasadsr/AMA-server.git
cd AMA-server
```

Construa e inicie os containers Docker:
```bash
docker-compose up --build
```
Isso irá configurar e iniciar a API, junto com um container do PostgreSQL.

## Configuração
Crie um arquivo .env na raiz do projeto e configure as seguintes variáveis de ambiente:
```env
WSRS_DATABASE_PORT=
WSRS_DATABASE_USER=
WSRS_DATABASE_PASSWORD=
WSRS_DATABASE_NAME=
WSRS_DATABASE_HOST="localhost"
```

## Uso
Para iniciar a API localmente, execute:
```bash
go run ./cmd/ws/main.go
```
A API estará disponível em http://localhost:8080.

## Documentação da API

### Endpoints

#### Rooms

- `POST /api/rooms` - Cria uma nova sala.
- `GET /api/rooms` - Retorna uma lista de salas.
- `GET /api/rooms/{room_id}` - Retorna detalhes de uma sala específica.

#### Messages

- `POST /api/rooms/{room_id}/messages` - Cria uma nova mensagem em uma sala.
- `GET /api/rooms/{room_id}/messages` - Retorna uma lista de mensagens em uma sala.
- `GET /api/rooms/{room_id}/messages/{message_id}` - Retorna detalhes de uma mensagem específica.
- `PATCH /api/rooms/{room_id}/messages/{message_id}/react` - Adiciona uma reação a uma mensagem.
- `DELETE /api/rooms/{room_id}/messages/{message_id}/react` - Remove uma reação de uma mensagem.
- `PATCH /api/rooms/{room_id}/messages/{message_id}/answer` - Marca uma mensagem como respondida.

#### WebSockets

- `GET /subscribe/{room_id}` - Estabelece uma conexão WebSocket para receber atualizações em tempo real sobre uma sala específica.
