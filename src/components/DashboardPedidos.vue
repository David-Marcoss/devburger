<template>
  
  <div id="burger-table">

    <menssageInfo :info_msg="msg.msg" :info_type="msg.type" v-if="msg"/>

    <div v-if="orders.length > 0">
        <div id="burger-table-header">
            <div class="order-id">
                ID
            </div>
            <div>Cliente</div>
            <div>Pão</div>
            <div>Carne</div>
            <div>Opcionais</div>
            <div>Status</div>
        </div>

        <div id="burger-table-rows">
            <div class="burger-table-row" v-for="order in orders" :key="order.id">
                <div class="order-number">
                    {{ order.id }}
                </div>
                <div>{{ order.client }}</div>
                <div>{{ order.bread }}</div>
                <div>{{ order.meat }}</div>
                <div>
                    <ul v-if="order.optionais.length > 0">
                        <li v-for="option in order.optionais" :key="option">{{option}}</li>
                    </ul>
                    <p v-else> Sem Opcionais</p>
                </div>
                <div>
                    <select name="status" class="status" @change="updateStaturOrder($event,order.id)">
                        <option  v-for="status in status" :key="status.id" :value="status.tipo" :selected= "order.status == status.tipo" > {{status.tipo}} </option>
                    </select>
                    <button class="delete-btn" @click="pedidoDelete(order.id)"> cancelar pedido</button>
                </div>
            </div>
        </div>
    </div>
    <div v-else> 
        <h2> Ainda Não há pedidos cadastrados :(</h2>
    </div>
  </div>


</template>

<script>
import axios from 'axios';
import MenssageInfo from './MenssageInfo.vue';

export default {
    components:{
        MenssageInfo
    },
    data(){
        return {
            orders: [],
            status: [],
            msg: null
        }
    },
    methods:{

        async getOrgers(){
            const orders= await axios({
                method: "GET",
                url: "http://localhost:3000/burgers"
            })

            this.orders = orders.data
        },
        async getStatusOrgers(){
            const status= await axios({
                method: "GET",
                url: "http://localhost:3000/status"
            })

            this.status = status.data
        },
        async pedidoDelete(id){
            await axios({
                method: "DELETE",
                url: "http://localhost:3000/burgers/" + id 
            })

            this.getOrgers()
            
            this.msg = {
                    msg: `Pedido N ${id} Cancelado !!!`,
                    type: "sucsess"
            }
        },
        async updateStaturOrder(event,id){
            const status = event.target.value

            console.log( status )
            
            await axios({
                method: "PATCH",
                url: "http://localhost:3000/burgers/" + id,
                data: {status}
            })

            this.getOrgers()
            this.msg = {
                    msg: `Pedido N ${id} atualizado !!!`,
                    type: "sucsess"
            }


        }
    },

    mounted(){
        this.getOrgers()
        this.getStatusOrgers()
    }

}
</script>

<style scoped>

  #burger-table {
    max-width: 1600px;
    margin: 0 auto;
  }

  #burger-table-header,
  #burger-table-rows,
  .burger-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #burger-table-header {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  .burger-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }

  #burger-table-header div,
  .burger-table-row div {
    width: 19%;
  }

  #burger-table-header .order-id,
  .burger-table-row .order-number {
    width: 5%;
  }

  select {
    padding: 12px 6px;
    margin-right: 12px;
  }

  .delete-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  
  .delete-btn:hover {
    background-color: transparent;
    color: #222;
  }

</style>