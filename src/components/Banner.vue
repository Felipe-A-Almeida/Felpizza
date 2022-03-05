<template>
  <div id="main-banner">
    <div class="banner-text">
      <h1>
        Welcome to Felpizza's pizzaria
      </h1>
      <h2>
        Build your own pizza selecting the ingredients based on your tastes
      </h2>
    </div>
  </div>
</template>

<script>
export default {
  name: "Banner"
}
</script>

<style scoped>
  #main-banner {
    height: 500px;
    background-image: url('/images/banner_home.png');
    background-position: 0 -250px;
    background-size: cover;
  }

  .banner-text {
    height: 500px;
    display: table-cell;
    vertical-align: middle;
    text-align: center;
  }

  #main-banner h1 {
    color: rgb(255, 208, 0);
    text-align: center;
    font-size: 58px;
    padding: 20px 40px;
    display: flex;
  }

  #main-banner h2 {
    color: rgb(255, 228, 109);
  }
</style>