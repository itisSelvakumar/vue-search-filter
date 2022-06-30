<template>
  <div class="filter">
    <h1>{{ msg }}</h1>
    
    <div class="option-group">
      <div class="options">
        <label for="category">Select category</label>
        <select v-model="category" id="category">
          <option value="">Select</option>
          <option value="Car">Car</option>
          <option value="Bike">Bike</option>
          <option value="Flight">Flight</option>
        </select> 
      </div>

      <div class="options">
        <label for="name">Search by name</label>
        <input type="text" v-model="name" id="name" placeholder="Filter By Name"/>
      </div>

      <div class="options">
        <label for="vol">Price (between 0 and 100000):</label>
        <input type="range" id="vol" v-model="range" min="0" max="100000" step="1000" />
      </div>
    </div>

    <ul>
        <li v-for="(product, index) in filterProducts" v-bind:key="index"> {{ index + 1 }}. {{product.name}} - Price : {{product.price}} ({{product.category}})</li>
    </ul>
    
  </div>
</template>

<script>
export default {
  name: 'FilterComponent',
  props: {
    msg: String
  },

  data: function() {
    return {
      category: '',
      name: '',
      range: '50000',
      products: [
          { name: "Audi", price: 4400, category: 'Car'},
          { name: "BMW", price: 2000, category: 'Car'},
          { name: "Suzuki", price: 39900, category: 'Car'},
          { name: "TATA", price: 5990, category: 'Bike'},
          { name: "YAMAGA", price: 8990, category: 'Bike'},
          { name: "Air India", price: 60000, category: 'Flight'},
          { name: "Spice Jet", price: 20000, category: 'Flight'},
          { name: "Hundai", price: 70000, category: 'Car'},
          { name: "IndiGo", price: 20000, category: 'Flight'},
          { name: "Dutch Airlines", price: 50000, category: 'Flight'}
      ]
    }
  },

  computed: {
    filterProducts: function(){
      return this.filterProductsByRange(this.filterProductsByName(this.filterProductsByCategory(this.products)))
    }
  },
        
  methods: {
    filterProductsByCategory: function(products){
      return products.filter(product => !product.category.indexOf(this.category))
    },
    filterProductsByName: function(products) {
      return products.filter(product => !product.name.indexOf(this.name))
    },
    filterProductsByRange: function(products){
      return products.filter(product => (product.price > 0 && product.price < this.range) ? product : '')
    }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
[v-cloak] {
  display: none;
}

*{
    margin:0;
    padding:0;
}
h1 {
  margin: 50px;
}
label,
input,
select {
  width: 200px;
  height: 30px;
  margin: 0 10px;
  text-align: left;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
input {
    padding: 10px;
}
ul{
    list-style: none;
    width: 428px;
    margin: 0 auto;
    text-align: left;
}

ul li{
    border-bottom: 1px solid #ddd;
    padding: 10px;
    overflow: hidden;
}

.option-group {

  display: flex;
  align-items: baseline;
  justify-content: center;
  
}

.option-group .options {
  display: flex;
  align-items: baseline;
  justify-content: center;
  flex-direction: column;

}

</style>
