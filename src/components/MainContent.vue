<template>
  <div class="main-content">
    <h1 class="main-title">{{ selectedMenu }}</h1>

    <div class="chat-container" ref="chatContainer">
      <div v-for="(msg, index) in messages" :key="index" class="message" :class="msg.sender">
        <div class="icon">
          <img v-if="msg.sender === 'user'" src="@/assets/user-icon.png" alt="Usuário" />
          <img v-else src="@/assets/bot-icon.png" alt="Bot" />
        </div>
        <div class="message-content">
          {{ msg.text }}
        </div>
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
      messages: [], // Lista de mensagens do chat
    };
  },
  methods: {
    sendMessage() {
      if (this.newMessage.trim() !== "") {
        this.messages.push({ text: this.newMessage, sender: "user" });
        this.newMessage = "";
        this.$nextTick(() => {
          this.scrollToBottom();
        });

        // Simulando resposta do bot
        setTimeout(() => {
          this.messages.push({ text: "Resposta do bot...", sender: "bot" });
          this.$nextTick(() => {
            this.scrollToBottom();
          });
        }, 1000);
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
  color: #fff;
}

.main-title {
  position: fixed;
  top: 0;
  left: 300px;
  width: calc(100% - 300px);
  background-color: #1e1e1e;
  padding: 15px 0;
  text-align: center;
  font-size: 24px;
  font-weight: bold;
  z-index: 10;
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
  gap: 10px;
  overflow-y: auto;
  max-height: 50vh;
  padding-bottom: 80px;
}

.chat-container::-webkit-scrollbar {
  width: 8px; /* Largura da barra de rolagem */
}

.chat-container::-webkit-scrollbar-track {
  background: #292929; /* Cor do fundo da barra de rolagem */
  border-radius: 10px;
}

.chat-container::-webkit-scrollbar-thumb {
  background: #00ff88; /* Cor do "botão" da barra de rolagem */
  border-radius: 10px;
}

.chat-container::-webkit-scrollbar-thumb:hover {
  background: #00ff95; /* Cor ao passar o mouse */
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
  background-color: #292929;
  padding: 10px;
  border-radius: 10px;
  position: fixed;
  bottom: 10px;
  left: 300px;
  width: calc(80% - 300px);
  z-index: 10;
  left: 30%;
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