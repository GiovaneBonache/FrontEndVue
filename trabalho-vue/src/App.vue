<template>
  <div>
    <div class="header">
      <h1>Site VUE Online</h1>
      <nav v-if="route.path !== '/'">
        <RouterLink to="/">Login</RouterLink>
        <RouterLink to="/home">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/usuarios">Usuários</RouterLink>
      </nav>
    </div>

    <div class="alternate" v-if="route.path !== '/'">
      <button v-if="isADM" @click="toggleADM">Administrador</button>
      <button @click="mudarCor">Cores</button>
    </div>

  
    <UserView v-show="mostrarADM && route.path !== '/'" />


    <RouterView :cor-ativa="corAtual" />
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import { useRoute } from "vue-router";
import UserView from './views/UsuarioView.vue';

const route = useRoute();


const mostrarADM = ref(false);
const toggleADM = () => mostrarADM.value = !mostrarADM.value;

const corAtual = ref("#34495E");
const cores = ["#34495E", "#E74C3C", "#2C3E50", "#F1C40F", "#1ABC9C"];
function mudarCor() {
  let nova = corAtual.value;
  while (nova === corAtual.value) {
    nova = cores[Math.floor(Math.random() * cores.length)];
  }
  corAtual.value = nova;
}

const papeis = JSON.parse(localStorage.getItem("papeis") || "[]");
const isADM = computed(() => papeis.includes("ADMIN"));
</script>

<style>
.header {
  position: fixed;
  top: 0;        
  left: 0;
  right: 0;         
  height: 60px;     
  background-color: #32805f;
  color: white;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 20px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}

nav {
  display: flex;
  gap: 40px; 
}
nav a {
  color: white;
  font-weight: bold;
  font-size: 20px;
}


button {
  margin: 5px;
  padding: 10px 20px;
  background-color: #32805f;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #27694b;
}

.alternate {
  display: flex;
  flex-direction: row;
  gap: 10px;
  position: fixed;
  top: 70px;
  left: 20px;
  z-index: 1000;
}
</style>