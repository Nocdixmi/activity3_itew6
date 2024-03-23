<template>
  <div class="cart">
    
    <table style="width:100%; table-layout: fixed;" align="center">
      <th>Product Name</th>
      <th>Price</th>
      <th>Unit Price</th>
      <th>Quantity</th>
      <th>Edit Quantity</th>
      <th>Remove from Cart</th>
      <tr v-for="(item, index) in cart" :key="index">
        <td>{{ item.name }}</td>
        <td align="right">₱{{ computedItemPrice(item) }}</td>
        <td align="right">₱ {{ item.unitPrice }}</td>
        <td align="right">{{ item.quantity }}</td>
        <td><button @click="editQuantity(index)">Edit</button></td>
        <td><button @click="removeFromCart(index)">Remove</button></td>
      </tr>
    </table>

    <div class="prices">
      <p>Total Price: ₱{{ totalPrice }}</p>
    </div>
    <br>
    <br>
    <button @click="handleLogout">Logout</button>
    
  </div>
</template>

<script>
import { cart } from "../main.js";

export default {
  data() { 
    return {
      cart: cart,
    };
  },
  methods: {
    removeFromCart(index) {
      if (confirm("Are you sure you want to remove this item from the cart?")) {
        this.cart.splice(index, 1);
      }
    },
    editQuantity(index) {
      const newQuantity = prompt("Enter the new quantity:", this.cart[index].quantity);
      let unitPrice = this.cart[index].price / this.cart[index].quantity;
      if (newQuantity !== null && !isNaN(newQuantity) && newQuantity > 0) {
        this.cart[index].price = unitPrice * newQuantity;
        this.cart[index].quantity = parseInt(newQuantity);
      }
    },
    handleLogout() {
      localStorage.removeItem('token')
      this.$router.push('/login')
    },
    computedItemPrice(item) {
      return item.unitPrice * item.quantity;
    }
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => total + this.computedItemPrice(item), 0);
    }
  }
};
</script>

<style>
table, th, td {
  border: 1px solid black;
}
</style>
