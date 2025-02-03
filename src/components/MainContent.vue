<template>
    <div class="main-content">
      <h1 class="main-title">{{ selectedMenuText }}</h1>
  
      <div class="chat-container">
        <!-- Mensagem do usuário -->
        <div class="user-message">
          <div class="message-content">
            Qual é o email de contato do IFSP de Itapetininga?
          </div>
          <div class="user-icon">
            <img src="@/assets/user-icon.png" alt="Ícone do Usuário" />
          </div>
        </div>
  
        <!-- Resposta do chatbot -->
        <div class="bot-message">
          <div class="bot-icon">
            <img src="@/assets/bot-icon.png" alt="Ícone do Sistema" />
          </div>
          <div class="message-content">
            O e-mail do campus de Itapetininga é matricula.itp@ifsp.edu.br.
          </div>
        </div>
  
        <!-- Campo de entrada -->
        <div class="input-container">
          <input type="text" placeholder="Escreva sua pergunta..." />
          <button>
            <img src="@/assets/send-icon.png" alt="Enviar" />
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      selectedMenuText: {
        type: String,
        default: "Bem Vindo",
      },
    },
  };
  </script>
  
  <style scoped>
  .main-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    color: #fff;
  }
  
  .main-title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 20px;
  }
  
  .chat-container {
    width: 80%;
    max-width: 600px;
    background-color: #1e1e1e;
    padding: 20px;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    gap: 20px;
  }
  
  /* Mensagem do usuário */
  .user-message,
  .bot-message {
    display: flex;
    align-items: flex-start;
    gap: 10px;
  }
  
  .user-message .message-content,
  .bot-message .message-content {
    background-color: #292929;
    padding: 10px 15px;
    border-radius: 10px;
    color: #fff;
  }
  
  .user-message .user-icon img {
    width: 30px;
    height: 30px;
  }
  
  .bot-message .bot-icon img {
    width: 30px;
    height: 30px;
    border-radius: 50%;
  }
  
  /* Campo de entrada */
  .input-container {
    display: flex;
    align-items: center;
    gap: 10px;
    background-color: #292929;
    padding: 10px;
    border-radius: 10px;
  }
  
  .input-container input {
    flex: 1;
    background: transparent;
    border: none;
    outline: none;
    color: #fff;
    padding: 10px;
  }
  
  .input-container button {
    background: none;
    border: none;
    cursor: pointer;
  }
  
  .input-container button img {
    width: 25px;
    height: 25px;
  }
  </style>
  