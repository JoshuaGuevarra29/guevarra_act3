<template>
  <div id="app">
    <div class="container">
      <div class="products">
        <h2>Yamaha Motorcyles</h2>
        <table>
          <tr>
            <th>Product</th>
            <th>Price</th>
          </tr>
          <tr v-for="product in products" :key="product.id">
            <td>{{ product.name }}</td>
            <td>P{{ product.price }}</td>
            <td><button @click="addToCart(product)">Add to Cart</button></td>
          </tr>
        </table>
      </div>
      <div class="cart">
        <h2>Cart</h2>
        <div v-if="cart.length === 0">
          Click Add to Cart to place an order
        </div>
        <div v-else>
          <item v-for="(item, index) in cart" :key="index" :item="item" @remove-from-cart="removeCart(index)" @update-quantity="updateQuantity(index)"></item>
          <p>Total Amount: ₱{{ total }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Item from './components/Item.vue';

export default {
  components: {
    Item
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Mio Gravis 125', price: 86000 },
        { id: 2, name: 'Mio Fazzio', price: 93000 },
        { id: 3, name: 'Mio Aerox 155', price: 135000 },
        { id: 4, name: 'Sniper 155', price: 128000 },
        { id: 5, name: 'NMAX 155', price: 151000 },
      ],
      cart: []
    };
  },
  computed: {
    total() {
      return this.cart.reduce((total, item) => total + item.price * item.quantity, 0);
    }
  },
  methods: {
    addToCart(product) {
      let stockItem = this.cart.find(item => item.id === product.id);
      if (stockItem) {
        stockItem.quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    removeCart(index) {
      this.cart.splice(index, 1);
    },
    updateQuantity(index) {
      if (this.cart[index].quantity < 1) {
        this.cart[index].quantity = 1;
      }
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: left;
  margin-top: 100px;
}

.products, .cart {
  color: white;
  text-align: center;
  width: 100%,100%;
  max-width: 800px;
  border: 1px solid #ccc;
  padding: 1px;
}

.products table, .cart table {
  border-color: rgb(255, 252, 252);
  width: 100%;
  border-collapse: collapse;
}

.products th, .products td, .cart th, .cart td {
  border: 1px solid #13121200;
  padding: 10px;
}

.products button {
  cursor: pointer;
}

</style>