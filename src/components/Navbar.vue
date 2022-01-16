<template>
   <div id="nav">
     <router-link to="/" id="logo-link">
      <img :src="logo" :alt="alt" id="logo">
     </router-link>
    <router-link to="/">Home</router-link>
    <router-link to="/orders">Orders</router-link>
  </div>
</template>
<script>
import { defineComponent } from '@vue/composition-api'

export default {
  name: "Navbar",
  props: ["logo", "alt"]
}
</script>
<style scoped>
  #nav {
    background-color: black;
    border-bottom: 4px solid rgb(29, 29, 29);
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }

  #nav #logo-link {
    margin: auto;
    margin-left: 0;
  }

  #logo {
    width: 120px;
    height: 50px;
  }

  #nav a {
    color: rgb(255, 208, 0);
    text-decoration: none;
    margin: 12px;
    transition: .5s;
  }

  #nav a:hover{
    color: rgb(236, 106, 0);
  }
</style>
