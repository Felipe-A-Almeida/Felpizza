<template>
  <div id="pizza-table">
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
            <select name="status" id="status">
              <option value="">Select</option>
            </select>
            <button class="delete-btn">Cancel</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dashboard',
  data() {
    return {
      pizzas: null,
      pizza_id: null,
      status: []
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