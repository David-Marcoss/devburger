<template>

  <div>
    
    <NavBar :logo="logo_src" :alt="app_name"/>
    
    <div>
      <router-view/>
    </div>

    <FooterVue/>
  </div>
 
  
</template>

<script>

import FooterVue from './components/FooterVue.vue'
import NavBar from "./components/NavBar.vue"

export default {
  components:{
    NavBar,
    FooterVue
  },

  data(){
    return {
      logo_src: "/img/logo.png",
      app_name: "DevBurger"
    }
  }
}

</script>

<style>

*{
  margin: 0;
  padding: 0;
  font-family: Helvetica;
  box-sizing: border-box;
}

.main-container{
  margin: 50px;
  overflow-y: auto; /* Permite a rolagem vertical */
  height: calc(100% - 100px); /* Altura dinâmica para preencher a tela entre o menu e o footer */
}

h1{
  text-align: center;
  font-size: 48px;
  margin-bottom: 40px;
  color: #222

}

</style>
