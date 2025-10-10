# MyAgentAI
MyAgentAI

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

3) Edit Fields (Set): promptFInal: Inclui instrução de prompt para o Agent AI
4) AI Agent
5) Model Ollama Chat (llama3.2) Local Docker
6) Simple Memory (Guarda as últimas 5 interações)
7) Google Search para pesquisas na internet (https://www.searchapi.io/docs/google)
8) Send text message Telegram

OBS: Para utilizar o Telegram é necessário acessar o N8N via HTTPS. Para isso foi utlizado NGROK (https://dashboard.ngrok.com/agents) para gerar a conexão HTTPS.
