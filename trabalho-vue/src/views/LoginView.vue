<script setup>
import { ref } from "vue"
import api from "@/api"
import { useRouter } from "vue-router"

const email = ref("")
const senha = ref("")
const router = useRouter()

async function login() {
  try {
    const response = await api.post("/login", {
      email: email.value,
      senha: senha.value
    });

    const token = response.data.token;
    localStorage.setItem("token", token);
    
    await buscarUsuarioLogado();
    alert("Login feito!");
    router.push("/home")
  } catch (e) {
    alert("Erro no login");
  }
}

function logout() {
  localStorage.removeItem("token")
  router.push("/login")
}

async function buscarUsuarioLogado() {
  try {
    const response = await api.get("/usuarios", {
      headers: { Authorization: `Bearer ${localStorage.getItem("token")}` }
    });
    const usuario = response.data.find(u => u.email === email.value);

    if (usuario) {
      localStorage.setItem("papeis", JSON.stringify(usuario.papeisString));
    }
  } catch (e) {
    console.error("Erro ao buscar usuário logado:", e);
  }
}


</script>

<template>
  <div class="conteudo">
    <div class="imagem">
      <img src="@/img/vueimagem.jpeg" alt="">
    </div>
    <div class="login">
      <div class="texto">
        <h1>Faça o login</h1>
      </div>
      <div >
        <input class="usuario"  v-model="email" placeholder="Usuario" />
      </div>
      <div>
        <input class="senha"  v-model="senha" type="password" placeholder="Senha" />
      </div>
      <div class="botoes">
        <button @click="login">Entrar</button>
        <button @click="logout">Logout</button>
      </div>

    </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Merriweather:ital,opsz,wght@0,18..144,300..900;1,18..144,300..900&display=swap');
.conteudo {
    display: flex;
    justify-content: center;
    flex-direction: row;
    width: 1280px;
    height: 700px;
    position: absolute;
    transform: translate(-50%, -50%);
    top: 51%;
    left: 52%;
}

.imagem img{
  width: 900px;
  height: 700px;
  border-radius: 20px 0px 0px 20px;
}

.login{
  width: 385px;
  height: 700px;
  border-radius: 0px 20px 20px 0px;
  background-color: #32805f ;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.usuario, .senha{
  width: 250px;
  height: 40px;
  padding: 10px;
  border: 1px solid black;
  box-sizing: border-box;
}

.senha,.usuario {
  margin-top: 5%;
  border-radius: 10px;
  
}

.botoes{
  margin-top: 2%;
  display: flex;
  flex-direction: column;
  gap: 10%;
  padding: 10px;
}

.botoes button{
   height: 40px;
   width: 250px;
  border-radius: 10px;
  background-color: #35496E;
  color: white;
  box-shadow: 2px 1px 6px 1px rgba(24, 24, 24, 0.384);
}

.texto h1{
  font-family: "Merriweather", serif;
  font-size: 40px;
  font-weight: 800;
  color: white;
}
</style>