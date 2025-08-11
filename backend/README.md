# Documentação do Backend - UTM Observer

## Visão Geral

O backend do sistema UTM Observer é uma API RESTful construída com FastAPI que fornece funcionalidades para gerenciamento de interações no ecossistema UTM (Unmanned Traffic Management). O sistema permite consultas a dados de voos, restrições e intenções operacionais em áreas específicas.

## Documentação Organizada

A documentação completa do backend foi organizada em uma estrutura mais clara e acessível.

## Estrutura de Diretórios

```
backend/
├── app.py                 # Ponto de entrada da aplicação FastAPI
├── main.py                # Script para execução do servidor
├── config/                # Configurações do sistema
│   └── config.py          # Configuração das variáveis de ambiente
├── routes/                # Definições das rotas da API
│   ├── fetch.py           # Rota para consultas de volumes
│   ├── constraint_management.py  # Rota para gerenciamento de restrições
│   └── health.py          # Rota para verificação de saúde
├── schemas/               # Definições de esquemas Pydantic
│   ├── common/            # Esquemas comuns
│   ├── dss/               # Esquemas específicos para DSS
│   ├── uss/               # Esquemas específicos para USS
│   └── fetch.py           # Esquemas para requisições de fetch
├── services/              # Implementações dos serviços
│   ├── dss/               # Serviços para DSS
│   ├── uss/               # Serviços para USS
│   └── flights.py         # Serviço para consulta de voos
└── requirements.txt       # Dependências do projeto
```

## Dependências Principais

- **FastAPI**: Framework web moderno e rápido
- **Uvicorn**: Servidor ASGI para execução da API
- **Pydantic**: Validação e serialização de dados
- **Motor**: Cliente assíncrono para MongoDB
- **HTTPX**: Cliente HTTP assíncrono

## Configurações do Ambiente

O sistema utiliza variáveis de ambiente definidas no arquivo `.env`. As principais variáveis são:

- `BRUTM_KEY`: Chave de acesso ao serviço
- `BRUTM_BASE_URL`: URL base do serviço

## Rotas Principais

### Consulta de Volumes
- **POST** `/fetch/volumes`
  - Consulta restrições e intenções operacionais em uma área específica
  - Retorna dados sobre voos, restrições e áreas de serviço

### Consulta de Voos
- **POST** `/fetch/flights`
  - Consulta dados de voos em tempo real
  - Retorna informações sobre voos atuais na área especificada

### Saúde da API
- **GET** `/api/healthy`
  - Verifica o status de saúde da API

## Como Executar

1. Instalar UV e dependências:

```sh
curl -LsSf https://astral.sh/uv/install.sh | sh
```

2. Instalar Python e criar ambiente virtual:

```sh
uv venv --python 3.12
source .venv/bin/activate
```

3. Instalar dependências:

```sh
uv sync --group test
```

4. Configure as variáveis de ambiente no arquivo `.env`

```ini
BRUTM_KEY=brutm
BRUTM_BASE_URL=http://api.dev.br-utm.org
```

5. Execute o servidor:
   ```sh
   cd backend
   uv run main.py
   ```

6. A API poderá ser testada em `http://localhost:8000/api/healthy`
