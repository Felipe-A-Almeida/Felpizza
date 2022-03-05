<template>
  <div>
    <Message
      v-show="this.message"
      :message="message"
    />
    <div>
      <form 
        id="pizza-builder-form"
        @submit="createPizza"
      >
        <div class="input-container">
          <label for="name">
            Name
          </label>
          <input type="text" id="name" name="name" v-model="form.name" placeholder="Enter your name">
        </div>
        <div class="input-container">
          <label for="size">
            Choose your pizza size
          </label>
          <select name="size" id="size" v-model="form.size">
            <option value="">Select a option</option>
            <option 
              v-for="size in sizes"
              :key="size.id"
              :value="size.name"
            >
              <span
                class="size-name"
              >
                {{ size.name }} - 
              </span>
              <p
                class="size-description"
              >
                {{ size.description }}
              </p>
            </option>
          </select>          
        </div>
        <div class="input-container">
          <label for="sauce">
            Choose your pizza sauce
          </label>
          <select name="sauce" id="sauce" v-model="form.sauce">
            <option value="">Select a option</option>
            <option
              v-for="sauce in sauces"
              :key="sauce.id"
              :value="sauce.name"
            >
              {{ sauce.name }}
            </option>
          </select>          
        </div>
        <div class="input-container">
          <label for="cheese">
            Choose your pizza cheese
          </label>
          <select name="cheese" id="cheese" v-model="form.cheese">
            <option value="">Select a option</option>
            <option
              v-for="cheese in cheeses"
              :key="cheese.id"
              :value="cheese.name"
            >
              {{ cheese.name }}
            </option>
          </select>          
        </div>
        <div class="input-container">
          <label for="meat">
            Choose your pizza meat
          </label>
          <select name="meat" id="meat" v-model="form.meat">
            <option value="">Select a option</option>
            <option
              v-for="meat in meats"
              :key="meat.id"
              :value="meat.name"
            >
              {{ meat.name }}
            </option>
          </select>          
        </div>
        <div class="input-container" id="additives-container">
          <label id="additives-title" for="additives">
            Choose your pizza additives
          </label>
          <div 
            v-for="additive in allAdditives"
            :key="additive.id"
            class="checkbox-container"
          >
            <input type="checkbox" name="additives" id="additives" v-model="form.additives" :value="additive.name">
            <span> {{ additive.name }}</span>
          </div>
        </div>
        <div class="input-container">
          <input type="submit" class="submit-btn" value="Create pizza">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from './Message.vue';
export default {
  name: 'BuildForm',

    components: {
      Message,
    },

    data() {
    return {
      form:{
        size: null,
        sauce: null,
        cheese: null,
        meat: null,
        additives: [],
        name: null,
        status: "Ordered",
      },
      message: null,
      sizes: null,
      sauces: null,
      cheeses: null,
      meats: null,
      allAdditives: null,
    }
  },
  methods: {
    async getIngredients() {

      const request = await fetch("http://localhost:3000/ingredients");
      const data = await request.json();
       
      console.log(data);

      this.sizes = data.sizes;
      this.sauces = data.sauces;
      this.cheeses = data.cheeses;
      this.meats = data.meats;
      this.allAdditives = data.additives;
    },

    async createPizza(event) {
      event.preventDefault();

      const data = {
        name: this.form.name,
        size: this.form.size,
        sauce: this.form.sauce,
        cheese: this.form.cheese,
        meat: this.form.meat,
        additives: Array.from(this.form.additives),
        status: "Ordered",
      }

      const dataJson = JSON.stringify(data);

      const request = await fetch('http://localhost:3000/orders', {
        method: "POST",
        headers: {
          'Content-Type': 'application/json'
        },
        body: dataJson
      });
      
      const response = await request.json();

      this.message = `Successfully ordered! Your number is ${ response.id }`;

      setTimeout(() => this.message = "", 3000);

      this.clearForm();
    },

    clearForm() {
      for (var field in this.form) { 
        this.form[field] = Array.isArray(this.form[field]) ? [] : null;
      };
    }
  },
  mounted() {
    this.getIngredients();
  }
}
</script>

<style scoped>
  #pizza-builder-form {
    max-width: 300px;
    margin: 0 auto;
  }

  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: black;
    padding: 5px 10px;
    border-left: 4px solid rgb(255, 208, 0);
  }

  input, select {
    padding: 5px 10px;
    width: 300px;
  }

  #additives-container {
    flex-direction: row;
    flex-wrap: wrap;
  }

  #additives-title {
    width: 100%;
  }

  .checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
  }

  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }

  .checkbox-container span{
    margin-left: 6px;
    font-weight: bold;
  }

  .submit-btn {
    background-color: black;
    color: rgb(255, 208, 0);
    font-weight: bold;
    border: 2px solid black;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: black;
  }

</style>