<template>
  <div 
    class="message-container"
  >
    <p>
      {{ this.message }}
    </p>
  </div>
</template>


<script>
export default {
  name: "Message",
  props: {
    message: {
      type: String,
      default: null,
    }
  }
}
</script>

<style scoped>  
  .message-container {
    color: rgb(29, 80, 95);
    background-color: rgb(142 232 255 / 76%);
    border: 2px solid rgb(123 225 255);
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
  }
</style>