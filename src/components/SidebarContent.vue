<template>
  <aside class="sidebar">
    <button class="close-btn" @click="$emit('close-sidebar')">✕</button>

    <div class="logo">
      <img src="@/assets/logo.png" alt="Logo ChatBot IFSP" />
      <h2>SEÇÃO DE DÚVIDAS</h2>
    </div>
    <ul class="menu">
      <li v-for="item in menuItems" :key="item.text" @click="selectItem(item)">
        {{ item.text }}
      </li>
    </ul>
  </aside>
</template>

<script>
export default {
  data() {
    return {
      menuItems: [
        { text: "Locais de Prova", value: "Locais de Prova" },
        { text: "Emails de contato", value: "Emails de Contato" },
        { text: "Datas importantes", value: "Datas Importantes" },
        { text: "Outras Dúvidas", value: "Outras Dúvidas" },
      ],
    };
  },
  methods: {
    selectItem(item) {
      this.$emit("menu-selected", item.text);
    },
  },
};
</script>

<style scoped>
.sidebar {
  width: 300px;
  height: 100vh;
  background-color: #292929;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  padding-top: 20px;
}

.close-btn {
  display: none;
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  color: #fff;
  font-size: 24px;
  cursor: pointer;
  z-index: 1000;
}

@media (max-width: 420px) {
  .close-btn {
    display: block;
  }
}

.logo {
  text-align: center;
  margin-bottom: 30px;
  margin-top: 30px;
}

.logo img {
  width: 100px;
  margin-bottom: 10px;
}

.logo h2 {
  font-size: 18px;
  color: white;
}

.menu {
  list-style: none;
  padding: 0;
  margin: 0;
  width: 100%;
}

.menu li {
  cursor: pointer;
  margin: 10px 0;
  padding: 10px;
  text-align: center;
  border-radius: 4px;
  color: #ffffff;
  transition: background-color 0.3s ease;
}

.menu li:hover {
  background-color: #00ff88;
  color: #000;
}
</style>
