<template>
  <Navbar
    :logo="logo_src"
    :alt="app_name"
  />
  <router-view/>
  <Footer />
</template>

<script>
import Navbar from './components/Navbar';
import Footer from './components/Footer';

export default {
  components: {
    Navbar,
    Footer
  },

  data() {
    return {
      logo_src: "images/logo_black_background.png",
      logo_alt: "Felpizza"
    };
  }
}
</script>

<style>
  * {
    font-family: sans-serif;
    padding: 0px;
    margin: 0px;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height:  250px;
  }

  h1 {
    text-align: center;
    font-size: 45px;
    margin-bottom: 30px;
    color: black;
  }
</style>
