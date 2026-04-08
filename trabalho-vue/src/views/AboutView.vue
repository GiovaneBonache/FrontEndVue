<template>
  <div class="content">
    <!-- Topo: About com quadrado e texto -->
    <div class="about">
      <div class="quadrado" :style="{ backgroundColor: corQuadrado }">
        <h2 style="color:white;text-align:center;margin-top:70px;">Logo</h2>
      </div>
      <div class="desc1">
        <h1>Página Protótipo</h1>
        <p>texto para preencher espaço</p>
      </div>
    </div>

    <!-- Retângulo 1 -->
    <div class="retangulo">
      <h1>Seção 1</h1>
    </div>

    <!-- Quadrados laterais -->
    <div class="formas-laterais">
      <div class="quadrado-pequeno" :style="{ backgroundColor: corQuadrado }">A</div>
      <div class="quadrado-pequeno" :style="{ backgroundColor: corQuadrado }">B</div>
      <div class="quadrado-pequeno" :style="{ backgroundColor: corQuadrado }">C</div>
    </div>

    <div class="retangulo">
      <h1>Seção 2</h1>
    </div>

    <div class="formas-laterais">
      <div class="triangulo"></div>
      <div class="circulo"></div>
      <div class="quadrado-pequeno" :style="{ backgroundColor: corQuadrado }">D</div>
    </div>

    <div class="retangulo">
      <h1>Seção 3</h1>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  corAtiva: String
})

const corQuadrado = ref("#34495E");

watch(() => props.corAtiva, (novaCor) => {
  corQuadrado.value = novaCor;
})
</script>

<style scoped>
html, body {
  height: 100%;   
  width: 100%;  
  margin: 0;
  padding: 0;
}

#app {               
  height: 100%;
  width: 100%;      
}

.content {
  display: flex;
  flex-direction: column;   
  justify-content: flex-start; 
  align-items: center;      
  padding-top: 20px;        
  width: 1300px;           
  background-color: #41B883;
  gap: 20px;
}

.about {
  display: flex;
  flex-direction: row; 
  align-items: center;
  gap: 30px;
  width: 100%;
}

.desc1{
  color: white;
  text-shadow:1px 1px 1px #34495E;
}

.quadrado{
  width: 450px;
  height: 200px;
  border-radius: 16px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.retangulo {
  width: 800px;        
  height: 200px;
  background-color: #34495E;
  border-radius: 16px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.retangulo h1{
  color: white;
  text-shadow:1px 1px 1px #34495E;
}

.formas-laterais {
  display: flex;
  gap: 20px;
  justify-content: center;
}

.quadrado-pequeno{
  width: 150px;
  height: 150px;
  border-radius: 12px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  font-weight: bold;
}

.circulo {
  width: 150px;
  height: 150px;
  background-color: #E74C3C;
  border-radius: 50%;
}

.triangulo {
  width: 0;
  height: 0;
  border-left: 75px solid transparent;
  border-right: 75px solid transparent;
  border-bottom: 150px solid #F1C40F;
}
</style>