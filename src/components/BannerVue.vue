<template>
  <div id="banner">
    <div id="banner-text">
      <h1>DeV Burguer</h1>
      <p> Monte seu pedido de acordo com seu gosto, de maneira simples e facil.</p>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>

#banner{
  background-image: url('/public/img/burger.jpg');
  background-position: 0 -450px;
  background-size: cover ;
  background-repeat: no-repeat;
  max-width: 100%;
  height: 680px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  margin-bottom: 100px;

}

#banner #banner-text{
  padding: 50px;
  text-align: left;
  color: #fff;
  max-width: 700px;
}

#banner-text h1{
  text-align: left;
  font-size: 50px;
  color: #ffffff;
}

#banner-text p{
  color: #a8a8a8;
  font-size: 30px;
}



</style>