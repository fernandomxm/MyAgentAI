# MyAgentAI
![IMAGE01](https://github.com/fernandomxm/MyAgentAI/blob/main/MyAgentAI.png) 

Componentes:

1) Telegram Trigger: Bot Telegram @BotFather
2) Code: Get Date (JavaScript) pegar data atual: <br> <br>

for (const item of items) {  <br>
  const dateOptions = { <br>
    day: '2-digit', <br>
    month: '2-digit', <br>
    year: 'numeric', <br>
    hour: '2-digit', <br>
    minute: '2-digit', <br>
    second: '2-digit', <br>
    hour12: false <br>
  };   <br>
  // Use o campo que o Telegram Trigger está gerando, que é 'text' <br>
  const userInput = item.json.text || item.json.message.text;  <br>
  item.json.currentDate = new Date().toLocaleString('pt-BR', dateOptions); <br>
  item.json.currentISO = new Date().toISOString(); <br>
  item.json.message.text = userInput; // Garante que o LLM receba no formato esperado <br>
} <br>
return items; <br> <br>

3) Edit Fields (Set): promptFInal: Inclui instrução de prompt para o Agent AI  <br>
4) AI Agent  <br>
5) Model Ollama (qwen2.5) rodando como processo no linux (Melhor performance que em Docker) <br>
     vim /etc/systemd/system/ollama.service <br>
      Environment="OLLAMA_HOST=0.0.0.0:11434" <br>
 <br>
      systemctl daemon-reload <br>
      systemctl stop ollama <br>
      systemctl start ollama <br>
      netstat -anp | grep 11434 <br>
 <br>
      docker-compose.yml <br>
 <br>
x-n8n: &service-n8n <br>
  image: n8nio/n8n:latest <br>
  networks: ['demo'] <br>
  environment: <br>
    - DB_TYPE=postgresdb <br>
    - DB_POSTGRESDB_HOST=postgres <br>
    - DB_POSTGRESDB_USER=${POSTGRES_USER} <br>
    - DB_POSTGRESDB_PASSWORD=${POSTGRES_PASSWORD} <br>
    - N8N_DIAGNOSTICS_ENABLED=false <br>
    - N8N_PERSONALIZATION_ENABLED=false <br>
    - N8N_ENCRYPTION_KEY <br>
    - N8N_USER_MANAGEMENT_JWT_SECRET <br>
    - OLLAMA_HOST=host.docker.internal:11434 <br>
 <br>
n8n: <br>
   ports: <br>
      - 5678:5678 <br>
    extra_hosts: <br>
      - "host.docker.internal:host-gateway" <br>
 <br>
Precisei usar qwen2.5 ao invés do llama3 pois o llama3 não suporta chamadas para tools <br>
 <br>
7) Simple Memory (Guarda as últimas 5 interações) <br>
8) Google Search para pesquisas na internet (https://www.searchapi.io/docs/google) <br>
9) Send text message Telegram <br>
 <br>
OBS: Para utilizar o Telegram é necessário acessar o N8N via HTTPS. Para isso foi utlizado NGROK (https://dashboard.ngrok.com/agents) para gerar a conexão HTTPS. <br>
 <br>
https://youtu.be/xz_X2N-hPg0?si=HozjCrOXs8a9ZXuW
