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


</script>

<template>
  <div class="conteudo">
    <div class="imagem">
      <img src="@/img/vueimagem.jpeg" alt="">
    </div>
    <div class="login">
      <div class="texto">
        <h1>Login</h1>
      </div>
      <div >
        <input class="usuario" v-model="email" placeholder="Usuario" />
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
.conteudo{
  display: flex;
  justify-content: center;
  flex-direction: row;
  width: 1280px;
  height: 700px;
  
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
  padding: 10px;
  border: 1px solid black;
  box-sizing: border-box;
}

.usuario input, .senha input{
  width: 100%;
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
}
</style>