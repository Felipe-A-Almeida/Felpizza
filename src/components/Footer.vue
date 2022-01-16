<template>
  <div id="footer">
    <p>Felpizza &copy; 2021</p>
  </div>
</template>

<script>
export default {
  name: "Footer"
}
</script>

<style scoped>
  #footer {
    height: 200px;
    background-color: black;
    border-top: 4px solid rgb(43, 43, 43);
    color: rgb(255, 208, 0);
    display: flex;
    align-items: center;
    justify-content: center;
    bottom: 0;
    width: 100%;
  }
</style>