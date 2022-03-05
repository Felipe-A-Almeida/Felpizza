<template>
  <div id="pizza-table">
    <Message
      v-show="this.message"
      :message="message"
    />
    <div>
      <div id="pizza-table-header">
        <div class="order-id">
          #
        </div>
        <div> Client </div>
        <div> Size </div>
        <div> Sauce </div>
        <div> Chesse </div>
        <div> Meat </div>
        <div> Additives </div>
        <div> Actions </div>
      </div>
      <div id="pizza-table-rows">
        <div 
          v-for="pizza in pizzas"
          :key="pizza.id"
          class="pizza-table-row"          
        >
          <div class="order-number"> {{ pizza.id }}</div>
          <div>{{ pizza.name }}</div>
          <div> {{ pizza.size }} </div>
          <div> {{ pizza.sauce }} </div>
          <div> {{ pizza.cheese }} </div>
          <div> {{ pizza.meat }} </div>
          <div>
            <ul>
              <li
                v-for="(additive, index) in pizza.additives"
                :key="index"
              >
                {{ additive }}
              </li>
            </ul>
          </div>
          <div>
            <select 
              name="status" 
              id="status"
              @change="updatePizza($event, pizza.id)"
            >
              <option value="">Select</option>
              <option 
                v-for="s in status"
                :key="s.id"
                :value="s.name" 
                :selected="pizza.status == s.name" 
              >
                {{ s.name }}  
              </option>
            </select>
            <button class="delete-btn" @click="deletePizza(pizza.id)">Cancel</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Message from './Message.vue';

export default {
  name: 'Dashboard',

  components: {
    Message,
  },


  data() {
    return {
      pizzas: null,
      pizza_id: null,
      status: [],
      message: null,
    }
  },

  mounted() {
    this.getOrders();
  },

  methods: {
    async getOrders() {
      const request = await fetch("http://localhost:3000/orders");

      const data = await request.json();

      this.pizzas = data;

      this.getStatus();
    },

    async getStatus(){
      const request = await fetch("http://localhost:3000/status");

      const data = await request.json();

      this.status = data;      
    },

    async deletePizza(id) {
      const request = await fetch(`http://localhost:3000/orders/${id}`, {
        method: "DELETE"
      });

      const data = await request.json();

      this.message = 'Successfully deleted';

      setTimeout(() => this.message = "", 3000);

      this.getOrders();
    },

    async updatePizza(event, id){
      const status = event.target.value;

      const dataJson = JSON.stringify({ status: status });

      const request = await fetch(`http://localhost:3000/orders/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJson
      });

      const response = await request.json();

      console.log(response);

      this.message = `Successfully updated the order ${ response.id }`;

      setTimeout(() => this.message = "", 3000);
    }
  }
}
</script>

<style scoped>
  #pizza-table {
    max-width: 1200px;
    margin:  0 auto;
  }

  #pizza-table-header,
  #pizza-table-rows,
  .pizza-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #pizza-table-header {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  #pizza-table-header div,
  .pizza-table-row div {
    width: 12%;
  }

  .pizza-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCCC;
  }

  #pizza-table-header .order-id,
  .pizza-table-row .order-number {
    width: 5%;
  }

  select {
    padding: 12px 6px;
    margin-right: 12px;
  }

  .delete-btn {
    background-color: #222;
    color: #FCBA03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .delete-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>