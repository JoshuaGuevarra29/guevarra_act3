<template>
    <div class="item">
      <table>
        <tr>
          <th>Items</th>
          <th>Price</th>
          <th>Quantity</th>
          <th>Cancel Order</th>
        </tr>
        <tr>
          <td>{{ item.name }}</td>
          <td>P {{ item.price }}</td>
          <td>
            <div class="quantity">
              <button @click="updateQuantity('increment')">+</button>
              <span>{{ item.quantity }}</span>
              <button @click="updateQuantity('decrement')">-</button>
            </div>
          </td>
          <td>
            <button @click="removeFromCart">Cancel</button>
          </td>
        </tr>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      item: {
        type: Object,
        required: true
      }
    },
    methods: {
      removeFromCart() {
        this.$emit('remove-from-cart');
      },
      updateQuantity(action) {
        if (action === 'increment') {
          this.item.quantity++;
        } else if (action === 'decrement' && this.item.quantity > 1) {
          this.item.quantity--;
        }
        this.$emit('update-quantity');
      }
    }
  };
  </script>
  
  <style scoped>
  .cart-item {
    margin-bottom: 10px;
  }
  
  table {
    width: 100%;
    border-collapse: collapse;
  }
  
  th, td {
    width: 100%;
    border: 1px solid #ddd;
    padding: 8px;
    text-align: center;
  }
  
  th {
    background-color: #646060;
  }
  
  .quantity {
    display: flex;
    align-items: center;
  }
  
  .quantity button {
    padding: 4px 8px;
    margin: 0 4px;
    border: none;
    background-color: #03e73cf8;
    color: rgb(148, 141, 141);
    cursor: pointer;
  }
  
  .quantity button:hover {
    background-color: #757c85;
  }
  </style>