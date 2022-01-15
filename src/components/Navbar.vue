<template>
   <div id="nav">
     <router-link to="/">
      <img src="" alt="" id="logo">
     </router-link>
    <router-link to="/">Home</router-link> |
    <router-link to="/orders">Orders</router-link>
  </div>
</template>
<script>
import { defineComponent } from '@vue/composition-api'

export default {
  name: "Navbar"
}
</script>
<style scoped>

</style>
