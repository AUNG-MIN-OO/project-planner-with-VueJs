<template>
  <nav class="main-nav">
      <router-link to="/" class="first-link routerlink-css text-uppercase">Projects</router-link>
      <router-link :to="{name:'AddProject'}" class="second-link routerlink-css text-uppercase">Add Projects</router-link>
  </nav>
</template>

<script>
export default {
    
}
</script>

<style>
    .main-nav{
        text-align: center;
        margin-top: 30px;
        margin-bottom: 30px;
    }
    .routerlink-css{
        text-decoration: none;
        color: #ba53de;
        font-size: 20px;
        font-weight: bold;
        transition: all ease-in-out .2s;
    }
    a.router-link-active{
        border-bottom: 5px solid #ba53de;
    }
    .first-link{
        margin-right: 30px;
    }
</style>