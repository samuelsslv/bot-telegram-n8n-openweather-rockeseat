# Bot de Clima no Telegram com N8N

Bot do Telegram que consulta a temperatura atual de qualquer cidade do Brasil utilizando a API do OpenWeather.

## 📋 Descrição do Projeto

Este chatbot recebe o nome de uma cidade e estado via mensagem no Telegram, consulta a API do OpenWeather, processa os dados e retorna uma mensagem formatada com a temperatura atual da cidade solicitada.

**Exemplo de uso:**
- Usuário envia: `São Paulo,SP`
- Bot responde: `🌤️ A temperatura em São Paulo é de 25°C`

## 🚀 Como Criar um Bot no Telegram

### Passo 1: Criar o Bot no Telegram

1. Abra o aplicativo **Telegram** (web, desktop ou mobile)
2. Procure por **@BotFather** na busca
3. Inicie uma conversa e envie o comando `/newbot`
4. Siga as instruções:
   - Escolha um **nome** para o bot (ex: "Bot de Clima")
   - Escolha um **username** que termine com `bot` (ex: `meu_bot_clima_bot`)
5. O BotFather retornará um **token de acesso** no formato:
   ```
   123456789:ABCdefGHIjklMNOpqrsTUVwxyz
   ```
6. **IMPORTANTE:** Copie e guarde este token em local seguro. Você precisará dele para configurar o workflow no N8N.

### Passo 2: Obter API Key do OpenWeather

1. Acesse [https://home.openweathermap.org/users/sign_up](https://home.openweathermap.org/users/sign_up)
2. Crie uma conta gratuita
3. Confirme seu email através do link enviado
4. Após login, acesse [https://home.openweathermap.org/api_keys](https://home.openweathermap.org/api_keys)
5. Copie sua **API Key** (pode levar alguns minutos para ser ativada)

## 📥 Importação do Workflow no N8N

### Pré-requisitos

- N8N instalado e rodando (local ou cloud)
- Token do bot do Telegram
- API Key do OpenWeather

### Passos para Importar

1. Abra o N8N no seu navegador
2. Clique em **"Workflows"** no menu lateral
3. Clique no botão **"Import from File"** ou **"Import from URL"**
4. Selecione o arquivo `workflow-telegram-chatbot.json`
5. O workflow será importado e aparecerá na lista

## 🔐 Configuração de Credenciais
### Configurar Credencial do Telegram

1. No workflow importado, localize o nó **"Monitora Msgs do Bot"** 
2. Clique no nó e selecione **"Credential to connect with"**
3. Clique em **"Create New Credential"**
4. Escolha **"Telegram API"**
5. No campo **"Access Token"**, cole o token obtido do BotFather
6. Confirme se o campo **"Base URL"** esta com a URL **"https://api.telegram.org"**
6. Clique em **"Save"**

**Repita este processo para todos os nós do Telegram no workflow**.

### Configurar Credencial do OpenWeather

1. Localize o nó **"HTTP Request"** no workflow
2. No campo de parâmetros da query, encontre o parâmetro `appid`
3. Substitua `[OPENWEATHER_API_KEY]` pela sua API Key real
4. Ou configure como variável de ambiente no N8N:
   - Acesse **Settings** → **Variables**
   - Adicione uma variável chamada `OPENWEATHER_API_KEY` com o valor da sua chave
   - No nó HTTP Request, use `={{ $env.OPENWEATHER_API_KEY }}`

## 🎯 Como Executar o Bot

1. Após configurar todas as credenciais, clique em **"Active"** no workflow (toggle no canto superior direito)
2. O workflow ficará ativo e pronto para receber mensagens
3. Abra o Telegram e procure pelo seu bot pelo username que você criou
4. Envie uma mensagem no formato: `Cidade,UF`
   - Exemplos válidos:
     - `São Paulo,SP`
     - `Rio de Janeiro,RJ`
     - `Belo Horizonte,MG`
5. O bot responderá com a temperatura atual da cidade

Este projeto foi desenvolvido como parte de um desafio educacional.
