<template>
  <BannerVue/>
  <div class="main-container">
    <h1>Monte seu Hamburguer</h1>

    <FormBurguer/>

 
  </div>
</template>

<script>
import BannerVue from '@/components/BannerVue.vue'
import FormBurguer from '@/components/FormBurguer.vue'

export default {

  components:{
    BannerVue,
    FormBurguer
  }

}
</script>
