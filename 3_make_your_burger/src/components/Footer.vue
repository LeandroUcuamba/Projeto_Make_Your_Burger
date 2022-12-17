<template>
  <footer id="footer">
      <p>Make Your Burger &COPY; 2022</p>
  </footer>
</template>

<script>
   export default{
      name: "Footer"
    
   }
</script>

<style scoped>
   #footer{
      height: 200px; /* Altura */
      background-color: #222; /* Cor do fundo */
      border-top: 4px solid #111;
      color: #FCBA03; /* Cor da letra */
      display: flex; /* utilizando isto: */
      align-items: center; /* alinha o conteudo no centro vista "vertical" */
      justify-content: center; /* alinha o conteudo no centro vista "horizontal" */
      bottom: 0; /* posicionando 0 para baixo "só para posicionar"*/
      width: 100%; /* Assegurando que ele vai preencher a tela 100% na largura*/
   }

</style>