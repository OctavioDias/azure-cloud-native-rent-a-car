
# 🚗 Rent-a-Car API

Este projeto é uma API backend para gerenciamento de **locações de veículos**, desenvolvida com foco em um ambiente cloud-native utilizando serviços da **Azure**, como o **Service Bus** e **Container Apps**.

## 📦 Funcionalidades

- Criação de registros de locações de veículos.
- Envio de mensagens com os dados da locação para uma **fila do Azure Service Bus**.
- Suporte a CORS para integração com frontends diversos.
- Middleware para parsing de JSON.
- Estrutura preparada para autenticação com `DefaultAzureCredential`.

## 🛠️ Tecnologias Utilizadas

- [Node.js](https://nodejs.org/)
- [Express](https://expressjs.com/)
- [Azure Service Bus SDK](https://www.npmjs.com/package/@azure/service-bus)
- [dotenv](https://www.npmjs.com/package/dotenv)
- [CORS](https://www.npmjs.com/package/cors)

## 📁 Estrutura do Projeto

```bash
rent-a-car/
│
├── .env.example
├── index.js
├── package.json
├── Dockerfile
└── README.md
```

## ▶️ Como Executar o Projeto

### 1. Pré-requisitos

- Node.js instalado (versão 16 ou superior)
- Conta no [Microsoft Azure](https://azure.microsoft.com/)
- Azure Service Bus com uma fila chamada `fila-locacao-auto`

### 2. Configuração

Clone o repositório e instale as dependências:

```bash
git clone https://github.com/oMaestro174/azure-cloud-native-lab007.git
cd azure-cloud-native-lab007
npm install
```

Crie um arquivo `.env` com as variáveis de ambiente necessárias:

```env
AZURE_CLIENT_ID=<seu-client-id>
AZURE_TENANT_ID=<seu-tenant-id>
AZURE_CLIENT_SECRET=<seu-client-secret>
SERVICE_BUS_CONNECTION_STRING="Endpoint=sb://<seu-servicebus>.servicebus.windows.net/;SharedAccessKeyName=...;SharedAccessKey=..."
```

### 3. Executar o Servidor

```bash
node index.js
```

O servidor ficará disponível em: [http://localhost:3001](http://localhost:3001)

## 🔁 Endpoints

### POST `/api/locacao`

**Descrição**: Envia uma solicitação de locação para a fila no Azure Service Bus.

**Corpo da Requisição**:
```json
{
  "nome": "João",
  "email": "taguardado.net@gmail.com",
  "modelo": "Fusca",
  "ano": 1970,
  "tempoAluguel": 5
}
```

**Resposta de Sucesso (200)**:
```json
{
  "message": "Locação de veiculo enviada para a fila com sucesso para o Service Bus"
}
```

**Erro (500)**:
```json
{
  "message": "Erro ao enviar mensagem para o Service Bus"
}
```