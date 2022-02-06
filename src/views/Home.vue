<template>
  <Banner />
  <div class="main-container">
    <h1>
      Build your pizza
    </h1>
    <BuildForm />
  </div>
</template>

<script>
  import Banner from "../components/Banner.vue";
  import BuildForm from "../components/BuildForm.vue";

  export default {
    name: "Home",
    components: {
      Banner,
      BuildForm
    }
  }
</script>
