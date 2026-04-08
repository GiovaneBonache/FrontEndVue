<template>
  <div class="content">
    <div class="about">
      <div class="quadrado">
        <img src="@/img/vue.png" alt="">
      </div>
      <div class="desc1"><h1>Essa é a pagina home</h1></div>
    </div>

    <div class="retangulo">
      <h1>conteudo</h1>
    </div>

  </div>
  
  
</template>

<style>
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
  padding-top: 10%;        
  width: 1300px;           
  height: 100%;          
  background-color: #41B883;
}

.about {
  display: flex;
  flex-direction: row; 
  align-items: center;
  gap: 30px;
  margin-bottom: 20px;  
}

.retangulo {
  width: 800px;        
  height: 500px;
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
.quadrado{
  width: 450px;
  height: 200px;
  background-color: #34495E;
  border-radius: 16px;
}
.quadrado img{
    width: 40%;
    margin-left: 30%;
    margin-top: 3%;
}

.desc1{
  color: white;
  text-shadow:1px 1px 1px #34495E;
}


</style>
