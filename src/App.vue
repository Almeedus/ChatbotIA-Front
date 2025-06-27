<template>
  <div id="app" class="app-container">
    <header class="app-header">
      <button class="mobile-menu-btn" @click="toggleSidebar">
        ☰
      </button>
      <h1 class="main-title">{{ selectedMenu }}</h1>
    </header>

    <SidebarContent
      v-if="showSidebar"
      class="sidebar"
      @menu-selected="updateSelectedMenu"
      @close-sidebar="showSidebar = false"
    />


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
      showSidebar: false, // inicia sempre fechado
    };
  },
  mounted() {
    if (window.innerWidth > 1000) {
      this.showSidebar = true; // mostra automaticamente no desktop
    }
    window.addEventListener("resize", this.handleResize);
  },
  beforeUnmount() {
    window.removeEventListener("resize", this.handleResize);
  },
  methods: {
    updateSelectedMenu(menu) {
      this.selectedMenu = menu;
      if (window.innerWidth <= 1000) this.showSidebar = false;
    },
    toggleSidebar() {
      this.showSidebar = !this.showSidebar;
    },
    handleResize() {
      if (window.innerWidth > 1000) {
        this.showSidebar = true;
      } else {
        this.showSidebar = false;
      }
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
  flex-direction: column;
  height: 100vh;
  position: relative;
}

.app-header {
  display: flex;
  align-items: center;
  padding: 10px 15px;
  background-color: #1e1e1e;
  border-bottom: 1px solid #444;
  z-index: 2;
  position: relative;
  justify-content: center;
}

.main-title {
  margin: 0;
  font-size: 20px;
  font-weight: bold;
  margin-left: 10px;
  flex: 1;
  text-align: center;
  width: 100%;
}

.mobile-menu-btn {
  background-color: #444;
  color: white;
  border: none;
  padding: 10px 15px;
  font-size: 20px;
  border-radius: 5px;
  cursor: pointer;
  z-index: 2;
}

.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  width: 300px;
  height: 100%;
  background-color: #292929;
  z-index: 10;
  transition: transform 0.3s ease-in-out;
}

.content-container {
  flex: 1;
  overflow-y: auto;
  padding: 15px;
}

/* DESKTOP */
@media (min-width: 1001px) {
  .app-container {
    flex-direction: row;
  }

  .app-header {
    position: fixed;
    top: 0;
    left: 300px;
    width: calc(100% - 300px);
  }

  .mobile-menu-btn {
    display: none;
  }

  .sidebar {
    position: static;
    width: 300px;
    height: auto;
    z-index: 1;
  }

  .content-container {
    margin-top: 60px;
  }
}
</style>
