<script setup>
import { ref } from "vue";
import api from "../api";

const usuariosLista = ref([]);

const buscarUsuarios = async () => {
  try {
    const response = await api.get("/usuarios", {
      headers: { Authorization: `Bearer ${localStorage.getItem("token")}` }
    });

    usuariosLista.value = Array.isArray(response.data) ? response.data : response.data.usuarios || [];

  } catch (e) {
    console.error("Erro ao buscar usuários:", e);
    alert("Erro ao buscar usuários");
  }
};

</script>

<template>
  <main>
    <div class="">
      <section id="card-1">
        <div class="usuarios-box">
          <div class="container">
          <button @click="buscarUsuarios" class="btn">Carregar Usuários</button>
          </div>
          <div v-for="usuario in usuariosLista" :key="usuario.id" class="usuario-card">
            <p><strong>ID:</strong> {{ usuario.id_usuario }} - <strong>Nome:</strong> {{ usuario.nome }} - <strong>Email:</strong> {{ usuario.email }} - <strong>Papel:</strong> {{ usuario.papeisString.join(", ") }}</p>
          </div>
        </div>

      </section>
    </div>

  </main>

</template>

<style scoped>
.container {
  max-width: 800px;
  text-align: center;
}

.btn {
  padding: 10px 20px;
  background-color: #41B883;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
  margin-bottom: 20px;
}

.btn:hover {
  background-color: #19d1df;
  transition: 1s;
}

.usuarios-box {
    background-color: #34495E;
    border-radius: 12px;
    padding: 20px;
    transition: all 0.3s ease;
    display: flex;
    gap: 10px;
    display: flex;
    flex-direction: column;
        width: 1000px;
    align-items: center;
    color: white;
    font-weight: 800;
    position: absolute;
    transform: translate(-50%, -50%);
    top: 55%;
    left: 50%;
    height: 760px;
    max-height: 760px;
    overflow-y: auto;
}

.usuario-card {
  background-color: none;
  border: 1px solid black;
  border-radius: 12px;
  padding: 15px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  transition: transform 0.2s;
  width: 900px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.usuario-card:hover {
  transform: translateY(-5px);
}
</style>

