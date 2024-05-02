<template>
  <div class="info-container" :id="info_id" v-if="showMsg">
        <p>{{ info_msg }}</p>
  </div>
</template>

<script>
export default {
    props: ["info_type","info_msg"],
    data(){
        return {
            info_id: "",
            showMsg: true
        }
    },
    mounted(){
        this.info_id = `info-${this.info_type}`
    },
    beforeUnmount(){
        setTimeout( () => this.showMsg = false, 5000)
    }

}
</script>

<style>

.info-container{
    text-align: center;
    border-radius: 5px;
    margin-bottom: 10px ;
    padding: 10px;
}

#info-sucsess{
    color: #004085;
    background-color: #cce5ff;
    border: 2px solid #b8daff;
}

#info-danger{
    color: #850000;
    background-color: #ffcccc;
    border: 2px solid #ffb8b8;

}
</style>