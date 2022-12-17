<template>
  <div id="nav">
    <router-link to="/" id="logo-url">
        <img :src="logo" :alt="alt" id="logo ">
    </router-link>
    <router-link to="/">Home</router-link> |
    <router-link to="/Pedidos">Pedidos</router-link>
  </div>
</template>

<script>
   export default{
      name: "NavBar",
      props: ["logo","alt"]
    
   }
</script>

<style scoped>

  #nav{
    background-color: #222; /* Cor do fundo */
    border-bottom: 4px solid #111; /* borda em baixo */
    padding: 15px 50px; /* cima-baixo e direita-esquerda */
    display: flex; /* utilizamos display:flex */
    justify-content: flex-end; /* mandamos todo conteudo para o fim "direita" */
    align-items: center; /* alinhdo no centro na vertical */
  }

  #nav #logo-url{
    margin:auto;
    margin-left:0;
  }

  #nav a{
    color: #FCBA03;
    text-decoration: none;
    margin: 12px;
    transition: .5s; /* Muda a cor de amarelo para branco em 5s */
  }

  #nav a:hover{
    color: #FFF; /* Ao clicar no link fica branco */
  }

</style>