<template>
  <div>
     <Message :msg="msg" v-show="msg" />
     <div>
        <form id="burger-form" @submit="createBurger">
            <div class="input-container">
               <label for="nome">Nome do cliente:</label>
               <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite o seu nome" />
            </div>
            <div class="input-container">
               <label for="pao">Escolha o pão:</label>
               <select name="pao" id="pao" v-model="pao">
                  <option value="">Selecione o seu pão</option>
                  <option v-for="pao in paes" :key="pao.id" :value="pao.tipo"> 
                  {{pao.tipo}} </option>
               </select>
            </div>
            <div class="input-container">
               <label for="carne">Escolha a carne do seu Burger:</label>
               <select name="carne" id="carne" v-model="carne">
                  <option value="">Selecione o seu pão</option>
                  <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo"> 
                  {{carne.tipo}} </option>
               </select>
            </div>
            <div id="opcionais-container" class="input-container">
               <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
               <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                 <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo" />
                 <span>{{opcional.tipo}}</span>
               </div>
            </div>
            <div class="input-container">
               <input type="submit" class="submit-btn" value="Criar seu burger" />
            </div>
        </form>
     </div>
  </div>
</template>

<script>
   
   import Message from "./Message.vue";

   export default{
     name: "BurgerForm",
     data(){
        return{
            paes: null, // dados preenchido depois no getIngrediente;
            carnes: null, // dados preenchido depois no getIngrediente;
            opcionaisdata: null, // dados preenchido depois no getIngrediente;
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            msg: null
        }
     },
     components:{
        Message
     },
     methods:{
        //Metodo para buscar os dados do json
        async getIngredientes(){

           const req = await fetch("http://localhost:3000/ingredientes");
           const data = await req.json();

           //Preenchendo os dados do data() com os dados que veem do servidor;
           this.paes = data.paes;
           this.carnes = data.carnes;
           this.opcionaisdata = data.opcionais;

        },

        async createBurger(e){
  
           e.preventDefault();
        
           const data = {
              nome: this.nome,
              carne: this.carne,
              pao: this.pao,
              opcionais: Array.from(this.opcionais),
              status: "Solicitado"
           }

         // O navegador não entendi obj, então vamos converter o obj -> txt;
         const dataJson = JSON.stringify(data);

         const req = await fetch("http://localhost:3000/burgers", {
            //isso é para ele entender que é post e não GET como padrão;
            method: "POST",
            headers: { "Content-Type": "application/json" }, //para dizer que estou me comunicando com json;
            body: dataJson //O corpo da requisição vai enviar os dados do "dataJson";
         });

         const res = await req.json();

         //Colocar uma msm no sistema;
         this.msg = `Pedido N ${res.id} realizado com sucesso`;

         //Limpar mensagem;
         setTimeout(()=>{
             this.msg ="";
         }, 3000)

         //Limpar os campos;
         this.nome= "";
         this.carne = "";
         this.pao = "";
         this.opcionais ="";
                            
        },
     },

     //Para executar o metodo quando carregar a pagina;
     mounted(){
        this.getIngredientes();
     }
   }//fim export default
</script>

<style scoped>

  #burger-form{
    max-width: 400px; /* largura maxima */
    margin: 0 auto; /* para cetralizar os elementos filhos no centro */
  }

  .input-container{
    display: flex; /* utilizamos flex */
    flex-direction: column; /* para aparecerem em coluna "um abaixo do outro" */
    margin-bottom: 20px;
  }

  label{
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px; 
    border-left: 4px solid #FCBA03;
  }

  input, select{
    padding: 5px 10px;
    width: 300px;
  }

  #opcionais-container{
     flex-direction: row;
     flex-wrap: wrap;
  }

  #opcionais-title{
    width: 100%;
  }

  .checkbox-container{
     display: flex;
     align-items: flex-start;
     width: 50%;
     margin-bottom: 20px;
  }

  .checkbox-container span, .checkbox-container input{
     width: auto;
  }
  .checkbox-container span{
      margin-left: 6px;
      font-weight: bold;
  }

  .submit-btn{
    background-color: #222;
    color: #FCBA03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

   .submit-btn:hover{
      background-color: transparent;
      color: #222;
   }

</style> 