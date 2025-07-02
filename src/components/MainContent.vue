<template>
  <div class="main-content">

    <div class="chat-container" ref="chatContainer">
      <div v-for="(msg, index) in messages" :key="index" class="message" :class="msg.sender">
        <div class="icon" v-if="msg.sender === 'user'">
          <img src="@/assets/user-icon.png" alt="Usuário" />
        </div>
      <div class="message-content" v-html="msg.text"></div>
    </div>
    </div>

    <div class="input-container">
      <input v-model="newMessage" @keyup.enter="sendMessage" type="text" placeholder="Escreva sua pergunta..." />
      <button @click="sendMessage">
        <img src="@/assets/send-icon.png" alt="Enviar" />
      </button>
    </div>
  </div>
</template>

<script>
import api from '@/api';

export default {
  props: {
    selectedMenu: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      newMessage: "",
      messages: [], 
    };
  },
  methods: {
    async sendMessage() {
      if (this.newMessage.trim() !== "") {
        const userMessage = this.newMessage;
        this.messages.push({ text: this.newMessage, sender: "user" });
        this.newMessage = '';
        this.scrollToBottom();

        try {
          const response = await api.post("/duvidas", { query: userMessage }, {headers: { "Content-Type": "application/json" }});
          const botMessage = response.data.messages.find(msg => msg.role === "assistant")?.content || "Desculpe, não consegui entender a resposta.";
          this.messages.push({ text: botMessage, sender: "bot" });
          this.scrollToBottom();
        }
        catch (error) {
          console.error("Erro ao enviar a mensagem:", error);
          this.messages.push({ text: "Desculpe, aconteceu um erro ao processar sua pergunta.", sender: "bot" });
          this.scrollToBottom();	
        }
      }
    },
    scrollToBottom() {
      const container = this.$refs.chatContainer;
      if (container) {
        container.scrollTop = container.scrollHeight;
      }
    }
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
  box-sizing: border-box;
  overflow: hidden;
  color: #fff;
}

.chat-container {
  width: 80%;
  max-width: 600px;
  background-color: #1e1e1e;
  padding: 20px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  overflow-y: auto;
  max-height: 50vh;
  max-width: 1000px;
  padding-bottom: 80px;
  flex-grow: 1; 
  margin-bottom: 20px; 
}

.chat-container::-webkit-scrollbar {
  width: 8px; 
}

.chat-container::-webkit-scrollbar-track {
  background: #292929;
  border-radius: 10px;
}

.chat-container::-webkit-scrollbar-thumb {
  background: #00ff88;
  border-radius: 10px;
}

.chat-container::-webkit-scrollbar-thumb:hover {
  background: #00ff95;
}

.message {
  display: flex;
  align-items: center;
  gap: 10px;
}

.user {
  justify-content: flex-end;
}

.bot {
  justify-content: flex-start;
}

.icon img {
  width: 30px;
  height: 30px;
  border-radius: 50%;
}

.message-content {
  background-color: #292929;
  padding: 10px 15px;
  border-radius: 10px;
  color: #fff;
}

.input-container {
  display: flex;
  align-items: center;
  gap: 10px;
  position: fixed;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  width: 90%;
  max-width: 500px;
  z-index: 10;
}

.input-container input {
  flex: none;
  width: 85%;
  background-color: #292929;
  border: none;
  outline: none;
  padding: 10px 15px;
  border-radius: 10px;
  color: #fff;
  font-size: 16px;
}

.input-container button {
  flex: none;
  width: 40px;
  height: 40px;
  background: #444;
  border-radius: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  border: none;
  padding: 0;
}

.input-container button img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

@media (max-width: 420px) {
  .chat-container {
    width: 100%;
    padding: 10px;
    border-radius: 0;
    height: 65vh;
    overflow-y: auto;
  }
}
</style>
