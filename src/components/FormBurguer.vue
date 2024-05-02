<template>
  
  <div>
      
      <form id="form-burguer" @submit.prevent="createOrder">
        <MenssageInfo v-if="msg" :info_type="msg.type" :info_msg="msg.msg"/>
        <div class="container-input">
            <label for="name"> Nome do Cliente</label>
            <input type="text" id="name" name="name" v-model="client" placeholder="Digite seu nome">
        </div>
        <div class="container-input">
            <label for="bread"> Tipo de pão</label>
            <select name="bread" id="bread" v-model="bread">

                <option v-for=" bread in Ingredients_breads" :key="bread.id" :value="bread.tipo"> {{ bread.tipo }}</option> 

            </select>
            
        </div>

        <div class="container-input">
            <label for="meat"> Tipo de carne</label>
            <select name="meat" id="meat" v-model="meat">

                <option v-for=" meat in Ingredients_meats" :key="meat.id" :value="meat.tipo"> {{ meat.tipo }}</option> 

            </select>
            
        </div>

        <div id="options-container" class="container-input">
            <label for="options" id="options-title"> Selecione os opcionais</label>
            <div class="checkbox-input" v-for=" option in Ingredients_optionais" :key="option.id">
                <input type="checkbox"  v-model="optionais" id="options" name="options" :value="option.tipo">
                <span>{{ option.tipo }}</span>
            </div>
            
            
            

        </div>
        
        <div class="container-input">
            <input type="submit" class="submit-btn" value="Criar pedido">
        </div>   

    </form>
  </div>

</template>

<script>

import axios from 'axios';
import MenssageInfo from "@/components/MenssageInfo.vue"

export default {
    components:{
        MenssageInfo,
    },

    data(){
        return {
            Ingredients_breads: null,
            Ingredients_meats: null,
            Ingredients_optionais: null,
            client: null,
            bread: null,
            meat: null,
            optionais: null,
            msg: null
            
        }
    },

    methods: {
        
        async getIngredients(){
            const ingredients = await axios({
                method: "GET",
                url: "http://localhost:3000/ingredientes"}
            )
            
            this.Ingredients_breads = {...ingredients.data.paes}
            this.Ingredients_meats = {...ingredients.data.carnes}
            this.Ingredients_optionais = {...ingredients.data.opcionais}

        },

        async createOrder(){
            
            console.log(this.client, this.bread , this.meat, this.optionais)

            if( this.client && this.bread && this.meat){

                this.optionais = this.optionais != null ? Array.from(this.optionais): []

                const order = {
                    client: this.client,
                    bread: this.bread,
                    meat: this.meat,
                    optionais: this.optionais,
                    status: "Criado"
                }

                const req = await axios({
                    method: "POST",
                    url: "http://localhost:3000/burgers",
                    data: order
                })

                this.client , this.bread, this.meat = null
                
                this.msg = {
                    msg: `Pedido Numero:${req.data.id} criado com sucesso !!!`,
                    type: "sucsess"
                }
                
                
            }else{
                this.msg = {
                    msg: "Não foi possivel criar pedido, Preencha as informações corretamente!!!",
                    type: "danger"
                }
            }
        }
    },

    mounted(){
        this.getIngredients()
    }

}
</script>

<style scoped>

#form-burguer{
    max-width: 400px;
    margin: 0 auto;
}

.container-input{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label{
    font-size: 20px;
    font-weight: bold ;
    color: #222;
    margin-bottom: 5px ;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
}

select{
    height: 35px;
    padding: 5px 10px;
    max-width: 300px;
}

#name{

    height: 35px;
    padding: 5px 10px;
    max-width: 300px;
}

#options-container{
    flex-direction: row;
    flex-wrap: wrap;
}

#options-title{
    width: 100%;
}

.checkbox-input{
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkbox-input span, .checkbox-input input{
    width: auto;
}

.checkbox-input span{
    margin-left: 5px;
}

.submit-btn{
    background-color: #222;
    color: #fcba03;
    border: 2px solid #222;
    font-weight: bold;
    padding: 10px;
    font-size: 16px;
    cursor: pointer;
    transition: .5s;
}

.submit-btn :hover{
    background-color: transparent;
    color: #390000;
}

</style>