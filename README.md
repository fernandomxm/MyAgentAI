# MyAgentAI
MyAgentAI

Componentes:

1) Telegram Trigger: Bot Telegram @BotFather
2) Get Date (JavaScript) pegar data atual: 

for (const item of items) {  
  const dateOptions = {
    day: '2-digit',
    month: '2-digit',
    year: 'numeric',
    hour: '2-digit',
    minute: '2-digit',
    second: '2-digit',
    hour12: false
  };  
  // Use o campo que o Telegram Trigger está gerando, que é 'text'
  const userInput = item.json.text || item.json.message.text; 
  item.json.currentDate = new Date().toLocaleString('pt-BR', dateOptions);
  item.json.currentISO = new Date().toISOString();
  item.json.message.text = userInput; // Garante que o LLM receba no formato esperado
}
return items;

3) promptFInal: Inclui instrução de prompt para o Agent AI
4) AI Agent
5) Model Ollama Chat (llama3.2) Local Docker
6) Simple Memory (Guarda as últimas 5 interações)
7) Google Search para pesquisas na internet (https://www.searchapi.io/docs/google)
8) Send text message Telegram

OBS: Para utilizar o Telegram é necessário acessar o N8N via HTTPS. Para isso foi utlizado NGROK (https://dashboard.ngrok.com/agents) para gerar a conexão HTTPS.
