<template>
  <div class="products">
    <table style="width:50%; table-layout: fixed;" align="center">
      <th>Product Name</th>
      <th>Price</th>
      <th>Button</th>
      <tr v-for="item in products" :key="item.id">
        <td>{{ item.name }}</td>
        <td align="right">₱{{ item.price }}</td>
        <td><button @click="addToCart(item)">Add to Cart</button></td>
      </tr>
    </table>
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
      products: [
        { name: "Rose", price: 500 },
        { name: "Sunflower", price: 600 },
        { name: "Tulip", price: 650 },
        { name: "Daisy", price: 550 },
        { name: "Orchid", price: 499 },
        { name: "Lily", price: 699 },
        { name: "Carnation", price: 899 },
        { name: "Hydrangea", price: 999 },
        { name: "Peony", price: 679 },
        { name: "Gerbera Daisy", price: 799 }
      ],
    };
  },
  methods: {
    addToCart(item) {
      if (localStorage.getItem('token')) {
        let existingItemIndex = cart.findIndex(cartItem => cartItem.name === item.name);

        if (existingItemIndex !== -1) {
          cart[existingItemIndex].quantity++;
        } else {
          let totalPrice = item.price;
          let unitPrice = item.price;
          cart.push({
            name: item.name,
            price: totalPrice,
            unitPrice: unitPrice,
            quantity: 1
          });
          alert("You successfully added this product to the cart!");
        }
      } else {
        alert("Please login first to add items to the cart.");
        this.$router.push('/login');
      }
    },
    handleLogout() {
      localStorage.removeItem('token')
      this.$router.push('/login')
    },
  },
};
</script>

<style>
table, th, td {
  border: 2px solid gray  ;
}
</style>
