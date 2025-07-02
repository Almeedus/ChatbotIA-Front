<template>
  <div class="main-content">
    <div class="chat-container" ref="chatContainer">
      <div
        v-for="(msg, index) in messages"
        :key="index"
        class="message"
        :class="msg.sender"
      >
        <div class="icon" v-if="msg.sender === 'user'">
          <img src="@/assets/user-icon.png" alt="Usuário" />
        </div>
        <div v-if="msg.text !== '__pensando__'" class="message-content" v-html="msg.text"></div>
        <div v-else class="thinking-text">Pensando...</div>
      </div>
    </div>

    <div class="input-container">
      <input
        v-model="newMessage"
        @keyup.enter="sendMessage"
        type="text"
        placeholder="Escreva sua pergunta..."
      />
      <button @click="sendMessage">
        <img src="@/assets/send-icon.png" alt="Enviar" />
      </button>
    </div>
  </div>
</template>

<script>
import api from "@/api";

export default {
  props: {
    selectedMenu: { type: String, required: true },
  },
  data() {
    return {
      newMessage: "",
      messages: [],
      thinkingIndex: null,
    };
  },
  methods: {
    async sendMessage() {
      if (!this.newMessage.trim()) return;

      const userText = this.newMessage;
      this.messages.push({ text: userText, sender: "user" });
      this.newMessage = "";
      this.scrollToBottom();

      this.thinkingIndex = this.messages.length;
      this.messages.push({ text: "__pensando__", sender: "bot" });
      this.scrollToBottom();

      try {
        const response = await api.post(
          "/duvidas",
          {
            query: userText,
            section: this.selectedMenu,
          },
          { headers: { "Content-Type": "application/json" } }
        );

        const botText =
          response.data.messages.find((m) => m.role === "assistant")?.content ||
          "Desculpe, não consegui entender a resposta.";

        this.messages.splice(this.thinkingIndex, 1, {
          text: botText,
          sender: "bot",
        });
        this.thinkingIndex = null;
        this.scrollToBottom();
      } catch (err) {
        const errorText = "Desculpe, aconteceu um erro ao processar sua pergunta.";
        this.messages.splice(this.thinkingIndex, 1, {
          text: errorText,
          sender: "bot",
        });
        this.thinkingIndex = null;
        this.scrollToBottom();
      }
    },
    scrollToBottom() {
      this.$nextTick(() => {
        const c = this.$refs.chatContainer;
        if (c) c.scrollTop = c.scrollHeight;
      });
    },
  },
};
</script>

<style scoped>
.main-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100%;
  overflow: hidden;
  box-sizing: border-box;
  padding-bottom: 70px;
  color: #fff;
}

.chat-container {
  width: 80%;
  max-width: 1000px;
  background: #1e1e1e;
  padding: 20px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  overflow-y: auto;
  flex-grow: 1;
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
  align-items: flex-start;
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
  background: #292929;
  padding: 10px 15px;
  border-radius: 10px;
  max-width: 80%;
  word-wrap: break-word;
  white-space: pre-wrap;
  color: #fff;
}

.thinking-text {
  font-style: italic;
  color: #ccc;
  font-size: 15px;
}

.input-container {
  position: fixed;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  align-items: center;
  width: 90%;
  max-width: 500px;
  gap: 10px;
  z-index: 10;
}

.input-container input {
  flex: 1;
  background: #292929;
  border: none;
  border-radius: 10px;
  padding: 12px 15px;
  color: #fff;
  font-size: 16px;
  outline: none;
}

.input-container button {
  width: 40px;
  height: 40px;
  background: #444;
  border-radius: 50%;
  border: none;
  padding: 0;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
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
  }

  .input-container {
    width: 95%;
  }
}
</style>
