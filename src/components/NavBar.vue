<template>

<nav id="nav">
    <router-link to="/" id="logo-url"> 
        <img :src="logo" :alt="alt" id="logo">
    </router-link> 
    <router-link to="/">Home</router-link> 
    <router-link to="/pedidos">Pedidos</router-link>
    
</nav>
    
</template>


<script>

export default {

    props:["logo","alt"]

}

</script>

<style scoped>

#nav{
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
}

#nav #logo-url{
    margin: auto;
    margin-left: 0;
}

#logo{
    height: 40px;
    width: 40px;
}

#nav a{
    text-decoration: none;
    color: #fcba03;
    margin: 12px;
    transition: .5s;
}

#nav a:hover{
    color: #fff;
}

</style>