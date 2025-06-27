<template>
  <div id="app" class="app-container">
    <button class="mobile-menu-btn" @click="toggleSidebar">
      ☰
    </button>
    <SidebarContent v-if="showSidebar" @menu-selected="updateSelectedMenu" />

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
      showSidebar: window.innerWidth > 420,
    };
  },
  methods: {
    updateSelectedMenu(menu) {
      this.selectedMenu = menu;
      if (window.innerWidth <= 420) this.showSidebar = false;
    },
    toggleSidebar() {
      this.showSidebar = !this.showSidebar;
    },
  },
};
</script>

<style>
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

.mobile-menu-btn {
  display: none;
  position: fixed;
  top: 10px;
  left: 10px;
  z-index: 9999;
  background-color: #444;
  color: white;
  border: none;
  padding: 10px 15px;
  font-size: 20px;
  border-radius: 5px;
}

@media (max-width: 420px) {
  .app-container {
    flex-direction: column;
  }

  .sidebar {
    display: none;
  }

  .mobile-menu-btn {
    display: block;
  }

  .content-container {
    width: 100%;
  }
}
</style>
