<template>
  <div id="app" class="app-container">
    <SidebarContent @menu-selected="updateSelectedMenu" />
    <div class="content-container">
      <MainContent :selectedMenu="selectedMenu" />
    </div>
  </div>
</template>

<script>
import SidebarContent from "./components/SidebarContent.vue";
import MainContent from "./components/MainContent.vue";

export default {
  components: {
    SidebarContent,
    MainContent,
  },
  data() {
    return {
      selectedMenu: "Bem-vindo",
    };
  },
  methods: {
    updateSelectedMenu(menu) {
      this.selectedMenu = menu;
    },
  },
};
</script>

<style>
/* Estilos gerais */
body {
  margin: 0;
  font-family: "Arial", sans-serif;
  background-color: #1e1e1e;
  color: #fff;
}

.app-container {
  display: flex;
  height: 100vh;
}

.content-container {
  flex: 1;
  display: flex;
  flex-direction: column;
}
</style>
