<template>
  <div id="app">
    <h1>Simple Product List</h1>
    <div style="width:880px; margin:auto; position:relative;">
      <button @click="addNewProduct" style="position:relative; right:26rem; margin-bottom: 20px;">New</button>
      <div class="margin-top:10px;">
        <table>
          <thead>
            <tr>
              <th>Product Name</th>
              <th>Product Price</th>
              <th>Quantity</th>
              <th>Total</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(product, index) in products" :key="index">
              <td><input v-model="product.name" /></td>
              <td><input v-model="product.price" type="number" /></td>
              <td><input v-model="product.qty" type="number" @input="calculateTotal" /></td>
              <td>{{ product.total }}</td>
              <td><button @click="removeProduct(index)">Delete</button></td>
            </tr>
          </tbody>
        </table>
        <div>
          <b>Grand Total: {{ grandTotal }}</b>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { name: "", price: 0, qty: 0, total: 0 }
      ]
    };
  },
  computed: {
    grandTotal() {
      return this.products.reduce((total, product) => total + product.total, 0);
    }
  },
  methods: {
    calculateTotal() {
      this.products.forEach(product => {
        product.total = product.price * product.qty;
      });
    },
    addNewProduct() {
      this.products.push({ name: "", price: 0, qty: 0, total: 0 });
    },
    removeProduct(index) {
      if (this.products.length > 1) {
        this.products.splice(index, 1);
      }
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

button {
  background-color: #f44336;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}

button:hover {
  background-color: #d32f2f;
}
</style>
