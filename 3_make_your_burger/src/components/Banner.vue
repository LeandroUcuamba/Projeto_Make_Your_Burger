<template>
  <div id="main-banner">
    <h1>Make Your Banner</h1>
  </div>
</template>

<script>
   export default{
      name: "Banner"
   }
</script>

<style scoped>

  #main-banner{
    background-image: url('../../public/img/burger.jpg');
    background-position:  0 -250px; /* Deslocando o banner no eixo y */
    background-size: cover; /* Deixa a img aparecer o maximo possivel*/
    height: 500px;
    display:flex;
    align-items: center;
    justify-content: flex-start;
  }

  #main-banner h1{
      color: #fff;
      text-align: center;
      font-size: 60px;
      background-color: #222;
  }

</style>